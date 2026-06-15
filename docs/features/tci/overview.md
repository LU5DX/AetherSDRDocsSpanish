# Descripción General del Servidor TCI

El applet del Servidor TCI ejecuta un servidor WebSocket que habla el protocolo TCI de Expert Electronics, permitiendo que aplicaciones de registro, modo digital y SDR de terceros — como Log4OM y herramientas SunSDR — lean y controlen la radio a través de una conexión de red local. Abra el applet para iniciar el servidor, configurar el puerto y ajustar la ganancia de audio para cada canal RX y TX.

- El audio TX de TCI se recibe a través del WebSocket y se alimenta en un slot dedicado del flujo `dax_tx` que es independiente de la ruta del dispositivo de audio SmartSDR DAX2 de Windows, por lo que el TX de TCI funciona en todas las plataformas, incluyendo Windows y Linux sin PipeWire (v0.9.5.1).
- Se corrigió un bloqueo al salir en v0.9.7: TciServer ahora se cierra explícitamente en `~MainWindow()` después de que el hilo de audio se detiene pero mientras `RadioModel` aún está activo, evitando un use-after-free a través de `releaseDaxForTci()`. Se agregó un `QPointer<RadioModel>` adicional como protección, de modo que las comprobaciones de nulo existentes capturen automáticamente cualquier regresión futura.
- Se agregaron tres comandos de TCI v2.0 (`volume`, `drive`, `rx_volume`) a la tabla de despacho con sincronización de estado bidireccional en v26.5.1.
- Se agregaron el reenvío del espectro del panadapter y `tx_gain`/`ALC` en v26.5.3.
- Haga clic derecho en el control deslizante de TX para elegir el manejo del desbordamiento de TX (Clip / NaNGuard / Measure) para la fidelidad de tonos de modo digital bit-exact.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- Esta función solo está presente en compilaciones realizadas con soporte WebSocket (`HAVE_WEBSOCKETS`). Si el botón de la bandeja TCI está ausente, su compilación no incluye TCI.

## Cómo funciona

El applet TCI está oculto por defecto. Actívelo con el botón de la bandeja **TCI** en la barra lateral derecha.

Cuando hace clic en **Enable**, AetherSDR vincula un servidor WebSocket en el puerto configurado (por defecto `50001`). Cualquier cliente compatible con TCI que se conecte a `ws://<su-host>:<puerto>` puede consultar y comandar la radio utilizando el protocolo TCI. El applet muestra el estado actual del servidor y el número de clientes conectados en el área de estado junto al botón **Enable**.

El audio RX para los canales 1 a 4 sigue las mismas asignaciones de canales DAX que el applet DAX. La letra del slice que se muestra junto a cada fila RX y TX — por ejemplo, `Slice A` — refleja el slice que está actualmente asignado a ese canal DAX. Si no hay ningún slice asignado, el indicador muestra `—`.

Los niveles de ganancia establecidos en el applet se aplican al flujo de audio de TCI y son independientes de los controles de ganancia de RF de la radio.

## Qué hace cada control

