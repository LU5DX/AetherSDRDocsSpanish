# Medir RTT y paquetes perdidos durante problemas de audio

Utilice el cuadro de diálogo Network Diagnostics para leer el tiempo de ida y vuelta en vivo y los recuentos de paquetes perdidos por categoría mientras ocurren problemas de audio. Esto le permite distinguir la pérdida de red de otras causas, como la falta de búfer o la fluctuación de fase.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. El cuadro de diálogo no requiere una conexión de radio activa, pero el RTT y los contadores de pérdidas solo tienen sentido mientras está conectado.
- Reproduzca o espere a que ocurra el problema de audio antes de leer los contadores; los recuentos de pérdidas se acumulan desde la conexión y el RTT refleja el momento actual.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Network Diagnostics.
2. Lea `Latency (RTT)` para conocer el tiempo de ida y vuelta actual hacia la radio.
3. Lea `Max Latency (RTT)` para conocer el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador de pérdidas `Audio`. El valor muestra paquetes perdidos, paquetes totales y un porcentaje de pérdida.
5. Verifique las filas de pérdidas `FFT`, `Waterfall`, `Meters` y `DAX` en la misma sección para ver si la pérdida está aislada al audio o afecta a todas las transmisiones.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador                 | Significado                                                                                                                                                                    | Notas                                                                             |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| `Latency (RTT)`           | Tiempo de ida y vuelta actual hacia la radio. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                     |                                                                                   |
| `Max Latency (RTT)`       | RTT más alto visto desde la conexión. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                             |                                                                                   |
| `Audio` (Packet Loss)     | Paquetes perdidos / paquetes totales (% de pérdida) para la transmisión de audio, inferido a partir de números de secuencia VITA faltantes.                                   |                                                                                   |
| `FFT` (Packet Loss)       | La misma métrica para la transmisión FFT.                                                                                                                                     |                                                                                   |
| `Waterfall` (Packet Loss) | La misma métrica para la transmisión waterfall.                                                                                                                               |                                                                                   |
| `Meters` (Packet Loss)    | La misma métrica para la transmisión de medidores.                                                                                                                            |                                                                                   |
| `DAX` (Packet Loss)       | La misma métrica para la transmisión DAX.                                                                                                                                     |                                                                                   |
| `Status`                  | Calidad general del enlace, codificada por colores desde verde (Excelente) hasta rojo (Pobre).                                                                                |                                                                                   |
| Overview (pestaña)        | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |                                                                                   |
| Details (pestaña)         | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                           |                                                                                   |
| Latency (pestaña)         | Gráfico de series temporales de ancho completo de RTT, intervalo de llegada y fluctuación en ms.                                                                              |                                                                                   |
| Rates (pestaña)           | Gráfico de series temporales de ancho completo en escala logarítmica de las tasas de bits entrantes por transmisión (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.   |                                                                                   |
| Packet Loss (pestaña)     | Gráfico de series temporales de ancho completo del % de pérdida de paquetes por categoría de transmisión.                                                                     |                                                                                   |
| Audio (pestaña)           | Gráfico de series temporales de ancho completo del llenado del búfer de reproducción (ms) y las subejecuciones/segundo.                                                       |                                                                                   |
| Logs (pestaña)            | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría. | El selector de periodo de tiempo está oculto mientras esta pestaña está activa.   |
| Timeframe                 | Selecciona cuánto tiempo atrás muestran el historial los gráficos de series temporales. El valor predeterminado es 5 minutos; las opciones son 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día y 1 semana. | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)  | Las casillas de verificación por categoría filtran la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.    |                                                                                   |
| Select All (Logs)         | Muestra todas las categorías de registro en el visor.                                                                                                                         |                                                                                   |
| Deselect All (Logs)       | Oculta todas las categorías de registro del visor.                                                                                                                            |                                                                                   |
| Live / Paused (Logs)      | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final. |                                                                                   |
| Close                     | Cierra el cuadro de diálogo.                                                                                                                                                  |                                                                                   |

Todos los contadores se actualizan una vez por segundo.

## Modo sin marco

