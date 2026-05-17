# Referencia de configuración del applet de forma de onda

El applet de forma de onda proporciona un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de TX o RX. Ayuda a los operadores a detectar recortes, cortes y problemas de nivel de audio de un vistazo.

## Descripción general

La visualización de forma de onda representa muestras PCM mono de coma flotante de 32 bits recibidas del motor de audio. La dirección TX tiene un tinte diferente al de RX, lo que permite identificar el lado activo sin necesidad de leer una etiqueta. El encabezado muestra RX/TX, RMS dBFS y PK dBFS.

## Interacciones con la visualización de forma de onda

| Interacción | Comportamiento |
|---|---|
| Un clic en la pantalla | Alterna la pausa. Se congela una instantánea del búfer hasta que se hace clic de nuevo. Útil para inspeccionar un transitorio. Aparece una insignia "PAUSED" en el pie de página mientras está en pausa. |
| Doble clic en la pantalla | Abre o cierra el panel de configuración. No borra el búfer; use la ranura WaveformWidget::clear() o reconéctese para restablecerlo. |

## Indicadores de la visualización de forma de onda

| Indicador | Estados | Significado |
|---|---|---|
| Tinte de dirección | RX (tinte frío), TX (tinte cálido) | Distingue visualmente si la forma de onda mostrada es el monitor de recepción o la ruta de transmisión saliente. |
| Resalte de recorte | Sin recorte (traza normal), Recorte (énfasis en rojo, etiqueta CLIP N) | Las columnas que contienen muestras en o por encima de ±0.98 de escala completa se resaltan; aparece un contador 'CLIP N' en el encabezado. |
| Insignia PAUSED | En vivo (sin insignia), En pausa (insignia PAUSED en el pie de página) | Indica que la pantalla muestra una instantánea congelada y no la transmisión de audio en vivo. |
| Marcador de posición sin audio | Forma de onda presente, mensaje 'Enable PC Audio' / 'no TX audio' | Cuando no llegan muestras del osciloscopio en 1 segundo, se muestra un mensaje de marcador de posición en lugar de una traza vacía. Para RX, el mensaje dice "Enable PC Audio". Para TX, dice "no TX audio". |

## Modo de vista

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el cuadro combinado View en la parte superior del panel.
3. Seleccione uno de los siguientes modos:

| Modo | Descripción |
|---|---|
| Scope | Gráfico = líneas de mín/máx + RMS |
| Envelope | Área rellena de pico/RMS |
| History | Barras de nivel horizontales |
| Bands | Barras de bandas de frecuencia mediante filtro Goertzel |

La configuración se guarda como `WaveApplet_ViewMode` con los valores 'Graph', 'Envelope', 'History' o 'Bands'.

## Control deslizante de zoom

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante Zoom.
3. Arrastre el control deslizante para ajustar el zoom de amplitud. El valor actual se muestra a la derecha del control deslizante en el formato `N.Nx`.

| Control | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|
| Zoom | 1.7x (170%) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` |

Los valores más altos estiran verticalmente las señales pequeñas, lo que hace que los artefactos de recorte aparezcan antes.

## Control deslizante de FPS

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante FPS.
3. Arrastre el control deslizante para ajustar la frecuencia de actualización. El valor actual se muestra a la derecha del control deslizante en el formato `N fps`.

| Control | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|
| FPS | 24 Hz | 5–30 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la carga de la CPU en sistemas lentos. La configuración no afecta la captura de audio ni la precisión del nivel.

## Control deslizante de ventana

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante Window en la parte inferior del panel.
3. Arrastre el control deslizante para seleccionar una ventana de tiempo para la visualización de la forma de onda.

| Control | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El control deslizante utiliza pasos discretos. Las tres primeras posiciones son de menos de un segundo (240 ms, 480 ms, 1 s), luego incrementos de 1 segundo de 1 a 10 segundos. El valor actual se muestra a la derecha del control deslizante.

Configurar una ventana más corta le permite ver detalles finos en la forma de onda. Configurar una ventana más larga muestra la tendencia general y facilita la detección de eventos poco frecuentes.

**Nota de migración:** Si anteriormente configuró una ventana de tiempo usando la opción anterior `WaveApplet_TimeWindowSec`, se convertirá automáticamente al paso discreto disponible más cercano en el primer uso. Luego, la clave anterior se elimina de la configuración.

## Consejos

- Un valor de 5 a 10 fps es suficiente para monitorear los niveles promedio y detectar recortes. Use valores más altos solo cuando necesite rastrear transitorios rápidos visualmente.
- El control deslizante de FPS usa un paso único de 5 y un paso de página de 10, por lo que presionar las teclas de flecha o Av Pág/Re Pág en el control deslizante lo mueve en esos incrementos.
- Las configuraciones de zoom, FPS y ventana son independientes: cambiar una no afecta a las otras.
- Use la función de pausa (un clic en la pantalla) para congelar la forma de onda e inspeccionar de cerca un transitorio o anomalía.

## Relacionado

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
