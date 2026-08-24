# Descripción general del servidor TCI

El applet del Servidor TCI ejecuta un servidor WebSocket que habla el protocolo TCI de Expert Electronics, permitiendo que aplicaciones de registro, modos digitales y SDR de terceros — como Log4OM y herramientas SunSDR — lean y controlen la radio a través de una conexión de red local. Abra el applet para iniciar el servidor, configurar el puerto y ajustar la ganancia de audio para cada canal RX y TX.

- El audio TX de TCI se recibe a través del WebSocket y se introduce en una ranura de flujo dedicada `dax_tx`, independiente de la ruta del dispositivo de audio DAX2 de SmartSDR para Windows. Así, el TX de TCI funciona en todas las plataformas, incluidas Windows y Linux, sin PipeWire (v0.9.5.1).
- Se corrigió un fallo al salir en la v0.9.7: TciServer ahora se cierra explícitamente en `~MainWindow()` después de que el hilo de audio se detiene, pero mientras `RadioModel` sigue activo, evitando un uso-después-de-liberación mediante `releaseDaxForTci()`. Se añadió un `QPointer<RadioModel>` como refuerzo adicional para que las comprobaciones de nulidad existentes detecten automáticamente cualquier regresión futura.
- Se añadieron tres comandos TCI v2.0 (`volume`, `drive`, `rx_volume`) a la tabla de despacho con sincronización de estado bidireccional en la v26.5.1.
- El reenvío del espectro del panadapter y `tx_gain` / `ALC` se añadieron en la v26.5.3.
- Haga clic derecho en el control deslizante TX para elegir el manejo de desbordamiento TX (Clip / NaNGuard / Measure) para una fidelidad de tono bit-exacta en modos digitales.
- En la v26.7.4, la etiqueta del botón Enable ahora cambia dinámicamente a "Enabled" o "Disabled" para reflejar el estado actual, y se añadieron propiedades de accesibilidad a los controles Port y Enable.
- En la v26.8.4, el applet ahora admite hasta 8 canales RX, coincidiendo con el rango de canales DAX disponible en radios con más de 4 slices (como una FLEX-6700). Las filas RX por encima de la capacidad de slices de la radio se ocultan, replicando el comportamiento del applet DAX.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión activa a la radio.
- Esta función solo está presente en compilaciones creadas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón TCI de la bandeja no aparece, su compilación no incluye TCI.

## Cómo funciona

El applet TCI está oculto por defecto. Actívelo con el botón **TCI** de la bandeja en la barra lateral derecha.

Cuando hace clic en **Enable**, AetherSDR vincula un servidor WebSocket en el puerto configurado (predeterminado `50001`). Cualquier cliente compatible con TCI que se conecte a `ws://<su-host>:<puerto>` puede consultar y controlar la radio mediante el protocolo TCI. El applet muestra el estado actual del servidor y el número de clientes conectados en el área de estado junto al botón **Enable**.

El botón Enable muestra "Enabled" o "Disabled" para indicar claramente el estado actual del servidor. Si ha activado **Autostart TCI with AetherSDR** en Settings, el botón mostrará "Enabled" al iniciar.

El audio RX para los canales 1–8 sigue las mismas asignaciones de canal DAX que el applet DAX. La letra de slice que se muestra junto a cada fila RX y TX — por ejemplo, `Slice A` — refleja el slice asignado actualmente a ese canal DAX. Si no hay ningún slice asignado, el indicador muestra `—`. El número de filas RX visibles coincide con la capacidad de slices de la radio — en una radio con solo 4 slices, solo se muestran las filas RX1–RX4.

Los niveles de ganancia configurados en el applet se aplican al flujo de audio TCI y son independientes de los controles de ganancia de RF de la radio.

## Qué hace cada control

