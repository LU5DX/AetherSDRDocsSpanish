# Cambiar el período de tiempo de los gráficos de historial (1 minuto a 1 semana)

El control **Timeframe** establece hasta qué punto en el pasado muestran historial los gráficos de series temporales en el diálogo Network Diagnostics. Úselo para alejar la vista y analizar tendencias a largo plazo, o para acercarla y examinar una ráfaga breve de pérdida de paquetes o latencia.

## Antes de comenzar

- Abra el diálogo Network Diagnostics desde `Settings > Network...`.
- Navegue a cualquier pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**. El control **Timeframe** se oculta cuando la pestaña **Logs** está activa.

## Pasos

1. Haga clic en `Settings > Network...` para abrir el diálogo Network Diagnostics.
2. Seleccione una pestaña de gráfico: **Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**.
3. Ubique el cuadro combinado **Timeframe** en la esquina superior derecha de la barra de pestañas.
4. Haga clic en **Timeframe** y seleccione el valor deseado en la lista desplegable.

Los gráficos se actualizan de inmediato para mostrar la ventana de historial seleccionada.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| **Timeframe** | Cuadro combinado | 5 minutes | 1 minute, 5 minutes, 15 minutes, 1 hour, 1 day, 1 week | Establece hasta qué punto en el pasado muestran historial todos los gráficos de series temporales. Se oculta cuando la pestaña **Logs** está activa. |

## Consejos

- El selector **Timeframe** se aplica a todas las pestañas de gráfico de forma simultánea. Cambiar de pestaña después de modificar el valor mantiene la misma ventana.
- Si selecciona **1 week** en una sesión recién conectada, el área del gráfico aparecerá vacía hasta que se hayan recopilado suficientes datos. Los gráficos muestran "Collecting graph data" hasta que haya al menos un punto de datos disponible.
- Use **1 minute** o **5 minutes** para aislar un corte de audio o un pico de latencia específicos; use **1 hour** o más para evaluar la estabilidad general del enlace durante una sesión.

## Solución de problemas

- **El selector Timeframe no es visible** — La pestaña **Logs** está activa. Cambie a cualquier otra pestaña (**Overview**, **Latency**, **Rates**, **Packet Loss** o **Audio**) y el selector reaparecerá en la esquina superior derecha de la barra de pestañas.
- **Los gráficos muestran "Collecting graph data" tras cambiar a un período de tiempo más largo** — Los datos históricos solo están disponibles desde el momento en que AetherSDR se conectó. No se almacenan datos entre sesiones.

## Relacionado

- [Descripción general de Network Diagnostics](overview.md)
- [Medir RTT y pérdida de paquetes durante problemas de audio](measure-rtt-and-packet-drops-during-audio-problems.md)
- [Verificar las tasas de datos por categoría (audio, FFT, waterfall, meters, DAX)](check-per-category-data-rates-audio-fft-waterfall-meters-dax.md)
- [Diagnosticar subdesbordamientos de audio y jitter](../../troubleshooting/networkdiagnostics/diagnose-audio-underruns-and-jitter.md)
