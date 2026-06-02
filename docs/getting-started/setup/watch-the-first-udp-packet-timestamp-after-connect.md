# Diagnóstico de Red

Use el cuadro de diálogo **Diagnóstico de Red** para monitorear el enlace de red activo entre AetherSDR y la radio FLEX-8600. El cuadro de diálogo ofrece un diseño con múltiples pestañas que incluye un panel general, paneles de métricas detalladas, gráficos de rendimiento por flujo y un visor de registros en vivo.

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo se puede abrir independientemente de si hay una radio conectada, pero los indicadores solo son significativos después de un intento de conexión.
- Debe haber iniciado una conexión a una radio FLEX-8600.

## Pasos

1. Haga clic en `Settings > Network...`.
2. En el cuadro de diálogo **Diagnóstico de Red**, navegue por las pestañas para ver diferentes aspectos de la conexión.
3. Haga clic en **Close** para cerrar el cuadro de diálogo.

## Descripción de cada control

| Indicador / Control                             | Significado o comportamiento                                                                                                                                                                                                 | Notas                                                                                              |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **First UDP Packet**                             | Muestra `Yes` o `No`. Se actualiza una vez por segundo. Indica si se ha recibido algún paquete UDP de la radio en la sesión actual.                                                                                            |                                                                                                    |
| **Status**                                       | Calidad general del enlace, codificada por colores de verde a rojo. Estados: Excellent, Very Good, Good, Fair, Poor.                                                                                                           |                                                                                                    |
| **Target Radio IP**                              | Dirección IP de la radio conectada, o "Not connected".                                                                                                                                                                        |                                                                                                    |
| **Selected Source**                              | NIC local o ruta de enlace utilizada para la conexión.                                                                                                                                                                        |                                                                                                    |
| **Local TCP**                                    | El extremo TCP local en uso para la conexión actual.                                                                                                                                                                          |                                                                                                    |
| **Local UDP**                                    | El extremo UDP local en el que AetherSDR está escuchando. Es útil para confirmar que el puerto correcto está enlazado.                                                                                                          |                                                                                                    |
| **Latency (RTT)**                                | Tiempo de ida y vuelta actual.                                                                                                                                                                                                |                                                                                                    |
| **Max Latency (RTT)**                            | Mayor RTT observado desde la conexión.                                                                                                                                                                                        |                                                                                                    |
| **Network Jitter**                               | Estimación suavizada de la fluctuación (jitter) de la red para el flujo de audio en ms.                                                                                                                                       |                                                                                                    |
| **Audio / FFT / Waterfall / Meters / DAX rates** | Tasa de ingreso por categoría en kbps.                                                                                                                                                                                        |                                                                                                    |
| **Total RX / Total TX**                          | Bytes agregados por segundo en cada dirección.                                                                                                                                                                                |                                                                                                    |
| **Audio / FFT / Waterfall / Meters / DAX drops** | Conteo y porcentaje de paquetes perdidos por categoría.                                                                                                                                                                       |                                                                                                    |
| **RX Buffer Now / Peak**                         | Llenado actual y máximo del búfer de audio en bytes y ms.                                                                                                                                                                    |                                                                                                    |
| **Underruns (total / last sec)**                 | Contadores de subejecución (underrun) de audio.                                                                                                                                                                               |                                                                                                    |
| **Audio Arrival Gap / Max Arrival Gap**          | Temporización de llegada entre paquetes.                                                                                                                                                                                       |                                                                                                    |
| **Log path label**                               | Muestra la ruta completa del archivo de registro que se está monitoreando en la pestaña Logs.                                                                                                                                 |                                                                                                    |
| Overview (pestaña)                               | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                             |                                                                                                    |
| Details (pestaña)                                | Cuadrícula desplazable con valores etiquetados para los grupos de Estado de Red, Tasas de Flujo Entrantes, Pérdida de Paquetes y Reproducción de Audio.                                                                        |                                                                                                    |
| Latency (pestaña)                                | Gráfico de series temporales a ancho completo de RTT, espacio de llegada y jitter en ms.                                                                                                                                       |                                                                                                    |
| Rates (pestaña)                                  | Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                          |                                                                                                    |
| Packet Loss (pestaña)                            | Gráfico de series temporales a ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                                    |                                                                                                    |
| Audio (pestaña)                                  | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos de audio RX por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo. | v26.5.3 (#2889): los diagnósticos de RX por flujo se exponen en el paquete de soporte y en la vista detallada de esta pestaña. |
| Logs (pestaña)                                   | Visualización en vivo del archivo de registro de AetherSDR, filtrado por categorías seleccionables. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                                          | El selector Timeframe está oculto mientras esta pestaña está activa.                               |
| Timeframe                                        | Selecciona cuánto tiempo hacia atrás muestran los gráficos de series temporales. El valor predeterminado es 5 minutos. Opciones: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week.                                       | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)                         | Casillas de verificación por categoría para filtrar la vista de registros. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                   |                                                                                                    |
| Select All (Logs)                                | Muestra todas las categorías de registro en el visor.                                                                                                                                                                         |                                                                                                    |
| Deselect All (Logs)                              | Oculta todas las categorías de registro del visor.                                                                                                                                                                            |                                                                                                    |
| Live / Paused (Logs)                             | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                                                 |                                                                                                    |
| Close                                            | Cierra el cuadro de diálogo.                                                                                                                                                                                                  |                                                                                                    |

