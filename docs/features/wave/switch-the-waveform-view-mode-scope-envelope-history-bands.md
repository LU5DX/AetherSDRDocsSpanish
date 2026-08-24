# Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)

El applet de Waveform ofrece cuatro modos de visualización para la ruta de audio activa. Cambiar de modo le permite elegir la representación que mejor se adapte a su tarea de monitoreo — por ejemplo, Bands para detectar desequilibrios de frecuencia en una señal de TX, o Scope para una traza tradicional en el dominio del tiempo.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la visualización de la forma de onda sin controles debajo, haga doble clic en la visualización de la forma de onda para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración si aún no está abierto.
2. En el cajón de configuración, localice la etiqueta **View:** en la primera fila.
3. Haga clic en el cuadro combinado a la derecha de **View:**. El cuadro combinado tiene un nombre accesible de "WAVE view mode".
4. Seleccione una de las cuatro opciones: **Scope**, **Envelope**, **History** o **Bands**.

La visualización se actualiza inmediatamente. La selección se guarda en `WaveApplet_ViewMode` y se restaura en el próximo inicio.

## Qué hace cada control

| Control               | Predeterminado | Valores válidos                                                                                                       |
|-----------------------|----------------|-----------------------------------------------------------------------------------------------------------------------|
| Cuadro combinado **View:** | Scope          | Scope, Envelope, History, Bands                                                                                       |
| Control deslizante **Window:** | 200 ms         | 10–500 ms                                                                                                             |
| Control deslizante **Zoom:** | 1.7x           | 1.0x – 6.0x (100–600)                                                                                                 |
| Control deslizante **FPS:** | 24 fps         | 5–30 Hz                                                                                                               |

## Controles del cajón de configuración

Todos los controles se encuentran en el cajón de configuración plegable debajo de la visualización de la forma de onda. Cada control tiene un nombre accesible para compatibilidad con lectores de pantalla:

| Control                        | Nombre accesible    | Clave de configuración                  | Comportamiento                                                         |
|--------------------------------|---------------------|-----------------------------------------|------------------------------------------------------------------------|
| Cuadro combinado **View:**     | WAVE view mode      | `WaveApplet_ViewMode`                   | Se persiste como 'Graph', 'Envelope', 'History' o 'Bands'              |
| Control deslizante **Zoom:**   | WAVE zoom           | `WaveApplet_ZoomPercent`                | Escala el eje de amplitud; predeterminado 170 (1.7x)                   |
| Control deslizante **FPS:**    | WAVE FPS            | `WaveApplet_RefreshRateHz`              | Controla la velocidad de repintado; predeterminado 24 fps, rango 5–30 Hz |
| Control deslizante **Window:** | WAVE window         | `WaveApplet_TimeWindowMs`               | Ventana de tiempo mostrada; predeterminado 200 ms, rango 10–500 ms     |

**Nota:** La clave heredada `WaveApplet_TimeWindowSec` se migra a `WaveApplet_TimeWindowMs` en el primer inicio. El estado plegado del cajón se persiste entre reinicios de la aplicación mediante `WaveApplet_DrawerExpanded`.

## Consejos

- El modo **Bands** utiliza un filtro de Goertzel para derivar barras de bandas de frecuencia. Es útil para verificar si la energía del audio de TX está distribuida en el rango de frecuencia esperado.
- El modo **History** muestra barras de nivel horizontales acumuladas a lo largo del tiempo, lo que facilita ver tendencias de nivel sostenidas en comparación con una traza momentánea.
- Si la visualización muestra un mensaje de **"no RX audio"** o **"no TX audio"**, no han llegado muestras de scope en el último segundo. Para la ruta de RX, habilite PC Audio en la configuración del radio. Para la ruta de TX, verifique que el micrófono o la entrada de línea esté activa. La configuración del modo de vista aún se aplica y tendrá efecto tan pronto como se reanude el audio.
- Un solo clic en la visualización de la forma de onda alterna la pausa. Si la visualización parece congelada, haga clic una vez para reanudar las actualizaciones en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.
- El estado del cajón de configuración (abierto o cerrado) se persiste. Si cierra el cajón y reinicia AetherSDR, permanecerá cerrado. Haga doble clic en la forma de onda para reabrirlo.
- La ruta de audio de TX está teñida con un color cálido y la ruta de RX con un color frío, para que pueda identificar la dirección activa de un vistazo sin leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.
- Cuando ocurre recorte (muestras en o por encima de ±0.98 de escala completa), las columnas afectadas se resaltan en rojo y aparece un contador **CLIP N** en el encabezado.

## Solución de problemas

- **El cuadro combinado View: no es visible** — El cajón de configuración está cerrado. Haga doble clic en la visualización de la forma de onda para abrirlo.
- **El modo seleccionado no persiste después del reinicio** — Confirme que AetherSDR tiene acceso de escritura a su almacenamiento de configuración. Si el problema se repite, verifique que no haya otra instancia de AetherSDR ejecutándose simultáneamente que sobrescriba `WaveApplet_ViewMode` al salir.
- **La visualización muestra un mensaje de marcador de posición en lugar de una forma de onda** — No han llegado muestras de scope en el último segundo. Verifique que la fuente de audio esté activa. Para la ruta de RX, asegúrese de que PC Audio esté habilitado en la configuración del radio. Para la ruta de TX, confirme que el micrófono o la entrada de línea esté activa.
- **La visualización de la forma de onda parece congelada** — La visualización puede estar en pausa. Haga un solo clic en la forma de onda para reanudar las actualizaciones en vivo. Una insignia **PAUSED** en el pie de página confirma el estado de pausa.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la visualización de la forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Pausar la forma de onda para inspeccionar un transitorio](pause-the-waveform-to-inspect-a-transient.md)
- [Configurar la tasa de actualización de la forma de onda para reducir la carga de CPU](set-the-waveform-refresh-rate-to-reduce-cpu-load.md)
- Configurar la ventana de tiempo de la forma de onda
