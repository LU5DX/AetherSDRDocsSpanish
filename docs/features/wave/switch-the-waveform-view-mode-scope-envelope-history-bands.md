# Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)

El applet Waveform ofrece cuatro modos de visualización para la ruta de audio activa. Cambiar entre modos le permite elegir la representación que mejor se adapte a su tarea de monitoreo; por ejemplo, Bands para detectar desequilibrios de frecuencia en una señal de TX, o Scope para una traza tradicional en el dominio del tiempo.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la visualización de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración, si aún no está abierto.
2. En el cajón de configuración, localice la etiqueta **View:** en la primera fila.
3. Haga clic en el cuadro combinado a la derecha de **View:**.
4. Seleccione una de las cuatro opciones: **Scope**, **Envelope**, **History** o **Bands**.

La pantalla se actualiza de inmediato. La selección se guarda en `WaveApplet_ViewMode` y se restaura en el próximo inicio.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave persistida | Comportamiento |
|---------|----------------------|-----------------|------------------|----------------|
| Cuadro combinado **View:** | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra líneas de mínimo/máximo y RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de banda de frecuencia. |
| Deslizador **Zoom:** | 1.7x | 1.0x – 6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas. |
| Deslizador **FPS:** | 24 fps | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de repintado. Los valores más bajos reducen la carga de la CPU. |

## Consejos

- El modo **Bands** utiliza un filtro Goertzel para obtener las barras de banda de frecuencia. Es útil para verificar si la energía de audio de TX está distribuida en el rango de frecuencia esperado.
- El modo **History** muestra barras de nivel horizontales acumuladas a lo largo del tiempo, lo que facilita ver tendencias de nivel sostenidas en comparación con una traza momentánea.
- Si la pantalla muestra un mensaje "no RX audio" o "no TX audio", no han llegado muestras del alcance en el último segundo. La configuración del modo de visualización aún se aplica y tendrá efecto tan pronto como se reanude el audio.
- Un solo clic en la visualización de la forma de onda alterna la pausa. Si la pantalla parece congelada, haga clic una vez para reanudar las actualizaciones en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.

## Solución de problemas

- **El cuadro combinado View: no es visible** — El cajón de configuración está cerrado. Haga doble clic en la visualización de la forma de onda para abrirlo.
- **El modo seleccionado no persiste después de reiniciar** — Confirme que AetherSDR tenga acceso de escritura a su almacenamiento de configuración. Si el problema se repite, verifique que no haya otra instancia de AetherSDR ejecutándose simultáneamente y sobrescribiendo `WaveApplet_ViewMode` al salir.

## Relacionados

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