## Uso de la pestaña Logs

La pestaña **Logs** proporciona una visualización en vivo del archivo de registro de AetherSDR directamente dentro del cuadro de diálogo.

1. Haga clic en la pestaña **Logs**.
2. La ruta completa del archivo de registro que se está monitoreando se muestra en la parte superior de la pestaña, en la etiqueta **Log path label**.
3. Use las casillas de verificación **Filter Categories** para mostrar solo las categorías que le interesen. La categoría **General** está disponible de forma predeterminada; las categorías adicionales reflejan todas las categorías registradas de LogManager.
4. Haga clic en **Select All** para habilitar todas las categorías a la vez, o en **Deselect All** para borrar todas las selecciones.
5. El visor se inicia en modo **Live** y se desplaza automáticamente a la salida más reciente. Desplácese hacia arriba en cualquier momento para pausar el desplazamiento automático; el conmutador cambia a **Paused**.
6. Haga clic en **Live** para reanudar el desplazamiento automático y volver al final.

Las entradas de registro tienen resaltado de sintaxis por nivel de registro (DBG, INF, WRN, CRT/FTL) y por nombre de categoría, marcas de tiempo, valores numéricos y palabras clave de protocolo.

> **Nota:** El selector **Timeframe** está oculto mientras la pestaña Logs esté activa. Cambie a cualquier otra pestaña para restaurarlo.

## Consejos

- El cuadro de diálogo actualiza todos los indicadores una vez por segundo. Si **First UDP Packet** permanece en `No` durante varios segundos después de la conexión, el tráfico UDP no está llegando al host: verifique las reglas del cortafuegos, el encaminamiento y que el extremo UDP local que se muestra en **Local UDP** sea accesible desde la radio.
- En una VPN o un enlace enrutado, la conexión TCP puede ser exitosa mientras que UDP está bloqueado por separado. Si **First UDP Packet** muestra `No` con **Status** mostrando un estado conectado, es una señal confiable de esta división.
- **First UDP Packet** se restablece en cada nueva conexión. Desconéctese y vuelva a conectarse si desea verificar nuevamente la entrega después de cambiar la configuración de red.
- Use el selector **Timeframe** para reducir o ampliar el historial que se muestra en todas las pestañas de series temporales. El valor predeterminado es 5 minutos.
- La pestaña **Rates** utiliza una escala logarítmica para que los flujos de baja tasa de bits (como Meters) permanezcan visibles junto con el total RX de mayor tasa de bits.
- El cuadro de diálogo utiliza una apariencia personalizada de tema oscuro con paneles, pestañas y controles estilizados para una retroalimentación visual consistente en todas las plataformas.
- La geometría del cuadro de diálogo (posición y tamaño) se recuerda entre sesiones mediante la configuración `NetworkDiagnosticsDialogGeometry`.

## Solución de problemas

- **First UDP Packet permanece en "No" después de conectar** — UDP no está llegando al extremo local. Verifique que ningún cortafuegos esté bloqueando UDP en el puerto que se muestra en **Local UDP** y que la radio pueda enrutar de vuelta a la dirección IP de su máquina. En una conexión VPN, confirme que la VPN pasa UDP en ambas direcciones.
- **First UDP Packet muestra "Yes" pero el audio está en silencio** — UDP está llegando, pero un problema diferente afecta la reproducción. Verifique el grupo **Audio Playback** en la pestaña Details para detectar subejecuciones o problemas de búfer, y consulte la página de diagnóstico de audio.
- **El visor de registros está vacío o no muestra entradas** — Confirme que al menos una casilla de verificación de **Filter Categories** esté seleccionada. Si todas las categorías están deseleccionadas, no se muestran entradas. Haga clic en **Select All** para restaurar la visibilidad.

## Relacionados

- [Network Diagnostics overview](../../features/network-diagnostics/overview.md)
- [Verify the radio's IP and local bind address](../../features/network-diagnostics/verify-the-radio-s-ip-and-local-bind-address.md)
- [Measure RTT and packet drops during audio problems](../../features/network-diagnostics/measure-rtt-and-packet-drops-during-audio-problems.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Connect by IP across a VPN or routed network](connect-by-ip-across-a-vpn-or-routed-network.md)
- [Pick the local network interface used for a manual connection](pick-the-local-network-interface-used-for-a-manual-connection.md)
