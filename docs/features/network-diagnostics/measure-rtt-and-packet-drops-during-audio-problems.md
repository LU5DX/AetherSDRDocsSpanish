# Medir RTT y pérdida de paquetes durante problemas de audio

Utilice el cuadro de diálogo Network Diagnostics (Diagnóstico de red) para consultar en tiempo real el tiempo de ida y vuelta y los recuentos de paquetes perdidos por categoría mientras se producen problemas de audio. Esto le permite distinguir la pérdida de red de otras causas, como la falta de datos en el búfer o la fluctuación de fase (jitter).

## Antes de comenzar

- AetherSDR debe estar en ejecución. El cuadro de diálogo no requiere una conexión activa a la radio, pero el RTT y los contadores de pérdida solo tienen sentido mientras esté conectado.
- Reproduzca o espere a que se produzca el problema de audio antes de leer los contadores; los recuentos de pérdida se acumulan desde la conexión y el RTT refleja el momento actual.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Network Diagnostics.
2. Lea `Latency (RTT)` para conocer el tiempo de ida y vuelta actual a la radio.
3. Lea `Max Latency (RTT)` para conocer el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador de pérdida de `Audio`. El valor muestra paquetes perdidos, paquetes totales y un porcentaje de pérdida.
5. Verifique las filas de pérdida de `FFT`, `Waterfall`, `Meters` y `DAX` en la misma sección para ver si la pérdida se limita al audio o afecta a todas las transmisiones.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador                 | Significado                                                                                                                                                                     | Notas                                                                            |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| `Latency (RTT)`           | Tiempo de ida y vuelta actual a la radio. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                          |                                                                                  |
| `Max Latency (RTT)`       | RTT más alto observado desde la conexión. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                          |                                                                                  |
| `Audio` (Pérdida de paq.) | Paquetes perdidos / paquetes totales (% de pérdida) para la transmisión de audio, inferido por números de secuencia VITA faltantes.                                             |                                                                                  |
| `FFT` (Pérdida de paq.)   | Misma métrica para la transmisión FFT.                                                                                                                                          |                                                                                  |
| `Waterfall` (Pérdida de paq.) | Misma métrica para la transmisión waterfall.                                                                                                                                 |                                                                                  |
| `Meters` (Pérdida de paq.) | Misma métrica para la transmisión de medidores.                                                                                                                                |                                                                                  |
| `DAX` (Pérdida de paq.)   | Misma métrica para la transmisión DAX.                                                                                                                                          |                                                                                  |
| `Status`                  | Calidad general del enlace, codificada por colores: verde (Excelente) a rojo (Malo).                                                                                        |                                                                                  |
| Overview (pestaña)        | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |                                                                                  |
| Details (pestaña)         | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                            |                                                                                  |
| Latency (pestaña)         | Gráfico de series temporales a ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                       |                                                                                  |
| Rates (pestaña)           | Gráfico de series temporales a ancho completo en escala logarítmica de las tasas de bits entrantes por transmisión (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.       |                                                                                  |
| Packet Loss (pestaña)     | Gráfico de series temporales a ancho completo del % de pérdida de paquetes por categoría de transmisión.                                                                       |                                                                                  |
| Audio (pestaña)           | Gráfico de series temporales a ancho completo del llenado del búfer de reproducción (ms) y subdesbordamientos/s.                                                               |                                                                                  |
| Logs (pestaña)            | Visualización en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Con resaltado de sintaxis por nivel de registro y nombre de categoría. | El selector de marco temporal está oculto mientras esta pestaña está activa.     |
| Timeframe                 | Selecciona cuánto tiempo atrás muestran los gráficos de series temporales. El valor predeterminado es 5 minutos; las opciones son 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día y 1 semana. | Se muestra en la esquina superior derecha de la barra de pestañas; se oculta cuando la pestaña Logs está activa. |
| Filter Categories (Logs)  | Casillas de verificación por categoría para filtrar la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.      |                                                                                  |
| Select All (Logs)         | Muestra todas las categorías de registro en el visor.                                                                                                                            |                                                                                  |
| Deselect All (Logs)       | Oculta todas las categorías de registro del visor.                                                                                                                               |                                                                                  |
| Live / Paused (Logs)      | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final. |                                                                                  |
| Close                     | Cierra el cuadro de diálogo.                                                                                                                                                    |                                                                                  |

Todos los contadores se actualizan una vez por segundo.

## Pestaña Logs

La pestaña Logs muestra el archivo de registro de AetherSDR en tiempo real. La ruta completa al archivo que se está siguiendo se muestra encima del visor de registros.

Las líneas de registro tienen resaltado de sintaxis por nivel de registro y categoría:

- Las marcas de tiempo se muestran en gris azulado apagado.
- Las líneas `DBG` están atenuadas; las líneas `INF` se resaltan en azul claro; las líneas `WRN` en ámbar; las líneas `CRT` y `FTL` en rojo.
- Los nombres de las categorías se muestran en negrita.
- Los valores numéricos (decimal, hexadecimal) se resaltan en verde; los tokens de protocolo (UDP, TCP, RX, TX, VITA-49 y similares) en púrpura claro.

Para filtrar la salida del registro:

1. Haga clic en la pestaña **Logs**.
2. Use las casillas de verificación **Filter Categories** para seleccionar qué categorías aparecen. Haga clic en **Select All** para mostrar todas las categorías o en **Deselect All** para borrarlas.
3. Para pausar el desplazamiento, desplácese hacia arriba en el visor. El botón cambia a **Paused**. Haga clic en **Live** para reanudar el desplazamiento automático y saltar a la línea más reciente.

## Consejos

- Una pérdida cero en la sección Packet Loss no descarta el problema. La fluctuación de fase (jitter) y la entrega tardía en ráfagas pueden causar cortes de audio sin generar espacios en los números de secuencia. Si las pérdidas son cero pero el audio sigue fallando, verifique `Underruns (total)`, `Underruns (last sec)`, `Audio Arrival Gap`, `Max Arrival Gap` y `Jitter Estimate` en la sección **Audio Playback**.
- `Max Latency (RTT)` es más útil que el RTT actual para detectar picos transitorios que ya han pasado.
- La pérdida que aparece en todas las categorías de transmisión simultáneamente apunta a un problema de ruta de red compartida, no a un problema específico de audio.
- Use el selector **Timeframe** para acercar o alejar los gráficos de series temporales. Los marcos temporales más estrechos (1 minuto) facilitan la visualización de picos recientes; los más amplios (1 hora o más) ayudan a identificar patrones recurrentes.
- Use la pestaña **Logs** con los filtros de categoría adecuados para correlacionar los eventos de registro sin procesar con las métricas que se muestran en las otras pestañas.

## Solución de problemas

- **Todos los contadores de pérdida muestran 0 / 0** — No se han recibido paquetes VITA en esa categoría. Confirme que la radio está conectada y transmitiendo las transmisiones relevantes.
- **El RTT indica `< 1 ms` pero el audio falla** — La latencia de red no es la causa. Consulte la sección Audio Playback para obtener datos de subdesbordamiento y jitter.
- **La pestaña Logs no muestra salida** — Verifique que al menos una casilla de verificación de categoría esté seleccionada. Haga clic en **Select All** para restaurar todas las categorías.

## Relacionados

- [Diagnóstico de subdesbordamientos y jitter de audio](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificación de tasas de datos por categoría (audio, FFT, waterfall, medidores, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Resumen de Network Diagnostics](overview.md)
- [Verificación de la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
