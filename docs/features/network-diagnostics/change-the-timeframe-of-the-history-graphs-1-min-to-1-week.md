# Cambiar el intervalo temporal de los gráficos de historial (de 1 minuto a 1 semana)

El control **Timeframe** define cuánto tiempo hacia atrás muestran historial los gráficos de series temporales en el cuadro de diálogo Network Diagnostics. Úselo para alejar la vista y analizar tendencias a largo plazo o para acercarla y examinar una ráfaga breve de pérdida de paquetes o latencia.

## Antes de empezar

- Abra el cuadro de diálogo Network Diagnostics mediante `Settings > Network...`.
- Navegue a cualquier pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**. El control **Timeframe** está oculto cuando la pestaña **Logs** está activa.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Network Diagnostics.
2. Seleccione una pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**.
3. Localice el cuadro combinado **Timeframe** en la esquina superior derecha de la barra de pestañas.
4. Haga clic en **Timeframe** y seleccione el valor deseado de la lista desplegable.

Los gráficos se actualizan inmediatamente para mostrar la ventana de historial seleccionada.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| **Timeframe** | Cuadro combinado | 5 minutos | 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día, 1 semana | Define cuánto tiempo hacia atrás muestran historial todos los gráficos de series temporales. Se oculta cuando la pestaña **Logs** está activa. |

## Consejos

- El selector **Timeframe** se aplica a todas las pestañas de gráfico simultáneamente. Al cambiar de pestaña después de modificar el valor, se mantiene la misma ventana temporal.
- Al seleccionar **1 week** en una sesión recién conectada, el área del gráfico aparecerá vacía hasta que se hayan recopilado suficientes datos. Los gráficos muestran "Collecting graph data" hasta que haya al menos un punto de datos disponible.
- Use **1 minute** o **5 minutes** para aislar una pérdida de audio o un pico de latencia específicos; use **1 hour** o más para evaluar la estabilidad general del enlace durante una sesión.

## Solución de problemas

- **El selector Timeframe no está visible** — La pestaña **Logs** está activa. Cambie a cualquier otra pestaña (**Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**) y el selector reaparecerá en la esquina superior derecha de la barra de pestañas.
- **Los gráficos muestran "Collecting graph data" tras cambiar a un intervalo temporal más largo** — Los datos históricos solo están disponibles desde el momento en que AetherSDR se conectó. No se almacenan datos entre sesiones.

## Relacionado

- [Network Diagnostics overview](overview.md)
- [Measure RTT and packet drops during audio problems](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Check per-category data rates (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnose audio underruns and jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
