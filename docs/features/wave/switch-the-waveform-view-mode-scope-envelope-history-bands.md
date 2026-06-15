# Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)

El applet Waveform ofrece cuatro modos de visualización para la ruta de audio activa. Cambiar de modo le permite elegir la representación que mejor se adapte a su tarea de monitoreo — por ejemplo, Bands para detectar desequilibrios de frecuencia en una señal de TX, o Scope para una traza tradicional en el dominio del tiempo.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El applet debe estar activo. Si la visualización de la forma de onda está completamente oculta o no aparece ninguna alimentación de audio, el applet puede estar en modo lean (completamente deshabilitado). No puede interactuar con el applet mientras esté inactivo.
- El cajón de configuración debe estar abierto. Si solo ve la visualización de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. En el cajón de configuración, localice la etiqueta **View:** en la primera fila.
3. Haga clic en el cuadro combinado a la derecha de **View:**.
4. Seleccione una de las cuatro opciones: **Scope**, **Envelope**, **History** o **Bands**.

La visualización se actualiza de inmediato. La selección se guarda en `WaveApplet_ViewMode` y se restaura en el próximo inicio.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave persistida | Comportamiento |
|---------|---------------------|-----------------|------------------|----------------|
| Cuadro combinado **View:** | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` | Selecciona el modo de visualización. Scope muestra líneas de mínimo/máximo y RMS. Envelope muestra un área rellena de pico/RMS. History muestra barras de nivel horizontales. Bands muestra barras de bandas de frecuencia. |
| Deslizador **Window:** | 1 s | Pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s | `WaveApplet_TimeWindowMs` | Establece la ventana de tiempo mostrada en la forma de onda. Ventanas más cortas (240 ms, 480 ms) proporcionan detalle en transitorios rápidos; ventanas más largas (hasta 10 s) ofrecen una vista más amplia de la dinámica de audio. |
| Deslizador **Zoom:** | 1.7x | 1.0x – 6.0x (100–600) | `WaveApplet_ZoomPercent` | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas. |
| Deslizador **FPS:** | 24 fps | 5–30 Hz | `WaveApplet_RefreshRateHz` | Controla la frecuencia de repintado. Los valores más bajos reducen la carga de la CPU. |

## Modo lean

Cuando AetherSDR opera en modo lean, el applet Waveform está completamente deshabilitado. Esto significa:

- El applet está oculto a la vista.
- La alimentación de audio se descarta — no se procesan muestras de osciloscopio y no se produce ningún repintado. Esto detiene el repintado de software de 24 Hz y evita que el búfer de muestras acumule datos.
- La señal del motor de audio ascendente (AudioEngine) sigue disparándose una vez por cada callback de audio (el evento Qt aún se coloca en la cola del hilo de la GUI), pero el trabajo de añadir y repintar se omite por completo.

El modo lean reduce la carga de la CPU en sistemas con recursos limitados. Mientras el applet está inactivo, ninguno de sus controles (View, Window, Zoom, FPS) se puede ajustar.

## Consejos

- El modo **Bands** utiliza un filtro Goertzel para derivar las barras de bandas de frecuencia. Es útil para verificar si la energía de audio de TX está distribuida en el rango de frecuencia esperado.
- El modo **History** muestra barras de nivel horizontales acumuladas a lo largo del tiempo, lo que facilita ver tendencias de nivel sostenidas en comparación con una traza momentánea.
- Si la visualización muestra un mensaje **"Enable PC Audio"** (para la ruta de RX) o un mensaje **"no TX audio"**, no han llegado muestras de osciloscopio en el último segundo. Para la ruta de RX, habilite PC Audio en la configuración de la radio. Para la ruta de TX, verifique que el micrófono o la entrada de línea estén activos. La configuración del modo de visualización aún se aplica y tendrá efecto tan pronto como se reanude el audio.
- Un solo clic en la visualización de la forma de onda alterna la pausa. Si la visualización parece congelada, haga clic una vez para reanudar las actualizaciones en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.
- El estado del cajón de configuración (abierto o cerrado) se persiste. Si cierra el cajón y reinicia AetherSDR, permanecerá cerrado. Haga doble clic en la forma de onda para volver a abrirlo.
- El deslizador **Window:** utiliza pasos discretos con paradas deliberadas, no un rango continuo. Cada muesca en el deslizador corresponde a una de las ventanas de tiempo disponibles: 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s. La apariencia del deslizador se adapta al tema activo.
- Los deslizadores **Zoom:** y **FPS:** utilizan un estilo consciente del tema. El color de su manija y pista coincide con la selección de tema actual para proporcionar una retroalimentación visual consistente en temas claros y oscuros.
- La ruta de audio de TX se tiñe con un color cálido y la ruta de RX con un color frío, para que pueda identificar la dirección activa de un vistazo sin leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.
- Cuando ocurre recorte (muestras en o por encima de ±0.98 de escala completa), las columnas afectadas se resaltan en rojo y aparece un contador **CLIP N** en el encabezado.

## Solución de problemas

- **El cuadro combinado View: no está visible** — El cajón de configuración está cerrado. Haga doble clic en la visualización de la forma de onda para abrirlo.
- **El modo seleccionado no persiste después del reinicio** — Confirme que AetherSDR tenga acceso de escritura a su almacenamiento de configuración. Si el problema se repite, verifique que no haya otra instancia de AetherSDR ejecutándose simultáneamente y sobrescribiendo `WaveApplet_ViewMode` al salir.
- **El deslizador Window: parece tener posiciones limitadas** — Esto es por diseño. El deslizador proporciona 12 pasos discretos de ventana de tiempo en lugar de un rango continuo, para que pueda seleccionar rápidamente una longitud de ventana estándar sin necesidad de ajuste fino.
- **La visualización muestra "Enable PC Audio" en lugar de "no RX audio"** — Este mensaje indica que PC Audio debe estar habilitado en la configuración de la radio para la ruta de RX. Navegue a Radio > Audio y habilite PC Audio.
- **La visualización de la forma de onda está en blanco o completamente ausente** — El applet puede estar en modo lean (completamente deshabilitado). Verifique si AetherSDR se está ejecutando en una configuración de ahorro de recursos. Si es así, el applet está intencionalmente oculto y no se puede usar hasta que se deshabilite el modo lean.

## Relacionados

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Pause the waveform to inspect a transient](pause-the-waveform-to-inspect-a-transient.md)
- [Set the waveform refresh rate to reduce CPU load](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- Set the waveform time window
