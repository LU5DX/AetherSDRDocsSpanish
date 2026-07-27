# Resumen del servidor TCI

El applet del servidor TCI ejecuta un servidor WebSocket que habla el protocolo TCI de Expert Electronics, permitiendo que aplicaciones de registro, modos digitales y SDR de terceros — como Log4OM y herramientas SunSDR — lean y controlen la radio a través de una conexión de red local. Abra el applet para iniciar el servidor, configurar el puerto y ajustar la ganancia de audio para cada canal de RX y TX.

- El audio TX de TCI se recibe a través del WebSocket y se alimenta en una ranura de flujo `dax_tx` dedicada que es independiente de la ruta del dispositivo de audio DAX2 de Windows SmartSDR, por lo que el TX de TCI funciona en todas las plataformas, incluyendo Windows y Linux sin PipeWire (v0.9.5.1).
- Se corrigió un cierre con fallo en v0.9.7: TciServer ahora se destruye explícitamente en `~MainWindow()` después de que el hilo de audio se detiene pero mientras `RadioModel` sigue vivo, evitando un uso después de liberación mediante `releaseDaxForTci()`. Se agregó un `QPointer<RadioModel>` de seguridad adicional para que las comprobaciones de nulidad existentes capturen cualquier regresión futura automáticamente.
- Se añadieron tres comandos de TCI v2.0 (`volume`, `drive`, `rx_volume`) a la tabla de despacho con sincronización de estado bidireccional en v26.5.1.
- El reenvío del espectro del panadaptador, `tx_gain` y `ALC` se agregaron en v26.5.3.
- Haga clic derecho en el control deslizante de TX para elegir el manejo de desbordamiento de TX (Clip / NaNGuard / Measure) para una fidelidad de tono de modo digital bit exacto.
- En v26.7.4, la etiqueta del botón Habilitar ahora cambia dinámicamente a "Enabled" o "Disabled" para reflejar el estado actual, y se agregaron propiedades de accesibilidad a los controles de Puerto y Habilitar.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- Esta característica solo está presente en compilaciones realizadas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI no aparece, su compilación no incluye TCI.

## Cómo funciona

El applet TCI está oculto por defecto. Actívelo con el botón **TCI** de la bandeja en la barra lateral derecha.

Cuando hace clic en **Enable**, AetherSDR vincula un servidor WebSocket en el puerto configurado (por defecto `50001`). Cualquier cliente compatible con TCI que se conecte a `ws://<su-host>:<puerto>` puede entonces consultar y comandar la radio usando el protocolo TCI. El applet muestra el estado actual del servidor y el recuento de clientes conectados en el área de estado junto al botón **Enable**.

El botón Enable muestra "Enabled" o "Disabled" para indicar claramente el estado actual del servidor. Si ha habilitado **Autostart TCI with AetherSDR** en Configuración, el botón mostrará "Enabled" al iniciar.

El audio RX para los canales 1–4 sigue las mismas asignaciones de canal DAX que el applet DAX. La letra de slice que se muestra junto a cada fila de RX y TX — por ejemplo, `Slice A` — refleja el slice que está actualmente asignado a ese canal DAX. Si no hay ningún slice asignado, el indicador muestra `—`.

Los niveles de ganancia establecidos en el applet se aplican al flujo de audio TCI y son independientes de los controles de ganancia de RF de la radio.

## Qué hace cada control