| Control                        | Qué hace                                                                                                                                                                      | Valor predeterminado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| RX1–RX4 medidor+ganancia       | Medidor de nivel y control deslizante de ganancia combinados para cada canal RX de TCI. Arrastre para establecer la ganancia de salida para el flujo de audio de ese canal. El control deslizante tiene un nombre accesible establecido como "TCI RX N gain". | 0.5                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| TX medidor+ganancia            | Medidor de nivel y control deslizante de ganancia combinados para la ganancia TX de TCI. Arrastre para establecer la ganancia de salida para el flujo de audio TX. El control deslizante tiene un nombre accesible establecido como "TCI TX gain". El clic derecho abre el selector de modo de desbordamiento TX (Clip / NaNGuard / Measure). | TciServer::setTxGain persiste TciTxGain internamente; la interfaz refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). El menú de clic derecho permite al usuario elegir cómo se manejan las muestras fuera de rango (>1.0) de los clientes de modo digital: Clip (saturación ±1.0, predeterminado heredado), NaNGuard (paso directo, solo anula NaN/Inf), o Measure (bypass verdadero con conteo de recortes). El valor predeterminado es Clip para que los usuarios existentes no vean cambios de comportamiento (#3065). |
| Etiquetas de asignación RX/TX  | Indicadores de solo lectura que muestran qué slice impulsa cada fila (`Slice A`, `Slice B`, etc., o `—` si no está asignado). Utiliza formato de texto enriquecido para que las letras de los slices se rendericen correctamente (#2606). | `—`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Puerto (Port)                  | Puerto WebSocket en el que escucha el servidor. Cambiar el valor mientras el servidor está en ejecución lo reinicia en el nuevo puerto. Los valores fuera del rango válido se restablecen a `50001`. | `50001`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Enable                         | Inicia o detiene el servidor TCI. Si el puerto ya está en uso, el botón vuelve a la posición de apagado y el estado muestra `(port in use)`. | Desactivado                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Estado del servidor            | Muestra `(stopped)`, `:<puerto> (<N> clients)` o `(port in use)`. Se vuelve rojo en caso de error de vinculación. | `(stopped)`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Modo de desbordamiento TX (clic derecho) | Haga clic derecho en el medidor/control deslizante de ganancia TX para abrir un menú contextual que selecciona el modo de manejo de desbordamiento TX. Emite tciTxOverflowModeChanged. | Clip. Clip sujeta los picos a ±1.0 con distorsión armónica; NaNGuard preserva los tonos digitales bit-exact anulando solo NaN/Inf; Measure cuenta los picos para telemetría sin modificación. Se persiste como `TciTxOverflowMode` (0/1/2).                                                                                                                                                                                                                                                                                                                                                    |

### Detalles del modo de desbordamiento TX

Haga clic derecho en el control **TX medidor+ganancia** para abrir un menú contextual con tres opciones:

| Modo        | Comportamiento                                                                                                                                                                                           |
|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Clip (0)    | Sujeta firmemente los picos a ±1.0. Predeterminado defensivo; introduce armónicos en los picos pero protege la conversión posterior a int16.                                                             |
| NaNGuard (1)| Pasa las muestras bit-exact; solo anula valores patológicos NaN/Inf. Preserva la fidelidad del tono de modo digital; los flotantes fuera de rango llegan a la radio.                                       |
| Measure (2) | Nunca modifica las muestras. Cuenta los picos para telemetría; la conversión posterior a int16 aún sujeta en la ruta DAX nativa de la radio.                                                               |

La configuración se persiste como `TciTxOverflowMode` y el valor predeterminado es `0` (Clip) para que los usuarios existentes no vean cambios de comportamiento.

## Consejos

- Para iniciar el servidor TCI automáticamente cada vez que se inicie AetherSDR, active `Settings > Autostart TCI with AetherSDR`. Esto establece la preferencia `AutoStartTCI`.
- El recuento de clientes que se muestra en el estado del servidor se actualiza en vivo a medida que los clientes se conectan y desconectan. Consulte [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md) para obtener más detalles.

## Solución de problemas

- **El estado muestra `(port in use)` y Enable se desactiva** — Otro proceso ya está vinculado a ese puerto. Cambie el puerto en el campo Puerto (Port) a un puerto libre en el rango 1024–65535 y haga clic en Enable nuevamente. Consulte [Cambiar el puerto TCI](change-the-tci-port.md).
- **Falta el botón de la bandeja TCI** — Esta compilación de AetherSDR se realizó sin soporte WebSocket. TCI no está disponible.
- **Las etiquetas de slice muestran `—` para todos los canales** — No hay slices con un canal DAX asignado. Asigne un canal DAX a un slice a través de la configuración de la radio para poblar las etiquetas RX y TX.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Ajustar la ganancia TX de TCI](adjust-tci-tx-gain.md)
- [Inicio automático de TCI al arrancar](autostart-tci-on-launch.md)
- [Ver cuántos clientes TCI están conectados](../../getting-started/setup/see-how-many-tci-clients-are-connected.md)