| Control                        | Qué hace                                                                                                                                                                         | Predeterminado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Ganancia+medidor RX1–RX8             | Medidor de nivel y control deslizante de ganancia combinados para cada canal RX de TCI. Arrastre para configurar la ganancia de salida del flujo de audio de ese canal. El control deslizante tiene un nombre accesible configurado como "TCI RX N gain". | 0.5                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Ganancia+medidor TX                  | Arrastrar configura la ganancia TX de TCI y emite tciTxGainChanged. El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure).                                                          | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de clientes de modos digitales: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo anula NaN/Inf), o Measure (bypass real con conteo de recortes). El predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Etiquetas de asignación de slice RX/TX  | Indicadores de solo lectura que muestran qué slice impulsa cada fila (`Slice A`, `Slice B`, etc., o `—` si no está asignado). Usa formato de texto enriquecido para que las letras de slice se rendericen correctamente (#2606).    | `—`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Port                           | Puerto WebSocket en el que escucha el servidor. Cambiar el valor mientras el servidor está en ejecución lo reinicia en el nuevo puerto. Los valores fuera del rango válido vuelven a `50001`.               | `50001`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Enable                         | Inicia o detiene el servidor TCI. La etiqueta del botón cambia a "Enabled" o "Disabled" para reflejar el estado actual. Si el puerto ya está en uso, el botón vuelve a "Disabled" y el estado muestra `(port in use)`.                          | Apagado. Si el inicio automático está activado, el botón muestra "Enabled" al iniciar.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Estado del servidor                  | Muestra `(stopped)`, `:<puerto> (<N> clientes)` o `(port in use)`. Se pone en rojo si falla la vinculación.                                                                                      | `(stopped)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite tciTxOverflowModeChanged.                                                 | Clip. Clip limita los excesos a ±1.0 con distorsión armónica; NaNGuard preserva tonos digitales bit-exactos anulando solo NaN/Inf; Measure cuenta los excesos para telemetría sin mutación. Se persiste como `TciTxOverflowMode` (0/1/2).                                                                                                                                                                                                                                                                                                                                           |

### Detalles del modo de desbordamiento TX

Haga clic derecho en el control **Ganancia+medidor TX** para abrir un menú contextual con tres opciones:

| Modo        | Comportamiento                                                                                                                                                                                                |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip (0)    | Limita los excesos a ±1.0. Predeterminado defensivo; introduce armónicos en los excesos pero protege la conversión posterior a int16.                                                                          |
| NaNGuard (1)| Pasa las muestras bit-exactas; solo anula valores patológicos NaN/Inf. Preserva la fidelidad de tono de los modos digitales; los flotantes fuera de rango llegan a la radio.                                                       |
| Measure (2) | Nunca muta las muestras. Cuenta los excesos para telemetría; la conversión posterior a int16 aún limita en la ruta DAX nativa de la radio.                                                                       |

La configuración se persiste como `TciTxOverflowMode` y su valor predeterminado es `0` (Clip) para que los usuarios existentes no vean cambios de comportamiento.

## Accesibilidad

Los controles del applet TCI incluyen nombres y descripciones accesibles:

| Control     | Nombre accesible        | Descripción accesible                            |
|-------------|------------------------|---------------------------------------------------|
| Port        | TCI port               | TCP port the TCI server listens on                |
| Enable      | TCI server enable      | Start or stop the TCI server                      |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que AetherSDR se lance, active `Settings > Autostart TCI with AetherSDR`. Esto configura la preferencia `AutoStartTCI`. Cuando está activado, el botón Enable mostrará "Enabled" al iniciar.
- El número de clientes mostrado en el estado del servidor se actualiza en vivo a medida que los clientes se conectan y desconectan. Consulte [See how many TCI clients are connected](../../getting-started/setup/see-how-many-tci-clients-are-connected.md) para más detalles.
- En radios con más de 4 slices — como una FLEX-6700 — las filas RX 5–8 están disponibles y se asignan a los canales DAX 5–8. El índice del receptor TCI (trx) no está limitado a 4; sigue la posición del slice y los canales de audio y ganancia de TciServer abarcan del 1 al 8.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se apaga a "Disabled"** — Otro proceso ya está vinculado a ese puerto. Cambie el puerto en el campo Port a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente. Consulte [Change the TCI port](change-the-tci-port.md).
- **El botón TCI de la bandeja no aparece** — Esta compilación de AetherSDR se creó sin soporte WebSocket. TCI no está disponible.
- **Las etiquetas de slice muestran `—` para todos los canales** — No hay ningún slice con un canal DAX asignado. Asigne un canal DAX a un slice mediante la configuración de la radio para rellenar las etiquetas RX y TX.
- **Solo aparecen 4 filas RX en una radio con más slices** — El applet oculta las filas RX por encima de la capacidad de slices de la radio para coincidir con el hardware disponible. Las filas no se destruyen, solo se ocultan; reaparecen si cambia la capacidad de slices de la radio.

## Relacionado

- [Enable the TCI server for Log4OM / SunSDR clients](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Change the TCI port](change-the-tci-port.md)
- [Adjust TCI RX gain per channel](adjust-tci-rx-gain-per-channel.md)
- [Adjust TCI TX gain](adjust-tci-tx-gain.md)
- [Autostart TCI on launch](autostart-tci-on-launch.md)
- [See how many TCI clients are connected](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
