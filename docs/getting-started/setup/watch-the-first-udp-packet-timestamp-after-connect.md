# Diagnóstico de red

Utilice el cuadro de diálogo **Network Diagnostics** para supervisar el enlace de red activo entre AetherSDR y la radio FLEX-8600. El cuadro de diálogo ofrece un diseño con varias pestañas que incluye un panel de visión general, paneles detallados de métricas, gráficos de rendimiento por flujo y un visor de registro en vivo.

## Antes de comenzar

- AetherSDR debe estar en ejecución. Puede abrir el cuadro de diálogo tanto si la radio está conectada como si no, pero los indicadores solo tienen significado después de un intento de conexión.
- Ya debe haber iniciado una conexión con una radio FLEX-8600.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el cuadro de diálogo **Network Diagnostics**, navegue por las pestañas para ver diferentes aspectos de la conexión.
3. Haga clic en **Close** para cerrar el cuadro de diálogo.

## Función de cada control

| Indicador / Control                            | Significado o comportamiento                                                                                                                                                                                                      | Notas                                                                                                  |
|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **First UDP Packet**                           | Muestra `Yes` o `No`. Se actualiza una vez por segundo. Indica si se ha recibido algún paquete UDP de la radio en la sesión actual.                                                                                               |                                                                                                        |
| **Status**                                     | Calidad general del enlace, codificada por colores de verde a rojo. Estados: Excellent, Very Good, Good, Fair, Poor.                                                                                                               |                                                                                                        |
| **Target Radio IP**                            | Dirección IP de la radio conectada, o "Not connected".                                                                                                                                                                            |                                                                                                        |
| **Selected Source**                            | NIC local o ruta de enlace utilizada para la conexión.                                                                                                                                                                            |                                                                                                        |
| **Local TCP**                                  | El extremo TCP local en uso para la conexión actual.                                                                                                                                                                              |                                                                                                        |
| **Local UDP**                                  | El extremo UDP local en el que AetherSDR está escuchando. Útil para confirmar que el puerto correcto está vinculado.                                                                                                               |                                                                                                        |
| **Latency (RTT)**                              | Tiempo de ida y vuelta actual.                                                                                                                                                                                                    |                                                                                                        |
| **Max Latency (RTT)**                          | El RTT más alto observado desde la conexión.                                                                                                                                                                                       |                                                                                                        |
| **Network Jitter**                             | Estimación suavizada de la fluctuación de la red para el flujo de audio, en ms.                                                                                                                                                   |                                                                                                        |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Velocidad de ingreso por categoría en kbps.                                                                                                                                                                                       |                                                                                                        |
| **Total RX / Total TX**                        | Bytes agregados por segundo en cada dirección.                                                                                                                                                                                    |                                                                                                        |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Recuentos y porcentaje de paquetes perdidos por categoría.                                                                                                                                                                        |                                                                                                        |
| **RX Buffer Now / Peak**                       | Llenado actual y máximo del búfer de audio en bytes y ms.                                                                                                                                                                         |                                                                                                        |
| **Underruns (total / last sec)**               | Contadores de subejecución de audio.                                                                                                                                                                                              |                                                                                                        |
| **Audio Arrival Gap / Max Arrival Gap**        | Temporización de llegada entre paquetes.                                                                                                                                                                                          |                                                                                                        |
| **Log path label**                             | Muestra la ruta completa del archivo de registro que se está siguiendo en la pestaña Logs.                                                                                                                                        |                                                                                                        |
| Overview (pestaña)                             | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de serie temporal (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                     |                                                                                                        |
| Details (pestaña)                              | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                                                                               |                                                                                                        |
| Latency (pestaña)                              | Gráfico de serie temporal de ancho completo del RTT, intervalo de llegada y fluctuación en ms.                                                                                                                                    |                                                                                                        |
| Rates (pestaña)                                | Gráfico de serie temporal en escala logarítmica de ancho completo de las velocidades de bits de entrada por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                         |                                                                                                        |
| Packet Loss (pestaña)                          | Gráfico de serie temporal de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                                         |                                                                                                        |
| Audio (pestaña)                                | Gráfico de serie temporal de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnóstico de audio RX por flujo que muestra la velocidad de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y el estado de cada flujo de audio activo. | v26.5.3 (#2889): los diagnósticos RX por flujo se exponen en el paquete de soporte y en la vista detallada de esta pestaña. |
| Logs (pestaña)                                 | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                                   | El selector Timeframe está oculto mientras esta pestaña esté activa.                                   |
| Timeframe                                      | Selecciona cuánto tiempo atrás muestran historial los gráficos de serie temporal. El valor predeterminado es 5 minutes. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week.                                          | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)                       | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                       |                                                                                                        |
| Select All (Logs)                              | Muestra todas las categorías de registro en el visor.                                                                                                                                                                             |                                                                                                        |
| Deselect All (Logs)                            | Oculta todas las categorías de registro del visor.                                                                                                                                                                                |                                                                                                        |
| Live / Paused (Logs)                           | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba lo pausa automáticamente; al hacer clic en Live se reanuda y salta al final.                                           |                                                                                                        |
| Close                                          | Cierra el cuadro de diálogo.                                                                                                                                                                                                      |                                                                                                        |

## Uso de la pestaña Logs

La pestaña **Logs** proporciona un seguimiento en vivo del archivo de registro de AetherSDR directamente dentro del cuadro de diálogo.

1. Haga clic en la pestaña **Logs**.
2. La ruta completa del archivo de registro que se está siguiendo se muestra en la parte superior de la pestaña, en el campo **Log path label**.
3. Use las casillas de verificación **Filter Categories** para mostrar solo las categorías que le interesan. La categoría **General** está disponible de forma predeterminada; las categorías adicionales reflejan todas las categorías registradas de LogManager.
4. Haga clic en **Select All** para habilitar todas las categorías a la vez, o en **Deselect All** para borrar todas las selecciones.
5. El visor comienza en modo **Live** y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba en cualquier momento para pausar el desplazamiento automático; el interruptor cambia a **Paused**.
6. Haga clic en **Live** para reanudar el desplazamiento automático y volver al final.

Las entradas de registro se resaltan sintácticamente por nivel de registro (DBG, INF, WRN, CRT/FTL) y por nombre de categoría, marcas de tiempo, valores numéricos y palabras clave de protocolo.

> **Nota:** El selector **Timeframe** está oculto mientras la pestaña Logs esté activa. Cambie a cualquier otra pestaña para restaurarlo.

## Consejos

- El cuadro de diálogo actualiza todos los indicadores una vez por segundo. Si **First UDP Packet** permanece en `No` durante varios segundos después de la conexión, el tráfico UDP no está llegando al host; verifique las reglas del cortafuegos, el enrutamiento y que el extremo UDP local mostrado en **Local UDP** sea accesible desde la radio.
- En una VPN o un enlace enrutado, TCP puede conectarse correctamente mientras que UDP está bloqueado por separado. Que **First UDP Packet** muestre `No` con **Status** mostrando un estado conectado es una señal confiable de esta división.
- **First UDP Packet** se restablece en cada nueva conexión. Desconéctese y reconéctese si desea volver a verificar la entrega después de cambiar la configuración de red.
- Use el selector **Timeframe** para reducir o ampliar el historial que se muestra en todas las pestañas de serie temporal. El valor predeterminado es 5 minutes.
- La pestaña **Rates** utiliza una escala logarítmica para que los flujos de baja velocidad de bits (como Meters) permanezcan visibles junto con el total RX de mayor velocidad de bits.
- El cuadro de diálogo utiliza una apariencia personalizada de tema oscuro con paneles, pestañas y controles estilizados para una retroalimentación visual coherente en todas las plataformas.
- La geometría del cuadro de diálogo (posición y tamaño) se recuerda entre sesiones a través de la configuración `NetworkDiagnosticsDialogGeometry`.

## Solución de problemas

- **First UDP Packet permanece en "No" después de conectar** — UDP no llega al extremo local. Verifique que ningún cortafuegos esté bloqueando UDP en el puerto mostrado en **Local UDP** y que la radio pueda enrutar de vuelta a la IP de su máquina. En una conexión VPN, confirme que la VPN pase UDP en ambas direcciones.
- **First UDP Packet muestra "Yes" pero el audio está en silencio** — UDP está llegando, pero un problema diferente afecta la reproducción. Verifique el grupo **Audio Playback** en la pestaña Details para detectar subejecuciones o problemas de búfer, y consulte la página de diagnóstico de audio.
- **El visor de registro está vacío o no muestra entradas** — Confirme que al menos una casilla de verificación de **Filter Categories** esté seleccionada. Si todas las categorías están deseleccionadas, no se muestra ninguna entrada. Haga clic en **Select All** para restaurar la visibilidad.

## Relacionado

- [Network Diagnostics overview](../../features/network-diagnostics/overview.md)
- [Verify the radio's IP and local bind address](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Measure RTT and packet drops during audio problems](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Pick the local network interface used for a manual connection](pick-the-local-network-interface-used-for-a-manual-connection.md)
