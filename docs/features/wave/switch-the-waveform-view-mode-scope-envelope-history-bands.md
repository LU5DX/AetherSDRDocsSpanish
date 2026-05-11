# Cambie el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)

El applet de forma de onda ofrece cuatro modos de visualización para la ruta de audio activa. Cambiar de modo le permite elegir la representación que mejor se adapte a su tarea de monitoreo — por ejemplo, Bands para detectar desequilibrios de frecuencia en una señal de TX, o Scope para una traza tradicional en el dominio del tiempo.

## Antes de comenzar

- El applet WAVE debe ser visible en el panel de applets. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la visualización de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. En el cajón de configuración, localice la etiqueta **View:** en la primera fila.
3. Haga clic en el cuadro combinado a la derecha de **View:**.
4. Seleccione una de las cuatro opciones: **Scope**, **Envelope**, **History** o **Bands**.

La visualización se actualiza de inmediato. La selección se guarda en `WaveApplet_ViewMode` y se restaura en el próximo inicio.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave persistida | Comportamiento |
|---------|----------------------|-----------------|------------------|----------------|
| Cuadro combinado **View:** | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra líneas de mínimo, máximo y RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de bandas de frecuencia. |
| Control deslizante **Window:** | 1 s | Pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s | `WaveApplet_TimeWindowMs` | Define la ventana de tiempo mostrada en la forma de onda. Ventanas más cortas (240 ms, 480 ms) proporcionan detalle en transitorios rápidos; ventanas más largas (hasta 10 s) ofrecen una vista más amplia de la dinámica del audio. |
| Control deslizante **Zoom:** | 1.7x | 1.0x – 6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala el eje de amplitud. Valores más altos estiran verticalmente las señales pequeñas. |
| Control deslizante **FPS:** | 24 fps | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de repintado. Valores más bajos reducen la carga de la CPU. |

## Consejos

- El modo **Bands** utiliza un filtro Goertzel para derivar las barras de bandas de frecuencia. Es útil para verificar si la energía del audio de TX se distribuye en el rango de frecuencia esperado.
- El modo **History** muestra barras de nivel horizontales acumuladas a lo largo del tiempo, lo que facilita ver tendencias de nivel sostenidas en comparación con una traza momentánea.
- Si la pantalla muestra un mensaje "no RX audio" o "no TX audio", no han llegado muestras de alcance en el último segundo. La configuración del modo de visualización aún se aplica y entrará en vigor tan pronto como se reanude el audio.
- Un solo clic en la visualización de la forma de onda activa o desactiva la pausa. Si la pantalla parece congelada, haga clic una vez para reanudar las actualizaciones en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.
- El control deslizante **Window:** utiliza pasos discretos con paradas deliberadas, no un rango continuo. Cada muesca en el control deslizante corresponde a una de las ventanas de tiempo disponibles: 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s o 10 s.

## Solución de problemas

- **El cuadro combinado View: no es visible** — El cajón de configuración está cerrado. Haga doble clic en la visualización de la forma de onda para abrirlo.
- **El modo seleccionado no persiste después de reiniciar** — Confirme que AetherSDR tenga acceso de escritura a su almacenamiento de configuración. Si el problema se repite, verifique que no haya otra instancia de AetherSDR ejecutándose simultáneamente y sobrescribiendo `WaveApplet_ViewMode` al salir.
- **El control deslizante Window: parece tener posiciones limitadas** — Esto es por diseño. El control deslizante proporciona 12 pasos discretos de ventana de tiempo en lugar de un rango continuo, para que pueda seleccionar rápidamente una longitud de ventana estándar sin necesidad de ajuste fino.

## Relacionados

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- [Set the waveform time window](set-the-waveform-time-window.md)
