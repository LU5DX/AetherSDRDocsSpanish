# Medir RTT y pérdida de paquetes durante problemas de audio

Utilice el diálogo Network Diagnostics para leer el tiempo de ida y vuelta en vivo y los contadores de pérdida de paquetes por categoría mientras ocurren problemas de audio. Esto le permite distinguir la pérdida de red de otras causas, como falta de buffer o jitter.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. El diálogo no requiere una conexión activa al radio, pero RTT y los contadores de pérdida solo son significativos mientras está conectado.
- Reproduzca o espere a que ocurra el problema de audio antes de leer los contadores: los contadores de pérdida se acumulan desde la conexión y RTT refleja el momento actual.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Lea `Latency (RTT)` para el tiempo de ida y vuelta actual al radio.
3. Lea `Max Latency (RTT)` para el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador de pérdida `Audio`. El valor muestra paquetes perdidos, paquetes totales y un porcentaje de pérdida.
5. Revise las filas de pérdida `FFT`, `Waterfall`, `Meters` y `DAX` en la misma sección para ver si la pérdida está aislada al audio o afecta a todos los flujos.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador                 | Significado                                                                                                                                                                                                                          | Notas                                                                                                |
|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| `Latency (RTT)`           | Tiempo de ida y vuelta actual al radio. Muestra `< 1 ms` cuando está por debajo de 1 ms.                                                                                                                                            |                                                                                                      |
| `Max Latency (RTT)`       | RTT más alto visto desde la conexión. Muestra `< 1 ms` cuando está por debajo de 1 ms.                                                                                                                                              |                                                                                                      |
| `Audio` (Packet Loss)     | Paquetes perdidos / paquetes totales (% de pérdida) para el flujo de audio, inferido a partir de números de secuencia VITA faltantes.                                                                                                |                                                                                                      |
| `FFT` (Packet Loss)       | Misma métrica para el flujo FFT.                                                                                                                                                                                                     |                                                                                                      |
| `Waterfall` (Packet Loss) | Misma métrica para el flujo de waterfall.                                                                                                                                                                                            |                                                                                                      |
| `Meters` (Packet Loss)    | Misma métrica para el flujo de medidores.                                                                                                                                                                                            |                                                                                                      |
| `DAX` (Packet Loss)       | Misma métrica para el flujo DAX.                                                                                                                                                                                                     |                                                                                                      |
| `Status`                  | Calidad general del enlace, codificada por colores verde (Excelente) a rojo (Pobre).                                                                                                                                                 |                                                                                                      |
| Overview (tab)            | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series temporales (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                    |                                                                                                      |
| Details (tab)             | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                                                                                  |                                                                                                      |
| Latency (tab)             | Gráfico de series temporales de ancho completo de RTT, llegada de gap y jitter en ms.                                                                                                                                                |                                                                                                      |
| Rates (tab)               | Gráfico de series temporales de ancho completo en escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                                |                                                                                                      |
| Packet Loss (tab)         | Gráfico de series temporales de ancho completo del % de pérdida de paquetes por categoría de flujo.                                                                                                                                  |                                                                                                      |
| Audio (tab)               | Gráfico de series temporales de ancho completo del llenado del buffer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos de RX de audio por flujo mostrando la tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y estado del flujo para cada flujo de audio activo. | v26.5.3 (#2889): diagnósticos de RX por flujo expuestos en el paquete de soporte y en la vista de detalle de esta pestaña. |
| Logs (tab)                | Seguimiento en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                                      | El selector de marco temporal está oculto mientras esta pestaña está activa.                          |
| Timeframe                 | Selecciona cuánto tiempo atrás muestran el historial los gráficos de series temporales. El valor predeterminado es 5 minutos; las opciones son 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día y 1 semana.                            | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)  | Casillas de verificación por categoría filtran la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                              |                                                                                                      |
| Select All (Logs)         | Muestra todas las categorías de registro en el visor.                                                                                                                                                                                |                                                                                                      |
| Deselect All (Logs)       | Oculta todas las categorías de registro del visor.                                                                                                                                                                                   |                                                                                                      |
| Live / Paused (Logs)      | Cuando está en Live, el visor se desplaza automáticamente a la salida más reciente. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                                                     |                                                                                                      |
| Close                     | Cierra el diálogo.                                                                                                                                                                                                                   |                                                                                                      |

Todos los contadores se actualizan una vez por segundo.

## Modo sin marco

El diálogo Network Diagnostics admite un modo de ventana sin marco que se controla mediante la configuración `FramelessWindow` en `Settings > Preferences > Advanced > Use frameless windows`. Cuando está habilitado, el diálogo no tiene barra de título y se puede arrastrar por su área de barra de título personalizada. El comportamiento de redimensionamiento (cursor de ocho direcciones en bordes y esquinas) permanece activo en el modo sin marco. Cuando está deshabilitado, el diálogo usa la decoración de ventana estándar del sistema operativo con una barra de título normal.

La configuración del modo sin marco se aplica inmediatamente cuando se cambia en Preferences; no es necesario volver a abrir el diálogo.

## Pestaña Logs

La pestaña Logs sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa del archivo que se está siguiendo se muestra encima del visor de registro.

Las líneas de registro se resaltan con sintaxis por nivel de registro y categoría:

- Las marcas de tiempo se muestran en gris azulado apagado.
- Las líneas `DBG` están atenuadas; las líneas `INF` se resaltan en azul claro; las líneas `WRN` en ámbar; las líneas `CRT` y `FTL` en rojo.
- Los nombres de categoría se muestran en negrita.
- Los valores numéricos (decimal, hexadecimal) se resaltan en verde; los tokens de protocolo (UDP, TCP, RX, TX, VITA-49 y similares) en púrpura claro.

Para filtrar la salida del registro:

1. Haga clic en la pestaña **Logs**.
2. Use las casillas de verificación **Filter Categories** para seleccionar qué categorías aparecen. Haga clic en **Select All** para mostrar todas las categorías o en **Deselect All** para limpiarlas.
3. Para pausar el desplazamiento, desplácese hacia arriba en el visor. El botón cambia a **Paused**. Haga clic en **Live** para reanudar el desplazamiento automático y saltar a la línea más reciente.

## Consejos

- Una pérdida cero en la sección Packet Loss no descarta el problema. El jitter y la entrega tardía en ráfagas pueden causar interrupciones de audio sin generar saltos en los números de secuencia. Si las pérdidas son cero pero el audio sigue entrecortado, revise `Underruns (total)`, `Underruns (last sec)`, `Audio Arrival Gap`, `Max Arrival Gap` y `Jitter Estimate` en la sección **Audio Playback**.
- `Max Latency (RTT)` es más útil que el RTT actual para detectar picos transitorios que ya han pasado.
- La pérdida que aparece en todas las categorías de flujo simultáneamente apunta a un problema de ruta de red compartida en lugar de un problema específico de audio.
- Use el selector **Timeframe** para acercar o alejar los gráficos de series temporales. Los marcos temporales más estrechos (1 minuto) facilitan la visualización de picos recientes; los marcos más amplios (1 hora o más) ayudan a identificar patrones recurrentes.
- Use la pestaña **Logs** con filtros de categoría apropiados para correlacionar eventos de registro sin procesar con las métricas mostradas en las otras pestañas.
- La configuración del modo sin marco afecta a todos los diálogos compatibles con modo sin marco de AetherSDR. Si el diálogo Network Diagnostics no muestra una barra de título, verifique que `FramelessWindow` esté habilitado en Preferences.

## Solución de problemas

- **Todos los contadores de pérdida muestran 0 / 0** — No se han recibido paquetes VITA en esa categoría. Confirme que el radio está conectado y transmitiendo los flujos correspondientes.
- **RTT muestra `< 1 ms` pero el audio está entrecortado** — La latencia de red no es la causa. Consulte la sección Audio Playback para datos de subejecución y jitter.
- **La pestaña Logs no muestra salida** — Verifique que al menos una casilla de verificación de categoría esté seleccionada. Haga clic en **Select All** para restaurar todas las categorías.
- **El diálogo no tiene barra de título y no se puede mover** — El modo sin marco está habilitado. Arrastre el diálogo haciendo clic en el área de la barra de título personalizada en la parte superior. Para deshabilitar el modo sin marco, vaya a `Settings > Preferences > Advanced` y desmarque `Use frameless windows`.

## Relacionado

- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Network Diagnostics overview](overview.md)
- [Verify the radio's IP and local bind address](verify-the-radio-s-ip-and-local-bind-address.md)
- Advanced preferences
