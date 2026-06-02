# Referencia de Configuración del Applet de Forma de Onda

El applet de Forma de Onda proporciona un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de TX o RX. Ayuda a los operadores a detectar recortes, cortes y problemas de nivel de audio de un vistazo.

## Descripción General

La visualización de forma de onda renderiza muestras PCM mono float-32 recibidas del motor de audio. La dirección TX se tiñe de un color diferente al de RX, haciendo evidente el lado actual sin necesidad de leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.

## Interacciones con la visualización de forma de onda

| Interacción | Comportamiento |
|---|---|
| Un clic en la visualización | Alterna pausa. Se congela una instantánea del búfer hasta que se haga clic nuevamente. Útil para inspeccionar un transitorio. Aparece una insignia "PAUSED" en el pie de página mientras está en pausa. |
| Doble clic en la visualización | Abre o cierra el cajón de configuración. No limpia el búfer; use el slot WaveformWidget::clear() o reconéctese para reiniciar. |

El intervalo de discriminación de un clic se lee de la configuración de discriminación de clic en Radio Setup. Si ajusta este valor en Radio Setup, surte efecto inmediatamente sin necesidad de reiniciar la aplicación.

## Indicadores de la visualización de forma de onda

| Indicador | Estados | Significado |
|---|---|---|
| Tinte de dirección | RX (tinte frío), TX (tinte cálido) | Desambigua visualmente si la forma de onda mostrada es el monitor de recepción o la ruta de transmisión saliente. |
| Resaltado de recorte | Sin recorte (traza normal), Recorte (énfasis rojo, etiqueta CLIP N) | Las columnas que contienen muestras en ±0.98 o más de escala completa se resaltan; aparece un contador 'CLIP N' en el encabezado. |
| Insignia PAUSED | En vivo (sin insignia), En pausa (insignia PAUSED en el pie de página) | Indica que la visualización muestra una instantánea congelada y no el flujo de audio en vivo. |
| Marcador de posición sin audio | Forma de onda presente, mensaje 'no RX audio' / 'no TX audio' | Cuando no han llegado muestras de alcance dentro de 1 segundo, se muestra un mensaje de marcador de posición en lugar de una traza vacía. |

## Cajón de configuración

El cajón de configuración se puede abrir o cerrar con un doble clic en la visualización de forma de onda. Su estado expandido se conserva entre sesiones mediante la configuración `WaveApplet_DrawerExpanded`. Cuando cierra el cajón y reinicia AetherSDR, permanece cerrado hasta que haga doble clic en la visualización para reabrirlo.

## Modo de vista

1. Haga doble clic en la visualización de forma de onda para abrir el cajón de configuración.
2. Localice el cuadro combinado View en la parte superior del cajón.
3. Seleccione uno de los siguientes modos:

| Modo | Descripción |
|---|---|
| Scope | Gráfico = líneas de min/máx + RMS |
| Envelope | Área rellena de pico/RMS |
| History | Barras de nivel horizontales |
| Bands | Barras de bandas de frecuencia mediante filtro Goertzel |

La configuración se conserva como `WaveApplet_ViewMode` con los valores 'Graph', 'Envelope', 'History' o 'Bands'.

## Control deslizante de zoom

1. Haga doble clic en la visualización de forma de onda para abrir el cajón de configuración.
2. Localice el control deslizante Zoom.
3. Arrastre el control deslizante para ajustar el zoom de amplitud. El valor actual se muestra a la derecha del control deslizante en el formato `N.Nx`.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 1.7x (170%) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` |

Los valores más altos estiran las señales pequeñas verticalmente, haciendo que los artefactos de recorte aparezcan antes. El control deslizante usa el estilo de control deslizante principal del tema actual.

## Control deslizante de FPS

1. Haga doble clic en la visualización de forma de onda para abrir el cajón de configuración.
2. Localice el control deslizante FPS.
3. Arrastre el control deslizante para ajustar la velocidad de actualización. El valor actual se muestra a la derecha del control deslizante en el formato `N fps`.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| FPS | 24 Hz | 5–30 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la carga de la CPU en sistemas lentos. La configuración no tiene efecto en la captura de audio ni en la precisión del nivel. El control deslizante usa el estilo de control deslizante principal del tema actual.

## Control deslizante de ventana

1. Haga doble clic en la visualización de forma de onda para abrir el cajón de configuración.
2. Localice el control deslizante Window en la parte inferior del cajón.
3. Arrastre el control deslizante para seleccionar una ventana de tiempo para la visualización de forma de onda.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El control deslizante usa pasos discretos. Las tres primeras posiciones son de menos de un segundo (240 ms, 480 ms, 1 s), luego incrementos de 1 segundo de 1 a 10 segundos. El valor actual se muestra a la derecha del control deslizante. El control deslizante usa el estilo de control deslizante principal del tema actual.

Establecer una ventana más corta le permite ver detalles finos en la forma de onda. Establecer una ventana más larga muestra la tendencia general y facilita la detección de eventos poco frecuentes.

**Nota de migración:** Si configuró previamente una ventana de tiempo usando la configuración anterior `WaveApplet_TimeWindowSec`, se convierte automáticamente al paso discreto disponible más cercano en el primer uso. La clave antigua se elimina entonces de la configuración.

## Consejos

- Un valor de 5–10 fps es suficiente para monitorear niveles promedio y detectar recortes. Use valores más altos solo cuando necesite rastrear transitorios rápidos visualmente.
- El control deslizante FPS usa un paso de 5 y un paso de página de 10, por lo que presionar las teclas de flecha o Re Pág/Av Pág en el control deslizante lo mueve en esos incrementos.
- Las configuraciones de zoom, FPS y ventana son independientes: cambiar una no afecta a las otras.
- Use la función de pausa (un clic en la visualización) para congelar la forma de onda y examinar de cerca un transitorio o anomalía.

## Relacionado

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