El cuadro de diálogo Network Diagnostics admite un modo de ventana sin marco que se controla mediante el ajuste `FramelessWindow` en `Settings > Preferences > Advanced > Use frameless windows`. Cuando está habilitado, el cuadro de diálogo no tiene barra de título y se puede arrastrar por su área de barra de título personalizada. El comportamiento de redimensionamiento (cursor de ocho ejes en bordes y esquinas) permanece activo en modo sin marco. Cuando está deshabilitado, el cuadro de diálogo usa la decoración de ventana estándar del sistema operativo con una barra de título normal.

El ajuste del modo sin marco se aplica inmediatamente cuando se cambia en Preferences; no es necesario volver a abrir el cuadro de diálogo.

## Pestaña Logs

La pestaña Logs realiza un seguimiento del archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo que se está siguiendo se muestra sobre el visor de registros.

Las líneas de registro tienen resaltado de sintaxis por nivel de registro y categoría:

- Las marcas de tiempo se muestran en gris azulado apagado.
- Las líneas `DBG` están atenuadas; las líneas `INF` se resaltan en azul claro; las líneas `WRN` en ámbar; las líneas `CRT` y `FTL` en rojo.
- Los nombres de categoría se muestran en negrita.
- Los valores numéricos (decimal, hexadecimal) se resaltan en verde; los tokens de protocolo (UDP, TCP, RX, TX, VITA-49 y similares) en púrpura claro.

Para filtrar la salida del registro:

1. Haga clic en la pestaña **Logs**.
2. Utilice las casillas de verificación **Filter Categories** para seleccionar qué categorías aparecen. Haga clic en **Select All** para mostrar todas las categorías o en **Deselect All** para limpiarlas.
3. Para pausar el desplazamiento, desplácese hacia arriba en el visor. El botón cambia a **Paused**. Haga clic en **Live** para reanudar el desplazamiento automático y saltar a la línea más reciente.

## Consejos

- Una pérdida cero en la sección Packet Loss no descarta el problema. La fluctuación y la entrega tardía en ráfagas pueden causar cortes de audio sin provocar saltos en el número de secuencia. Si las pérdidas son cero pero el audio aún está dañado, verifique `Underruns (total)`, `Underruns (last sec)`, `Audio Arrival Gap`, `Max Arrival Gap` y `Jitter Estimate` en la sección **Audio Playback**.
- `Max Latency (RTT)` es más útil que el RTT actual para detectar picos transitorios que ya han pasado.
- La pérdida que aparece en todas las categorías de transmisión simultáneamente apunta a un problema de ruta de red compartida en lugar de un problema específico de audio.
- Utilice el selector **Timeframe** para acercar o alejar los gráficos de series temporales. Los periodos de tiempo más cortos (1 minuto) facilitan la visualización de picos recientes; los periodos más largos (1 hora o más) ayudan a identificar patrones recurrentes.
- Utilice la pestaña **Logs** con los filtros de categoría adecuados para correlacionar los eventos de registro sin procesar con las métricas que se muestran en las otras pestañas.
- El ajuste del modo sin marco afecta a todos los cuadros de diálogo de AetherSDR que admiten este modo. Si el cuadro de diálogo Network Diagnostics no muestra una barra de título, verifique que `FramelessWindow` esté habilitado en Preferences.

## Solución de problemas

- **Todos los contadores de pérdidas muestran 0 / 0** — No se han recibido paquetes VITA en esa categoría. Confirme que la radio está conectada y transmitiendo las transmisiones relevantes.
- **El RTT muestra `< 1 ms` pero el audio está dañado** — La latencia de la red no es la causa. Consulte la sección Audio Playback para obtener datos de subejecución y fluctuación.
- **La pestaña Logs no muestra salida** — Verifique que al menos una casilla de verificación de categoría esté seleccionada. Haga clic en **Select All** para restaurar todas las categorías.
- **El cuadro de diálogo no tiene barra de título y no se puede mover** — El modo sin marco está habilitado. Arrastre el cuadro de diálogo haciendo clic en el área de barra de título personalizada en la parte superior. Para deshabilitar el modo sin marco, vaya a `Settings > Preferences > Advanced` y desmarque `Use frameless windows`.

## Relacionado

- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Network Diagnostics overview](overview.md)
- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
- [Advanced preferences](../../preferences/advanced.md)
