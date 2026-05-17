# Medir el RTT y la pérdida de paquetes durante problemas de audio

Utilice el diálogo Network Diagnostics para leer en vivo el tiempo de ida y vuelta (RTT) y los contadores de paquetes perdidos por categoría mientras ocurren problemas de audio. Esto le permite distinguir la pérdida de red de otras causas, como falta de datos en el búfer o fluctuación de fase (jitter).

## Antes de comenzar

- AetherSDR debe estar en ejecución. El diálogo no requiere una conexión activa con la radio, pero el RTT y los contadores de pérdida solo son significativos mientras está conectado.
- Reproduzca o espere a que ocurra el problema de audio antes de leer los contadores: los contadores de pérdida se acumulan desde la conexión y el RTT refleja el momento actual.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Lea `Latency (RTT)` para conocer el tiempo de ida y vuelta actual hacia la radio.
3. Lea `Max Latency (RTT)` para conocer el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador de pérdida `Audio`. El valor muestra los paquetes perdidos, el total de paquetes y el porcentaje de pérdida.
5. Revise las filas de pérdida `FFT`, `Waterfall`, `Meters` y `DAX` en la misma sección para ver si la pérdida está aislada en el audio o afecta a todos los flujos.
6. Haga clic en `Close` cuando haya terminado.

## Qué hace cada control

| Indicador                  | Significado                                                                                                                                                                         | Notas                                                                            |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| `Latency (RTT)`            | Tiempo de ida y vuelta actual hacia la radio. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                          |                                                                                  |
| `Max Latency (RTT)`        | RTT más alto visto desde la conexión. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                                  |                                                                                  |
| `Audio` (Packet Loss)      | Paquetes perdidos / paquetes totales (% de pérdida) para el flujo de audio, inferidos a partir de números de secuencia VITA faltantes.                                             |                                                                                  |
| `FFT` (Packet Loss)        | La misma métrica para el flujo FFT.                                                                                                                                                 |                                                                                  |
| `Waterfall` (Packet Loss)  | La misma métrica para el flujo waterfall.                                                                                                                                           |                                                                                  |
| `Meters` (Packet Loss)     | La misma métrica para el flujo de medidores.                                                                                                                                        |                                                                                  |
| `DAX` (Packet Loss)        | La misma métrica para el flujo DAX.                                                                                                                                                 |                                                                                  |
| `Status`                   | Calidad general del enlace, codificada por colores desde verde (Excelente) hasta rojo (Malo).                                                                                      |                                                                                  |
| Overview (pestaña)         | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de serie temporal (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer). |                                                                                  |
| Details (pestaña)          | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                               |                                                                                  |
| Latency (pestaña)          | Gráfico de serie temporal de ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                           |                                                                                  |
| Rates (pestaña)            | Gráfico de serie temporal de ancho completo en escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                |                                                                                  |
| Packet Loss (pestaña)      | Gráfico de serie temporal de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                           |                                                                                  |
| Audio (pestaña)            | Gráfico de serie temporal de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones por segundo.                                                               |                                                                                  |
| Logs (pestaña)             | Visualización en vivo del archivo de registro de AetherSDR, filtrada por casillas de verificación de categoría. Con resaltado de sintaxis por nivel de registro y nombre de categoría. | El selector Timeframe está oculto mientras esta pestaña está activa.            |
| Timeframe                  | Selecciona cuánto tiempo hacia atrás muestran los gráficos de serie temporal. El valor predeterminado es 5 minutos; las opciones son 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día y 1 semana. | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)   | Casillas de verificación por categoría para filtrar la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.       |                                                                                  |
| Select All (Logs)          | Muestra todas las categorías de registro en el visor.                                                                                                                               |                                                                                  |
| Deselect All (Logs)        | Oculta todas las categorías de registro del visor.                                                                                                                                  |                                                                                  |
| Live / Paused (Logs)       | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; haga clic en Live para reanudar y saltar al final. |                                                                                  |
| Close                      | Cierra el diálogo.                                                                                                                                                                  |                                                                                  |

Todos los contadores se actualizan una vez por segundo.

## Modo sin marco (Frameless)

