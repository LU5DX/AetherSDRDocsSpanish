# Referencia de configuración del applet de forma de onda

El applet de forma de onda proporciona un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio TX o RX activa en uno de cuatro modos de vista (Scope, Envelope, History bars, Bands spectrum). Ayuda a los operadores a detectar recortes, pérdidas de señal y problemas de nivel de audio de un vistazo. La ruta TX se tiñe de forma diferente a la RX para que la dirección actual sea inequívoca.

## Descripción general

La visualización de forma de onda renderiza muestras PCM mono de float-32 recibidas del motor de audio. La dirección TX se tiñe de forma diferente a la RX, lo que hace evidente el lado actual sin leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.

El renderizado de la forma de onda utiliza QPainter con reducción incremental mediante WaveformScopeModel: los repintes combinan contenedores previamente plegados en lugar de volver a escanear la ventana sin procesar, por lo que el costo de pintado ya no escala con la ventana de tiempo.

## Interacciones con la visualización de forma de onda

| Interacción | Comportamiento | Notas |
|---|---|---|
| Un clic en la visualización | Alterna la pausa. Se congela una instantánea del búfer hasta que se haga clic nuevamente. Útil para inspeccionar un transitorio. Aparece una insignia "PAUSED" en el pie de página mientras está en pausa. | El intervalo de discriminación de un clic se lee de la configuración de discriminación de clic en Radio Setup. Si ajusta este valor en Radio Setup, surte efecto de inmediato sin reiniciar la aplicación. |
| Doble clic en la visualización | Alterna el panel de configuración abierto o cerrado. No borra el búfer — use el slot WaveformWidget::clear() o reconecte para restablecer. | |

## Indicadores de la visualización de forma de onda

| Indicador | Estados | Significado |
|---|---|---|
| Tinte de dirección | RX (tinte frío), TX (tinte cálido) | Distingue visualmente si la forma de onda mostrada es el monitor de recepción o la ruta de transmisión saliente. |
| Resaltado de recorte | Sin recorte (traza normal), Recorte (énfasis en rojo, etiqueta CLIP N) | Las columnas que contienen muestras en o por encima de ±0.98 de escala completa se resaltan; aparece un contador 'CLIP N' en el encabezado. |
| Insignia PAUSED | En vivo (sin insignia), En pausa (insignia PAUSED en el pie de página) | Indica que la visualización muestra una instantánea congelada y no la transmisión de audio en vivo. |
| Marcador de posición sin audio | Forma de onda presente, mensaje 'no RX audio' / 'no TX audio' | Cuando no llegan muestras de alcance dentro de 1 segundo, se muestra un mensaje de marcador de posición en lugar de una traza vacía. |

## Panel de configuración

El panel de configuración puede alternarse abierto o cerrado haciendo doble clic en la visualización de forma de onda. Su estado expandido se conserva entre sesiones mediante la configuración `WaveApplet_DrawerExpanded`. Cuando cierra el panel y reinicia AetherSDR, permanece cerrado hasta que haga doble clic en la visualización para reabrirlo.

## Modo de vista

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el cuadro combinado View en la parte superior del panel. El cuadro combinado tiene nombre de objeto `waveViewCombo` y nombre accesible "WAVE view mode".
3. Seleccione uno de los siguientes modos:

| Modo | Descripción |
|---|---|
| Scope | Gráfico = líneas de mín/máx + RMS |
| Envelope | Área rellena de pico/RMS |
| History | Barras de nivel horizontales |
| Bands | Barras de banda de frecuencia mediante filtro Goertzel |

La configuración se conserva como `WaveApplet_ViewMode` con valores 'Graph', 'Envelope', 'History' o 'Bands'.

## Control deslizante de zoom

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante de Zoom. El control deslizante tiene nombre de objeto `waveZoomSlider` y nombre accesible "WAVE zoom".
3. Arrastre el control deslizante para ajustar el zoom de amplitud. El valor actual se muestra a la derecha del control deslizante en el formato `N.Nx`.

| Control | Predeterminado | Rango válido | Clave conservada |
|---|---|---|---|
| Zoom | 1.7x (170%) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` |

Los valores más altos estiran las señales pequeñas verticalmente, lo que hace que los artefactos de recorte aparezcan antes. El control deslizante usa el estilo de control deslizante principal del tema actual.

## Control deslizante de FPS

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante de FPS. El control deslizante tiene nombre de objeto `waveFpsSlider` y nombre accesible "WAVE FPS".
3. Arrastre el control deslizante para ajustar la tasa de refresco. El valor actual se muestra a la derecha del control deslizante en el formato `N fps`.

| Control | Predeterminado | Rango válido | Clave conservada |
|---|---|---|---|
| FPS | 24 Hz | 5–30 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la carga de CPU en sistemas lentos. El valor predeterminado de 24 fps proporciona una respuesta de alcance suave con una carga moderada en la CPU. Los usuarios que hayan guardado previamente un valor de FPS explícito conservan su configuración existente — el valor predeterminado solo se aplica cuando la clave de configuración está ausente.

La configuración no tiene efecto en la captura de audio ni en la precisión de nivel. El control deslizante usa el estilo de control deslizante principal del tema actual.

## Control deslizante de ventana

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante de Window en la parte inferior del panel. El control deslizante tiene nombre de objeto `waveWindowSlider` y nombre accesible "WAVE window".
3. Arrastre el control deslizante para seleccionar una ventana de tiempo para la visualización de forma de onda.

| Control | Predeterminado | Rango válido | Clave conservada |
|---|---|---|---|
| Window | 200 ms | 10–500 ms | `WaveApplet_TimeWindowMs` |

El control deslizante usa pasos discretos de la matriz de pasos de ventana. El valor actual se muestra a la derecha del control deslizante. El control deslizante usa el estilo de control deslizante principal del tema actual.

Configurar una ventana más corta le permite ver detalles finos en la forma de onda. Configurar una ventana más larga muestra más historial con resolución reducida.

**Nota de migración:** Si configuró previamente una ventana de tiempo usando la configuración más antigua `WaveApplet_TimeWindowSec`, se convierte automáticamente al paso discreto disponible más cercano en el primer uso. La clave antigua se elimina entonces de la configuración.

## Consejos

- Un valor de 5–10 fps es suficiente para monitorear niveles promedio y detectar recortes. Use valores más altos solo cuando necesite rastrear transitorios rápidos visualmente.
- El control deslizante de FPS usa un paso único de 5 y un paso de página de 10, por lo que presionar las teclas de flecha o Av Pág/Re Pág en el control deslizante lo mueve en esos incrementos.
- La configuración de zoom, FPS y ventana son independientes — cambiar una no afecta a las otras.
- Use la función de pausa (un clic en la visualización) para congelar la forma de onda e inspeccionar de cerca un transitorio o anomalía.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio TX o RX en la visualización de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
