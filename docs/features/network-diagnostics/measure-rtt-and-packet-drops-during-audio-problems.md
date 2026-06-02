# Medir RTT y pérdida de paquetes durante problemas de audio

Use el diálogo de Diagnóstico de Red para leer el tiempo de ida y vuelta en vivo y los contadores de pérdida de paquetes por categoría mientras ocurren los problemas de audio. Esto le permite distinguir la pérdida de red de otras causas como falta de memoria en el búfer o jitter.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. El diálogo no requiere una conexión de radio activa, pero RTT y los contadores de pérdida solo son significativos mientras está conectado.
- Reproduzca o espere a que ocurra el problema de audio antes de leer los contadores — los contadores de pérdida se acumulan desde la conexión y RTT refleja el momento actual.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo de Diagnóstico de Red.
2. Lea `Latency (RTT)` para ver el tiempo de ida y vuelta actual a la radio.
3. Lea `Max Latency (RTT)` para ver el RTT más alto registrado desde que se estableció la conexión.
4. En la sección **Packet Loss (Sequence Gaps)**, lea el contador de pérdida `Audio`. El valor muestra paquetes perdidos, paquetes totales y un porcentaje de pérdida.
5. Verifique las filas de pérdida `FFT`, `Waterfall`, `Meters` y `DAX` en la misma sección para ver si la pérdida está aislada al audio o afecta a todos los flujos.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Indicador                 | Significado                                                                                                                                                                                                                         | Notas                                                                                                  |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| `Latency (RTT)`           | Tiempo de ida y vuelta actual a la radio. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                                                                               |                                                                                                        |
| `Max Latency (RTT)`       | RTT más alto visto desde la conexión. Muestra `< 1 ms` cuando es inferior a 1 ms.                                                                                                                                                   |                                                                                                        |
| `Audio` (Pérdida de paq.) | Paquetes perdidos / paquetes totales (% de pérdida) para el flujo de audio, inferido a partir de números de secuencia VITA faltantes.                                                                                                |                                                                                                        |
| `FFT` (Pérdida de paq.)   | La misma métrica para el flujo FFT.                                                                                                                                                                                                 |                                                                                                        |
| `Waterfall` (Pérdida de paq.) | La misma métrica para el flujo waterfall.                                                                                                                                                                                       |                                                                                                        |
| `Meters` (Pérdida de paq.) | La misma métrica para el flujo de medidores.                                                                                                                                                                                       |                                                                                                        |
| `DAX` (Pérdida de paq.)   | La misma métrica para el flujo DAX.                                                                                                                                                                                                |                                                                                                        |
| `Status`                  | Calidad general del enlace, codificada por colores desde verde (Excelente) hasta rojo (Pobre).                                                                                                                                      |                                                                                                        |
| Overview (pestaña)        | Muestra cuatro tarjetas de estado (Status, Latency, Packet Loss, Audio Buffer) y cuatro gráficos de series de tiempo (Latency and Jitter, Recent Packet Loss, Total Stream Rates, Audio Buffer).                                    |                                                                                                        |
| Details (pestaña)         | Cuadrícula desplazable con valores etiquetados para los grupos Network Status, Incoming Stream Rates, Packet Loss y Audio Playback.                                                                                                 |                                                                                                        |
| Latency (pestaña)         | Gráfico de series de tiempo de ancho completo de RTT, intervalo de llegada y jitter en ms.                                                                                                                                          |                                                                                                        |
| Rates (pestaña)           | Gráfico de series de tiempo de ancho completo en escala logarítmica de las tasas de bits entrantes por flujo (RX total, Audio, FFT, Waterfall, Meters, DAX) en kbps.                                                                |                                                                                                        |
| Packet Loss (pestaña)     | Gráfico de series de tiempo de ancho completo del porcentaje de pérdida de paquetes por categoría de flujo.                                                                                                                         |                                                                                                        |
| Audio (pestaña)           | Gráfico de series de tiempo de ancho completo del llenado del búfer de reproducción (ms) y subejecuciones/s. Incluye diagnósticos RX de audio por flujo que muestran tasa de alimentación, déficit, paquetes tardíos, código de clase de paquete y salud del flujo para cada flujo de audio activo. | v26.5.3 (#2889): diagnósticos RX por flujo expuestos en el paquete de soporte y en la vista detallada de esta pestaña. |
| Logs (pestaña)            | Visualización en vivo del archivo de registro de AetherSDR, filtrado por casillas de verificación de categoría. Resaltado de sintaxis por nivel de registro y nombre de categoría.                                                   | El selector de intervalo de tiempo está oculto mientras esta pestaña está activa.                       |
| Timeframe                 | Selecciona cuánto tiempo atrás muestran los gráficos de series de tiempo. El valor predeterminado es 5 minutos; las opciones son 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día y 1 semana.                                         | Se muestra en la esquina superior derecha de la barra de pestañas; oculto cuando la pestaña Logs está activa. |
| Filter Categories (Logs)  | Casillas de verificación por categoría para filtrar la vista de registro. Incluye una categoría General (predeterminada) más todas las categorías registradas de LogManager.                                                        |                                                                                                        |
| Select All (Logs)         | Muestra todas las categorías de registro en el visor.                                                                                                                                                                              |                                                                                                        |
| Deselect All (Logs)       | Oculta todas las categorías de registro del visor.                                                                                                                                                                                 |                                                                                                        |
| Live / Paused (Logs)      | Cuando está en Live, el visor se desplaza automáticamente a la salida más nueva. Desplazarse hacia arriba pausa automáticamente; hacer clic en Live reanuda y salta al final.                                                       |                                                                                                        |
| Close                     | Cierra el diálogo.                                                                                                                                                                                                                 |                                                                                                        |

Todos los contadores se actualizan una vez por segundo.

## Modo sin marco

El diálogo de Diagnóstico de Red admite un modo de ventana sin marco que está controlado por la configuración `FramelessWindow` en `Settings > Preferences > Advanced > Use frameless windows`. Cuando está habilitado, el diálogo no tiene barra de título y se puede arrastrar por su área de barra de título personalizada. El comportamiento de redimensionamiento (cursor de ocho ejes en bordes y esquinas) permanece activo en el modo sin marco. Cuando está deshabilitado, el diálogo usa la decoración de ventana estándar del sistema operativo con una barra de título normal.

La configuración del modo sin marco se aplica inmediatamente cuando se cambia en Preferences; no es necesario volver a abrir el diálogo.

## Pestaña Logs

La pestaña Logs sigue el archivo de registro de AetherSDR en tiempo real. La ruta completa al archivo que se está siguiendo se muestra sobre el visor de registro.

Las líneas de registro tienen resaltado de sintaxis por nivel de registro y categoría:

- Las marcas de tiempo se muestran en azul grisáceo apagado.
- Las líneas `DBG` están atenuadas; las líneas `INF` se resaltan en azul claro; las líneas `WRN` en ámbar; las líneas `CRT` y `FTL` en rojo.
- Los nombres de categoría se muestran en negrita.
- Los valores numéricos (decimal, hexadecimal) se resaltan en verde; los tokens de protocolo (UDP, TCP, RX, TX, VITA-49 y similares) en púrpura claro.

Para filtrar la salida del registro:

1. Haga clic en la pestaña **Logs**.
2. Use las casillas de verificación **Filter Categories** para seleccionar qué categorías aparecen. Haga clic en **Select All** para mostrar todas las categorías o **Deselect All** para desmarcarlas.
3. Para pausar el desplazamiento, desplace hacia arriba en el visor. El botón cambia a **Paused**. Haga clic en **Live** para reanudar el desplazamiento automático y saltar a la línea más nueva.

## Consejos

- La pérdida cero en la sección Packet Loss no descarta el problema. El jitter y la entrega tardía en ráfagas pueden causar cortes de audio sin generar espacios en los números de secuencia. Si las pérdidas son cero pero el audio aún está defectuoso, verifique `Underruns (total)`, `Underruns (last sec)`, `Audio Arrival Gap`, `Max Arrival Gap` y `Jitter Estimate` en la sección **Audio Playback**.
- `Max Latency (RTT)` es más útil que el RTT actual para detectar picos transitorios que ya han pasado.
- La pérdida que aparece en todas las categorías de flujo simultáneamente apunta a un problema de ruta de red compartida en lugar de un problema específico de audio.
- Use el selector **Timeframe** para acercar o alejar los gráficos de series de tiempo. Intervalos de tiempo más cortos (1 minuto) facilitan ver picos recientes; intervalos más largos (1 hora o más) ayudan a identificar patrones recurrentes.
- Use la pestaña **Logs** con filtros de categoría apropiados para correlacionar eventos de registro sin procesar con las métricas mostradas en las otras pestañas.
- La configuración del modo sin marco afecta a todos los diálogos de AetherSDR compatibles con marcos. Si el diálogo de Diagnóstico de Red no muestra una barra de título, verifique que `FramelessWindow` esté habilitado en Preferences.

## Solución de problemas

- **Todos los contadores de pérdida muestran 0 / 0** — No se han recibido paquetes VITA en esa categoría. Confirme que la radio está conectada y transmitiendo los flujos relevantes.
- **RTT muestra `< 1 ms` pero el audio está defectuoso** — La latencia de red no es la causa. Consulte la sección Audio Playback para ver datos de subejecución y jitter.
- **La pestaña Logs no muestra salida** — Verifique que al menos una casilla de verificación de categoría esté seleccionada. Haga clic en **Select All** para restaurar todas las categorías.
- **El diálogo no tiene barra de título y no se puede mover** — El modo sin marco está habilitado. Arrastre el diálogo haciendo clic en el área de barra de título personalizada en la parte superior. Para deshabilitar el modo sin marco, vaya a `Settings > Preferences > Advanced` y desmarque `Use frameless windows`.

## Relacionados

- [Diagnosticar subejecuciones y jitter de audio](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Resumen de Diagnóstico de Red](overview.md)
- [Verificar la IP de la radio y la dirección de enlace local](verify-the-radio-s-ip-and-local-bind-address.md)
- Preferencias avanzadas
