# Cambiar el Marco Temporal de los Gráficos Históricos (1 Minuto a 1 Semana)

El control **Timeframe** establece cuánto tiempo hacia atrás muestran historial los gráficos de series temporales en el diálogo Network Diagnostics. Úselo para alejar la vista y analizar tendencias a largo plazo o para acercarla y examinar una ráfaga corta de pérdida de paquetes o latencia.

## Antes de comenzar

- Abra el diálogo Network Diagnostics mediante `View > Network Diagnostics` o el botón de la barra de herramientas.
- Navegue a cualquier pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**. El control **Timeframe** está oculto cuando la pestaña **Logs** está activa. También está oculto en la página **TCI Clients**.

## Pasos

1. Abra el diálogo Network Diagnostics mediante `View > Network Diagnostics` o el botón de la barra de herramientas.
2. Seleccione una pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**.
3. Localice el cuadro combinado **Timeframe** en la esquina superior derecha de la barra de pestañas.
4. Haga clic en **Timeframe** y seleccione el valor deseado de la lista desplegable.

Los gráficos se actualizan inmediatamente para mostrar la ventana de historial seleccionada.

## Qué hace cada control

| Control                                | Tipo                                                                                                                                                        | Valor predeterminado                                                                                                                           |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **Overview** (pestaña)                     | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). | Ninguno                                                                                                                                           |
| **Connection Details** (página)          | Cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la subsección Adaptive Frame-Rate Throttle. | Renombrado desde 'Details' en la reorganización de navegación de árbol de la v26.8.4. Incluye una acción Read-Only Clipboard Copy para copiar todo el resumen de diagnóstico. |
| **Adaptive Frame-Rate Throttle** (sección) | Muestra el Current State, Pending Lift y Sessions This Run del acelerador adaptativo. Reduce las velocidades de cuadro del panadapter cuando se detecta latencia o pérdida. | Nuevo en la v26.8.4. Oculto hasta que los datos del acelerador estén disponibles.                                                                                       |
| **Latency** (pestaña)                      | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                          | Ninguno                                                                                                                                           |
| **Rates** (pestaña)                        | Gráfico de series temporales de ancho completo con escala logarítmica de velocidades de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                              | Ninguno                                                                                                                                           |
| **Packet Loss** (pestaña)                  | Gráfico de series temporales de ancho completo de pérdida de paquetes % por categoría de flujo.                                                                                          | Ninguno                                                                                                                                           |
| **Audio** (pestaña)                        | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos de audio RX por flujo que muestran la velocidad de alimentación, el déficit, los paquetes tardíos, el código de clase de paquete y el estado del flujo para cada flujo de audio activo. | v26.5.3 (#2889): diagnósticos RX por flujo expuestos en el paquete de soporte y en la vista de detalle de esta pestaña.                                        |
| **Logs** (pestaña)                         | Cola en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                     | El selector de Timeframe está oculto mientras esta página está activa.                                                                                        |
| **TCI Clients** (página)                 | Enumera los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente.                 | Nuevo en la v26.8.4. Controlado por compilación con soporte HAVE_TCI / TCI. El selector de Timeframe está oculto en esta página.                                              |
| **Timeframe**                          | Cuadro combinado                                                                                                                                                    | 5 minutos                                                                                                                                      |
| **Filter Categories** (Logs)           | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría 'General' (predeterminada) más todas las categorías registradas de LogManager.                              | Ninguno                                                                                                                                           |
| **Select All** (Logs)                  | Botón pulsador que muestra todas las categorías de registro en el visor.                                                                                                    | Ninguno                                                                                                                                           |
| **Deselect All** (Logs)                | Botón pulsador que oculta todas las categorías de registro del visor.                                                                                                  | Ninguno                                                                                                                                           |
| **Live / Paused** (Logs)               | Botón de alternancia: cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                   | Live                                                                                                                                           |
| **Close**                              | Botón pulsador que cierra el diálogo.                                                                                                                         | Ninguno                                                                                                                                           |

Valores válidos para **Timeframe**: 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día, 1 semana.

## Consejos

- El selector **Timeframe** se aplica a todas las pestañas de gráfico simultáneamente. Cambiar de pestaña después de modificar el valor mantiene la misma ventana.
- Seleccionar **1 week** en una sesión recién conectada mostrará un área de gráfico vacía hasta que se haya recopilado suficiente información. Los gráficos muestran "Collecting graph data" hasta que haya al menos un punto de datos disponible.
- Use **1 minute** o **5 minutes** para aislar una caída de audio o un pico de latencia específico; use **1 hour** o más para evaluar la estabilidad general del enlace durante una sesión.

## Solución de problemas

- **El selector de Timeframe no es visible** — La pestaña **Logs** o la página **TCI Clients** están activas. Cambie a cualquier otra pestaña (**Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**) y el selector reaparecerá en la esquina superior derecha de la barra de pestañas.
- **Los gráficos muestran "Collecting graph data" después de cambiar a un marco temporal más largo** — Los datos históricos solo están disponibles desde el momento en que AetherSDR se conectó. No se almacenan datos entre sesiones.

## Relacionado

- [Resumen de Network Diagnostics](overview.md)
- [Medir RTT y caídas de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar velocidades de datos por categoría (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subejecuciones de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
