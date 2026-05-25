# Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)

El applet WAVE ofrece cuatro modos de visualización para la ruta de audio activa. Cambiar de modo le permite elegir la representación que mejor se adapte a su tarea de monitoreo — por ejemplo, Bands para detectar desequilibrios de frecuencia en una señal de TX, o Scope para una traza tradicional en el dominio del tiempo.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la visualización de la forma de onda sin controles debajo, haga doble clic en la visualización para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. En el cajón de configuración, localice la etiqueta **View:** en la primera fila.
3. Haga clic en el cuadro combinado a la derecha de **View:**.
4. Seleccione una de las cuatro opciones: **Scope**, **Envelope**, **History** o **Bands**.

La visualización se actualiza de inmediato. La selección se guarda en `WaveApplet_ViewMode` y se restaura en el próximo inicio.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave persistida | Comportamiento |
|---------|----------------------|-----------------|------------------|----------------|
| Cuadro combinado **View:** | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra líneas de mínimo/máximo y RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de banda de frecuencia. |
| Deslizador **Window:** | 1 s | Pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s | `WaveApplet_TimeWindowMs` | Establece la ventana de tiempo mostrada en la forma de onda. Ventanas más cortas (240 ms, 480 ms) proporcionan detalle en transitorios rápidos; ventanas más largas (hasta 10 s) ofrecen una vista más amplia de la dinámica del audio. |
| Deslizador **Zoom:** | 1.7x | 1.0x – 6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas. |
| Deslizador **FPS:** | 24 fps | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de repintado. Los valores más bajos reducen la carga de la CPU. |

## Consejos

- El modo **Bands** utiliza un filtro Goertzel para derivar barras de banda de frecuencia. Es útil para verificar si la energía del audio de TX está distribuida en el rango de frecuencia esperado.
- El modo **History** muestra barras de nivel horizontales acumuladas a lo largo del tiempo, lo que facilita ver tendencias de nivel sostenidas en comparación con una traza momentánea.
- Si la visualización muestra un mensaje **"Enable PC Audio"** (para la ruta de RX) o un mensaje **"no TX audio"**, no han llegado muestras de scope en el último segundo. Para la ruta de RX, habilite PC Audio en la configuración de la radio. Para la ruta de TX, verifique que el micrófono o la entrada de línea estén activos. La configuración del modo de visualización aún se aplica y entrará en vigor tan pronto como se reanude el audio.
- Un solo clic en la visualización de la forma de onda alterna la pausa. Si la visualización parece congelada, haga clic una vez para reanudar la actualización en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.
- El estado del cajón de configuración (abierto o cerrado) se persiste. Si cierra el cajón y reinicia AetherSDR, permanecerá cerrado. Haga doble clic en la forma de onda para volver a abrirlo.
- El deslizador **Window:** utiliza pasos discretos con paradas deliberadas, no un rango continuo. Cada muesca en el deslizador corresponde a una de las ventanas de tiempo disponibles: 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s o 10 s.

## Solución de problemas

- **El cuadro combinado View: no es visible** — El cajón de configuración está cerrado. Haga doble clic en la visualización de la forma de onda para abrirlo.
- **El modo seleccionado no persiste después del reinicio** — Confirme que AetherSDR tenga acceso de escritura a su almacenamiento de configuración. Si el problema se repite, verifique que ninguna otra instancia de AetherSDR se esté ejecutando simultáneamente y sobrescribiendo `WaveApplet_ViewMode` al salir.
- **El deslizador Window: parece tener posiciones limitadas** — Esto es por diseño. El deslizador proporciona 12 pasos de ventana de tiempo discretos en lugar de un rango continuo, para que pueda seleccionar rápidamente una longitud de ventana estándar sin ajuste fino.
- **La visualización muestra "Enable PC Audio" en lugar de "no RX audio"** — Este mensaje indica que PC Audio debe estar habilitado en la configuración de la radio para la ruta de RX. Navegue a Radio > Audio y habilite PC Audio.

## Relacionados

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la visualización de la forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Establecer la frecuencia de actualización de la forma de onda para reducir la carga de la CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- Establecer la ventana de tiempo de la forma de onda
