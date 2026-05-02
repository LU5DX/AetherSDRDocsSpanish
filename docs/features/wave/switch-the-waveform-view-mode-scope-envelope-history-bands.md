# Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)

El applet Waveform ofrece cuatro modos de visualización para la ruta de audio activa. Cambiar de modo le permite elegir la representación más adecuada para su tarea de monitoreo — por ejemplo, Bands para detectar desequilibrio de frecuencia en una señal TX, o Scope para una traza tradicional en el dominio del tiempo.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón WAVE de la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la pantalla de la forma de onda sin controles debajo, haga doble clic en la pantalla de la forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la pantalla de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. En el cajón de configuración, localice la etiqueta **View:** en la primera fila.
3. Haga clic en el cuadro combinado a la derecha de **View:**.
4. Seleccione una de las cuatro opciones: **Scope**, **Envelope**, **History** o **Bands**.

La pantalla se actualiza de inmediato. La selección se guarda en `WaveApplet_ViewMode` y se restaura en el próximo inicio.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave persistida | Comportamiento |
|---------|----------------------|-----------------|------------------|----------------|
| Cuadro combinado **View:** | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra líneas de mínimo/máximo y RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de banda de frecuencia. |
| Control deslizante **Zoom:** | 1.7x | 1.0x – 6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales débiles. |
| Control deslizante **FPS:** | 24 fps | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de actualización de la pantalla. Los valores más bajos reducen la carga de la CPU. |

## Sugerencias

- El modo **Bands** utiliza un filtro de Goertzel para derivar las barras de banda de frecuencia. Es útil para verificar si la energía del audio TX se distribuye en el rango de frecuencias esperado.
- El modo **History** muestra barras de nivel horizontales acumuladas en el tiempo, lo que facilita la observación de tendencias de nivel sostenidas en comparación con una traza momentánea.
- Si la pantalla muestra un mensaje "no RX audio" o "no TX audio", no han llegado muestras al osciloscopio en el último segundo. El ajuste del modo de visualización sigue aplicado y tendrá efecto en cuanto se reanude el audio.
- Un solo clic en la pantalla de la forma de onda activa o desactiva la pausa. Si la pantalla parece congelada, haga clic una vez para reanudar las actualizaciones en vivo. Un indicador **PAUSED** en el pie de pantalla confirma el estado de pausa.

## Solución de problemas

- **El cuadro combinado View: no es visible** — El cajón de configuración está cerrado. Haga doble clic en la pantalla de la forma de onda para abrirlo.
- **El modo seleccionado no persiste tras el reinicio** — Confirme que AetherSDR tiene acceso de escritura a su almacenamiento de configuración. Si el problema se repite, verifique que no haya otra instancia de AetherSDR en ejecución simultáneamente que esté sobreescribiendo `WaveApplet_ViewMode` al cerrar.

## Relacionados

- [Descripción general del Waveform](overview.md)
- [Monitorear audio TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Establecer la tasa de actualización de la forma de onda para reducir la carga de la CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
