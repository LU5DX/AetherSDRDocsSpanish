# Cambiar el período de los gráficos de historial (1 minuto a 1 semana)

El control **Timeframe** establece hasta dónde muestran historial los gráficos de series temporales en el diálogo de Diagnóstico de Red. Úselo para alejar la vista y analizar tendencias a largo plazo o acercarla para examinar una ráfaga breve de pérdida de paquetes o latencia.

## Antes de empezar

- Abra el diálogo de Diagnóstico de Red mediante `View > Network Diagnostics` o el botón de la barra de herramientas.
- Navegue a cualquier pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**. El control **Timeframe** está oculto cuando la pestaña **Logs** está activa.

## Pasos

1. Abra el diálogo de Diagnóstico de Red mediante `View > Network Diagnostics` o el botón de la barra de herramientas.
2. Seleccione una pestaña de gráfico — **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**.
3. Localice el cuadro combinado **Timeframe** en la esquina superior derecha de la barra de pestañas.
4. Haga clic en **Timeframe** y seleccione el valor deseado de la lista desplegable.

Los gráficos se actualizan inmediatamente para mostrar la ventana de historial seleccionada.

## Función de cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| **Timeframe** | Cuadro combinado | 5 minutes | 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week | Establece hasta dónde muestran historial todos los gráficos de series temporales. Oculto cuando la pestaña **Logs** está activa. |

## Consejos

- El selector **Timeframe** se aplica a todas las pestañas de gráfico simultáneamente. Cambiar de pestaña después de modificar el valor mantiene la misma ventana.
- Seleccionar **1 week** en una sesión recién conectada mostrará un área de gráfico vacía hasta que se haya recopilado suficiente información. Los gráficos muestran "Collecting graph data" hasta que haya al menos un punto de datos disponible.
- Use **1 minute** o **5 minutes** para aislar un corte de audio o un pico de latencia específico; use **1 hour** o más para evaluar la estabilidad general del enlace durante una sesión.

## Solución de problemas

- **El selector Timeframe no está visible** — La pestaña **Logs** está activa. Cambie a cualquier otra pestaña (**Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**) y el selector reaparecerá en la esquina superior derecha de la barra de pestañas.
- **Los gráficos muestran "Collecting graph data" después de cambiar a un período más largo** — Los datos históricos solo están disponibles desde el momento en que AetherSDR se conectó. No se almacenan datos entre sesiones.

## Relacionados

- [Resumen de Diagnóstico de Red](overview.md)
- [Medir RTT y caídas de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subejecuciones de audio y fluctuación de fase](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
