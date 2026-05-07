# Cambiar el marco temporal de los gráficos de historial (1 minuto a 1 semana)

El control **Marco temporal** establece cuánto tiempo atrás muestran el historial los gráficos de series temporales en el cuadro de diálogo de Diagnóstico de red. Úselo para alejar la vista y analizar tendencias a largo plazo o acercarla para examinar un breve período de pérdida de paquetes o latencia.

## Antes de comenzar

- Abra el cuadro de diálogo Diagnóstico de red mediante `Settings > Network...`.
- Navegue a cualquier pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**. El control **Marco temporal** está oculto cuando la pestaña **Logs** está activa.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el cuadro de diálogo Diagnóstico de red.
2. Seleccione una pestaña de gráfico — **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**.
3. Localice el cuadro combinado **Marco temporal** en la esquina superior derecha de la barra de pestañas.
4. Haga clic en **Marco temporal** y seleccione el valor deseado de la lista desplegable.

Los gráficos se actualizan inmediatamente para mostrar la ventana de historial seleccionada.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| **Marco temporal** | Cuadro combinado | 5 minutos | 1 minuto, 5 minutos, 15 minutos, 1 hora, 1 día, 1 semana | Establece cuánto tiempo atrás muestran el historial todos los gráficos de series temporales. Oculto cuando la pestaña **Logs** está activa. |

## Consejos

- El selector **Marco temporal** se aplica a todas las pestañas de gráficos simultáneamente. Cambiar de pestaña después de modificar el valor mantiene la misma ventana.
- Seleccionar **1 semana** en una sesión recién conectada mostrará un área de gráfico vacía hasta que se hayan recopilado suficientes datos. Los gráficos muestran "Collecting graph data" hasta que haya al menos un punto de datos disponible.
- Use **1 minuto** o **5 minutos** para aislar una interrupción de audio o un pico de latencia específicos; use **1 hora** o más para evaluar la estabilidad general del enlace durante una sesión.

## Solución de problemas

- **El selector de marco temporal no es visible** — La pestaña **Logs** está activa. Cambie a cualquier otra pestaña (**Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**) y el selector reaparecerá en la esquina superior derecha de la barra de pestañas.
- **Los gráficos muestran "Collecting graph data" después de cambiar a un marco temporal más largo** — Los datos históricos solo están disponibles desde el momento en que AetherSDR se conectó. No se almacenan datos entre sesiones.

## Relacionados

- [Información general del Diagnóstico de red](overview.md)
- [Medir RTT y caídas de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar tasas de datos por categoría (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subejecuciones de audio y fluctuación de fase](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
