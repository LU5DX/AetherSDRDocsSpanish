# Cambiar el Marco Temporal de los Gráficos de Historial (1 Minuto a 1 Semana)

El control **Timeframe** establece hasta dónde muestran el historial los gráficos de series temporales en el cuadro de diálogo Network Diagnostics. Úselo para alejar la vista y analizar tendencias a largo plazo o acercarla para examinar un breve periodo de pérdida de paquetes o latencia.

## Antes de comenzar

- Abra el cuadro de diálogo Network Diagnostics mediante `View > Network Diagnostics` o el botón de la barra de herramientas.
- Navegue a cualquier pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**. El control **Timeframe** está oculto cuando la pestaña **Logs** está activa.

## Pasos

1. Abra el cuadro de diálogo Network Diagnostics mediante `View > Network Diagnostics` o el botón de la barra de herramientas.
2. Seleccione una pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**.
3. Localice el cuadro combinado **Timeframe** en la esquina superior derecha de la barra de pestañas.
4. Haga clic en **Timeframe** y seleccione el valor deseado en la lista desplegable.

Los gráficos se actualizan inmediatamente para mostrar la ventana de historial seleccionada.

## Qué hace cada control

| Control      | Tipo        | Valor predeterminado |
|--------------|-------------|----------------------|
| **Timeframe**| Cuadro combinado | 5 minutes            |

Valores válidos: 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week.

## Consejos

- El selector **Timeframe** se aplica a todas las pestañas de gráfico simultáneamente. Al cambiar de pestaña después de modificar el valor, se mantiene la misma ventana.
- Seleccionar **1 week** en una sesión recién conectada mostrará un área de gráfico vacía hasta que se hayan recopilado suficientes datos. Los gráficos muestran "Collecting graph data" hasta que haya al menos un punto de datos disponible.
- Use **1 minute** o **5 minutes** para aislar una interrupción de audio o un pico de latencia específicos; use **1 hour** o más para evaluar la estabilidad general del enlace durante una sesión.

## Solución de problemas

- **El selector Timeframe no es visible** — La pestaña **Logs** está activa. Cambie a cualquier otra pestaña (**Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**) y el selector reaparecerá en la esquina superior derecha de la barra de pestañas.
- **Los gráficos muestran "Collecting graph data" después de cambiar a un marco temporal más largo** — Los datos históricos solo están disponibles desde el momento en que AetherSDR se conectó. No se almacenan datos entre sesiones.

## Relacionado

- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