El diálogo Network Diagnostics admite un modo de ventana sin marco que se controla mediante el ajuste `FramelessWindow` en `Settings > Preferences > Advanced > Use frameless windows`. Cuando está habilitado, el diálogo no tiene barra de título y se puede arrastrar por su área de barra de título personalizada. El comportamiento de redimensionamiento (cursor de ocho direcciones en bordes y esquinas) permanece activo en el modo sin marco. Cuando está deshabilitado, el diálogo utiliza la decoración de ventana estándar del sistema operativo con una barra de título normal.

El ajuste del modo sin marco se aplica inmediatamente al cambiarlo en Preferences; no es necesario volver a abrir el diálogo.

## Pestaña Logs

La pestaña Logs sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa al archivo que se está siguiendo se muestra encima del visor de registro.

Las líneas de registro tienen resaltado de sintaxis por nivel de registro y categoría:

- Las marcas de tiempo se muestran en gris azulado apagado.
- Las líneas `DBG` aparecen apagadas; las líneas `INF` se resaltan en azul claro; las líneas `WRN` en ámbar; las líneas `CRT` y `FTL` en rojo.
- Los nombres de categoría se muestran en negrita.
- Los valores numéricos (decimal, hexadecimal) se resaltan en verde; los tokens de protocolo (UDP, TCP, RX, TX, VITA-49 y similares) en púrpura claro.

Para filtrar la salida del registro:

1. Haga clic en la pestaña **Logs**.
2. Use las casillas de verificación **Filter Categories** para seleccionar las categorías que desea que aparezcan. Haga clic en **Select All** para mostrar todas las categorías o en **Deselect All** para limpiarlas.
3. Para pausar el desplazamiento, desplácese hacia arriba en el visor. El botón cambia a **Paused**. Haga clic en **Live** para reanudar el desplazamiento automático y saltar a la línea más reciente.

## Consejos

- Una pérdida cero en la sección Packet Loss no descarta el problema. La fluctuación de fase y la entrega tardía en ráfagas pueden causar cortes de audio sin generar saltos en los números de secuencia. Si las pérdidas son cero pero el audio sigue entrecortado, revise `Underruns (total)`, `Underruns (last sec)`, `Audio Arrival Gap`, `Max Arrival Gap` y `Jitter Estimate` en la sección **Audio Playback**.
- `Max Latency (RTT)` es más útil que el RTT actual para detectar picos transitorios que ya han pasado.
- La pérdida que aparece en todas las categorías de flujo simultáneamente apunta a un problema de ruta de red compartida, no a un problema específico del audio.
- Use el selector **Timeframe** para acercar o alejar los gráficos de serie temporal. Los marcos de tiempo más cortos (1 minuto) facilitan la visualización de picos recientes; los marcos más amplios (1 hora o más) ayudan a identificar patrones recurrentes.
- Use la pestaña **Logs** con filtros de categoría adecuados para correlacionar los eventos brutos del registro con las métricas mostradas en las otras pestañas.
- El ajuste del modo sin marco afecta a todos los diálogos de AetherSDR que admitan este modo. Si el diálogo Network Diagnostics no muestra una barra de título, verifique que `FramelessWindow` esté habilitado en Preferences.

## Solución de problemas

- **Todos los contadores de pérdida muestran 0 / 0** — No se han recibido paquetes VITA en esa categoría. Confirme que la radio esté conectada y transmitiendo los flujos correspondientes.
- **El RTT indica `< 1 ms` pero el audio está entrecortado** — La latencia de red no es la causa. Consulte la sección Audio Playback para obtener datos de subejecución y fluctuación de fase.
- **La pestaña Logs no muestra salida** — Verifique que al menos una casilla de verificación de categoría esté seleccionada. Haga clic en **Select All** para restaurar todas las categorías.
- **El diálogo no tiene barra de título y no se puede mover** — El modo sin marco está habilitado. Arrastre el diálogo haciendo clic en el área de la barra de título personalizada en la parte superior. Para deshabilitar el modo sin marco, vaya a `Settings > Preferences > Advanced` y desmarque `Use frameless windows`.

## Relacionados

- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Network Diagnostics overview](overview.md)
- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
- [Advanced preferences](../../preferences/advanced.md)
