# Medir RTT y pérdida de paquetes durante problemas de audio

Utilice el diálogo Network Diagnostics para leer el tiempo de ida y vuelta en vivo y los contadores de pérdida de paquetes por categoría mientras ocurren los problemas de audio. Esto le permite distinguir la pérdida de red de otras causas, como la falta de datos en el búfer o la fluctuación (jitter).

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión de radio activa, pero el RTT y los contadores de pérdida solo son significativos mientras está conectado.
- Reproduzca o espere a que ocurra el problema de audio antes de leer los contadores: los contadores de pérdida se acumulan desde la conexión y el RTT refleja el momento actual.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Lea `Latency (RTT)` para el tiempo de ida y vuelta actual hacia la radio.
3. Lea `Max Latency (RTT)` para el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador de pérdida `Audio`. El valor muestra paquetes perdidos, paquetes totales y un porcentaje de pérdida.
5. Verifique las filas de pérdida `FFT`, `Waterfall`, `Meters` y `DAX` en la misma sección para ver si la pérdida está aislada al audio o afecta a todos los flujos.
6. Haga clic en `Close` cuando haya terminado.

## Qué hace cada control

| Indicador                              | Significado                                                                                                                                                                                                                          | Notas                                                                                                                                          |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| `Latency (RTT)`                        | Tiempo de ida y vuelta actual hacia la radio. Muestra `< 1 ms` cuando es inferior a 1 ms, o `not measured on this link` cuando el transporte no tiene ida y vuelta que medir.                                                                            |                                                                                                                                                |
| `Max Latency (RTT)`                    | RTT más alto visto desde la conexión. Muestra `< 1 ms` cuando es inferior a 1 ms, o `not measured on this link` cuando el transporte no tiene ida y vuelta que medir.                                                                                  |                                                                                                                                                |
| `Audio` (Packet Loss)                  | Paquetes perdidos / paquetes totales (% de pérdida) para el flujo de audio, inferido de los números de secuencia VITA faltantes. Muestra `n/a` cuando el transporte no reporta estadísticas por categoría de flujo.                                     |                                                                                                                                                |
| `FFT` (Packet Loss)                    | Misma métrica para el flujo FFT. Muestra `n/a` cuando el transporte no reporta estadísticas por categoría de flujo.                                                                                                                 |                                                                                                                                                |
| `Waterfall` (Packet Loss)              | Misma métrica para el flujo del waterfall. Muestra `n/a` cuando el transporte no reporta estadísticas por categoría de flujo.                                                                                                           |                                                                                                                                                |
| `Meters` (Packet Loss)                 | Misma métrica para el flujo de medidores. Muestra `n/a` cuando el transporte no reporta estadísticas por categoría de flujo.                                                                                                              |                                                                                                                                                |
| `DAX` (Packet Loss)                    | Misma métrica para el flujo DAX. Muestra `n/a` cuando el transporte no reporta estadísticas por categoría de flujo.                                                                                                                 |                                                                                                                                                |
| `Status`                               | Calidad general del enlace, codificada por colores de verde (Excellent) a rojo (Poor).                                                                                                                                                          |                                                                                                                                                |
| Overview (tab)                         | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                                     |                                                                                                                                                |
| Connection Details (page)              | Cuadrícula desplazable con valores etiquetados para Network Status, Incoming Stream Rates, Packet Loss, Audio Playback y la subsección Adaptive Frame-Rate Throttle.                                                                     | Renombrado de 'Details' en la reorganización del árbol de navegación v26.8.4. Incluye una acción Read-Only Clipboard Copy para copiar todo el resumen de diagnóstico. |
| Adaptive Frame-Rate Throttle (section) | Muestra el Current State, Pending Lift y Sessions This Run del acelerador adaptativo. Reduce las tasas de cuadros del panadapter cuando se detecta latencia o pérdida.                                                                         | Nuevo en v26.8.4. Oculto hasta que haya datos del acelerador disponibles.                                                                                       |
| Latency (tab)                          | Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y jitter en ms. La traza RTT se omite cuando el transporte no tiene ida y vuelta que medir.                                                                                        |                                                                                                                                                |
| Rates (tab)                            | Gráfico de series temporales a ancho completo con escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                                                                   |                                                                                                                                                |
| Packet Loss (tab)                      | Gráfico de series temporales a ancho completo del % de pérdida de paquetes por categoría de flujo.                                                                                                                                                               |                                                                                                                                                |
| Audio (tab)                            | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos RX de audio por flujo que muestran la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. | v26.5.3 (#2889): diagnósticos RX por flujo expuestos en el paquete de soporte y en la vista de detalle de esta pestaña.                                        |
| Logs (tab)                             | Cola en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                                                                                         | El selector de marco temporal está oculto mientras esta página está activa.                                                                                        |
| TCI Clients (page)                     | Lista los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente.                                                                                     | Nuevo en v26.8.4. Compilación limitada por HAVE_TCI / soporte TCI. El selector de marco temporal está oculto en esta página.                                              |
| Timeframe                              | Selecciona cuánto historial muestran los gráficos de series temporales. El valor predeterminado es 5 minutos; las opciones son 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día y 1 semana.                                                                       | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa.                                                              |
| Filter Categories (Logs)               | Casillas de verificación por categoría para filtrar la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                                                                    |                                                                                                                                                |
| Select All (Logs)                      | Muestra todas las categorías de registro en el visor.                                                                                                                                                                                  |                                                                                                                                                |
| Deselect All (Logs)                    | Oculta todas las categorías de registro del visor.                                                                                                                                                                                        |                                                                                                                                                |
| Live / Paused (Logs)                   | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                                                                                                      |                                                                                                                                                |
| Close                                  | Cierra el diálogo.                                                                                                                                                                                                               |                                                                                                                                                |

Todos los contadores se actualizan una vez por segundo.

## Panel de navegación

El diálogo utiliza un panel de navegación de estilo árbol en el lado izquierdo en lugar de una barra de pestañas. El árbol contiene los siguientes elementos:

- **Overview** — Mismo contenido que la antigua pestaña Overview
- **Connection Details** — Mismo contenido que la antigua pestaña Details
- **Latency** — Mismo contenido que la antigua pestaña Latency
- **Rates** — Mismo contenido que la antigua pestaña Rates
- **Packet Loss** — Mismo contenido que la antigua pestaña Packet Loss
- **Audio** — Mismo contenido que la antigua pestaña Audio
- **Logs** — Mismo contenido que la antigua pestaña Logs
- **TCI Clients** — Lista los clientes TCI conectados con un monitor de tráfico en vivo (Pause/Save log/Clear), controles de supresión de comandos de respuesta y detalles por cliente. Compilación limitada por HAVE_TCI / soporte TCI.

El árbol de navegación admite navegación por teclado con las teclas de flecha. El elemento seleccionado está resaltado. El cuadro combinado Timeframe permanece en la esquina superior derecha del diálogo, oculto cuando la página Logs está activa.

## Barra de búsqueda

Hay un campo de búsqueda disponible sobre el panel de navegación. Escriba un nombre de página o una coincidencia parcial para filtrar el árbol de navegación. La búsqueda no distingue entre mayúsculas y minúsculas y se actualiza mientras escribe. Presione `Ctrl+F` o `Cmd+F` para enfocar el campo de búsqueda. Presione `Escape` para borrar la búsqueda.

## Rango fijo del eje Y

Los gráficos de series temporales en la pestaña Rates y otras pestañas ahora admiten un rango fijo del eje Y. Cuando no se establece un rango fijo, el gráfico se autoescala a los datos. Cuando se establece un rango fijo, el gráfico siempre muestra los valores mínimo y máximo especificados. Esta característica se controla programáticamente y no tiene un control visible para el usuario.

## Modo sin marco

El diálogo Network Diagnostics admite un modo de ventana sin marco que se controla mediante la configuración `FramelessWindow` en `Settings > Preferences > Advanced > Use frameless windows`. Cuando está habilitado, el diálogo no tiene barra de título y se puede arrastrar por su área de barra de título personalizada. El comportamiento de redimensionamiento (cursor de ocho ejes en bordes y esquinas) permanece activo en el modo sin marco. Cuando está deshabilitado, el diálogo utiliza la decoración de ventana estándar del sistema operativo con una barra de título normal.

La configuración del modo sin marco se aplica inmediatamente cuando se cambia en Preferences; no es necesario volver a abrir el diálogo.

## Pestaña Logs

La pestaña Logs sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo que se está siguiendo se muestra sobre el visor de registro.

Las líneas de registro se resaltan por nivel de registro y categoría:

- Las marcas de tiempo se muestran en gris azulado apagado.
- Las líneas `DBG` están atenuadas; las líneas `INF` se resaltan en azul claro; las líneas `WRN` en ámbar; las líneas `CRT` y `FTL` en rojo.
- Los nombres de categoría se muestran en negrita.
- Los valores numéricos (decimal, hexadecimal) se resaltan en verde; los tokens de protocolo (UDP, TCP, RX, TX, VITA-49 y similares) en púrpura claro.

Para filtrar la salida del registro:

1. Haga clic en el elemento **Logs** en el árbol de navegación.
2. Use las casillas de verificación **Filter Categories** para seleccionar qué categorías aparecen. Haga clic en **Select All** para mostrar todas las categorías o **Deselect All** para borrarlas.
3. Para pausar el desplazamiento, desplácese hacia arriba en el visor. El botón cambia a **Paused**. Haga clic en **Live** para reanudar el desplazamiento automático y saltar a la línea más reciente.

## Página TCI Clients

La página TCI Clients lista los clientes TCI conectados con un monitor de tráfico en vivo. Use los botones **Pause** / **Save log** / **Clear** para controlar el monitor de tráfico. La página también proporciona controles de supresión de comandos de respuesta y detalles por cliente. El selector Timeframe está oculto en esta página.

## Not measured on this link

Algunos transportes (por ejemplo, una conexión de flujo único) no proporcionan una ida y vuelta que medir ni estadísticas por categoría de flujo. En estos casos, el diálogo muestra `not measured on this link` para los valores de latencia y `n/a` para las cifras de tasa y pérdida por flujo, en lugar de mostrar un `0` o `< 1 ms` engañoso. Las filas totales RX/TX permanecen válidas en todos los transportes.

Cuando el transporte no tiene ida y vuelta que medir:

- La traza RTT en el gráfico Latency se omite en lugar de dibujarse como una línea plana de 0 ms.
- `Latency (RTT)` y `Max Latency (RTT)` muestran `not measured on this link`.
- La tarjeta de latencia Overview muestra `n/a`.

## Consejos

- Una pérdida cero en la sección Packet Loss no descarta el problema. La fluctuación y la entrega tardía en ráfagas pueden causar cortes de audio sin provocar huecos en los números de secuencia. Si las pérdidas son cero pero el audio sigue roto, verifique `Underruns (total)`, `Underruns (last sec)`, `Audio Arrival Gap`, `Max Arrival Gap` y `Jitter Estimate` en la sección **Audio Playback**.
- `Max Latency (RTT)` es más útil que el RTT actual para detectar picos transitorios que ya han pasado.
- La pérdida que aparece en todas las categorías de flujo simultáneamente apunta a un problema de ruta de red compartida en lugar de un problema específico del audio.
- Use el selector **Timeframe** para acercar o alejar los gráficos de series temporales. Los marcos temporales más estrechos (1 minuto) facilitan ver picos recientes; los más amplios (1 hora o más) ayudan a identificar patrones recurrentes.
- Use la pestaña **Logs** con filtros de categoría apropiados para correlacionar eventos de registro sin procesar con las métricas mostradas en las otras pestañas.
- La configuración del modo sin marco afecta a todos los diálogos sin marco de AetherSDR. Si el diálogo Network Diagnostics no muestra una barra de título, verifique que `FramelessWindow` esté habilitado en Preferences.
- Use el campo de búsqueda sobre el árbol de navegación para encontrar rápidamente una página de diagnóstico específica por nombre.
- Si los valores de latencia muestran `not measured on this link`, el transporte en uso no proporciona temporización de ida y vuelta. Consulte la sección Related para obtener información sobre la IP de la radio y la dirección de enlace local.

## Solución de problemas

- **Todos los contadores de pérdida muestran 0 / 0** — No se han recibido paquetes VITA en esa categoría. Confirme que la radio está conectada y transmitiendo los flujos relevantes.
- **Todos los contadores de pérdida muestran `n/a`** — El transporte en uso no reporta estadísticas por categoría de flujo. Solo las cifras totales RX/TX se aplican en este transporte.
- **El RTT muestra `< 1 ms` pero el audio está roto** — La latencia de red no es la causa. Consulte la sección Audio Playback para datos de subejecución y fluctuación.
- **El RTT muestra `not measured on this link`** — El transporte en uso no tiene ida y vuelta que medir. Este es un comportamiento esperado, no un error.
- **La pestaña Logs no muestra salida** — Verifique que al menos una casilla de categoría esté seleccionada. Haga clic en **Select All** para restaurar todas las categorías.
- **El diálogo no tiene barra de título y no se puede mover** — El modo sin marco está habilitado. Arrastre el diálogo haciendo clic en el área de barra de título personalizada en la parte superior. Para deshabilitar el modo sin marco, vaya a `Settings > Preferences > Advanced` y desmarque `Use frameless windows`.
- **El árbol de navegación no muestra elementos después de escribir en la búsqueda** — El filtro de búsqueda está activo. Borre el campo de búsqueda para mostrar todos los elementos de navegación.

## Relacionado

- [Diagnost