| Control                        | Qué hace                                                                                                                                                                             | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medidor+ganancia RX1–RX4       | Medidor de nivel combinado y control deslizante de ganancia para cada canal RX de TCI. Arrastre para establecer la ganancia de salida del flujo de audio de ese canal. El control deslizante tiene un nombre accesible configurado como "TCI RX N gain". | 0.5                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Medidor+ganancia TX            | Arrastrar establece la ganancia TX de TCI y emite tciTxGainChanged. Haga clic derecho para abrir el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure).                | TciServer::setTxGain persiste TciTxGain internamente; la IU refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú contextual permite elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (pasante, solo pone a cero NaN/Inf), o Measure (bypass real con conteo de recortes). El valor predeterminado es Clip para que los usuarios actuales no vean cambios de comportamiento (#3065). |
| Etiquetas de asignación RX/TX  | Indicadores de solo lectura que muestran qué slice impulsa cada fila (`Slice A`, `Slice B`, etc., o `—` si no está asignado). Usa formato de texto enriquecido para que las letras de slice se rendericen correctamente (#2606).                   | `—`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Puerto                         | Puerto WebSocket en el que escucha el servidor. Cambiar el valor mientras el servidor está en ejecución lo reinicia en el nuevo puerto. Los valores fuera del rango válido vuelven a `50001`.                                                         | `50001`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Habilitar                      | Inicia o detiene el servidor TCI. La etiqueta del botón cambia a "Enabled" o "Disabled" para reflejar el estado actual. Si el puerto ya está en uso, el botón vuelve a "Disabled" y el estado muestra `(port in use)`.                                | Desactivado. Si el inicio automático está habilitado, el botón muestra "Enabled" al iniciar.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Estado del servidor            | Muestra `(stopped)`, `:<puerto> (<N> clients)`, o `(port in use)`. Se vuelve rojo en caso de fallo de vinculación.                                                                   | `(stopped)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite tciTxOverflowModeChanged. | Clip. Clip fija los picos a ±1.0 con distorsión armónica; NaNGuard preserva los tonos digitales bit exacto solo poniendo a cero NaN/Inf; Measure cuenta los picos para telemetría sin mutación. Se persiste como `TciTxOverflowMode` (0/1/2).                                                                                                                                                                                                                                                                                                                                   |

### Detalles del modo de desbordamiento TX

Haga clic derecho en el control **Medidor+ganancia TX** para abrir un menú contextual con tres opciones:

| Modo        | Comportamiento                                                                                                                                                                                           |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip (0)    | Fija los picos a ±1.0. Predeterminado defensivo; introduce armónicos en los picos pero protege la conversión posterior a int16.                                                                         |
| NaNGuard (1)| Pasa las muestras bit exacto; solo pone a cero los valores patológicos NaN/Inf. Preserva la fidelidad del tono de modo digital; los flotantes fuera de rango llegan a la radio.                          |
| Measure (2) | Nunca muta las muestras. Cuenta los picos para telemetría; la conversión posterior a int16 aún fija en la ruta DAX nativa de la radio.                                                                  |

La configuración se persiste como `TciTxOverflowMode` y su valor predeterminado es `0` (Clip) para que los usuarios actuales no vean cambios de comportamiento.

## Accesibilidad

Los controles del applet TCI incluyen nombres y descripciones accesibles:

| Control     | Nombre accesible      | Descripción accesible                               |
|-------------|-----------------------|-----------------------------------------------------|
| Puerto      | TCI port              | TCP port the TCI server listens on                  |
| Habilitar   | TCI server enable     | Start or stop the TCI server                        |

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que AetherSDR se inicia, active `Settings > Autostart TCI with AetherSDR`. Esto establece la preferencia `AutoStartTCI`. Cuando está activado, el botón Enable mostrará "Enabled" al iniciar.
- El recuento de clientes que se muestra en el estado del servidor se actualiza en vivo a medida que los clientes se conectan y desconectan. Consulte [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md) para más detalles.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se desactiva a "Disabled"** — Otro proceso ya está vinculado a ese puerto. Cambie el puerto en el campo Puerto a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **El botón de la bandeja TCI falta** — Esta compilación de AetherSDR se realizó sin soporte WebSocket. TCI no está disponible.
- **Las etiquetas de slice muestran `—` para todos los canales** — No hay slices con un canal DAX asignado. Asigne un canal DAX a un slice a través de la configuración de la radio para poblar las etiquetas de RX y TX.

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
