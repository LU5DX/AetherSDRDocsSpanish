# Referencia de Configuración del Applet de Forma de Onda

El applet de Forma de Onda proporciona un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio TX o RX activa en uno de cuatro modos de vista (Osciloscopio, Envolvente, Barras de Historial, Espectro de Bandas). Ayuda a los operadores a detectar recortes, caídas y problemas de nivel de audio de un vistazo. La ruta TX se tiñe de forma diferente a la RX para que la dirección actual sea inequívoca.

## Descripción General

La visualización de forma de onda renderiza muestras PCM mono float-32 recibidas del motor de audio. La dirección TX se tiñe de forma diferente a la RX, haciendo evidente el lado actual sin necesidad de leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.

El renderizado de la forma de onda utiliza QPainter con reducción incremental a través de WaveformScopeModel: las repintadas fusionan bins previamente plegados en lugar de volver a escanear la ventana sin procesar, por lo que el costo de pintado ya no escala con la ventana de tiempo.

## Interacciones con la Pantalla de Forma de Onda

| Interacción | Comportamiento | Notas |
|---|---|---|
| Un clic en la pantalla | Alterna la pausa. Se congela una instantánea del búfer hasta que se hace clic de nuevo. Útil para inspeccionar un transitorio. Aparece una insignia "PAUSED" en el pie de página mientras está en pausa. | |
| Doble clic en la pantalla | Abre o cierra el panel de configuración. No borra el búfer: use el slot WaveformWidget::clear() o reconéctese para reiniciarlo. | |

El intervalo de discriminación de un clic se lee de la configuración de discriminación de clic en Configuración de Radio. Si ajusta este valor en Configuración de Radio, surte efecto inmediatamente sin necesidad de reiniciar la aplicación.

## Indicadores de la Pantalla de Forma de Onda

| Indicador | Estados | Significado |
|---|---|---|
| Tinte de dirección | RX (tinte frío), TX (tinte cálido) | Distingue visualmente si la forma de onda mostrada es el monitor de recepción o la ruta de transmisión saliente. |
| Resaltado de recorte | Sin recorte (traza normal), Recorte (énfasis rojo, etiqueta CLIP N) | Las columnas que contienen muestras en o por encima de ±0.98 de escala completa se resaltan; aparece un contador 'CLIP N' en el encabezado. |
| Insignia PAUSED | En vivo (sin insignia), En pausa (insignia PAUSED en el pie de página) | Indica que la pantalla muestra una instantánea congelada y no el flujo de audio en vivo. |
| Marcador de sin audio | Forma de onda presente, mensaje 'no RX audio' / 'no TX audio' | Cuando no llegan muestras del alcance en 1 segundo, se muestra un mensaje de marcador de posición en lugar de una traza vacía. |

## Panel de Configuración

El panel de configuración se puede abrir o cerrar haciendo doble clic en la pantalla de forma de onda. Su estado expandido se conserva entre sesiones usando la configuración `WaveApplet_DrawerExpanded`. Cuando cierra el panel y reinicia AetherSDR, permanece cerrado hasta que haga doble clic en la pantalla para reabrirlo.

## Modo de Vista

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el cuadro combinado Vista en la parte superior del panel. El cuadro combinado tiene el nombre de objeto `waveViewCombo` y el nombre accesible "WAVE view mode".
3. Seleccione uno de los siguientes modos:

| Modo | Descripción |
|---|---|
| Scope | Gráfico = líneas de mínimo/máximo + RMS |
| Envelope | Área rellena de pico/RMS |
| History | Barras de nivel horizontales |
| Bands | Barras de banda de frecuencia mediante filtro Goertzel |

La configuración se conserva como `WaveApplet_ViewMode` con los valores 'Graph', 'Envelope', 'History' o 'Bands'.

## Control Deslizante de Zoom

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante Zoom. El control deslizante tiene el nombre de objeto `waveZoomSlider` y el nombre accesible "WAVE zoom".
3. Arrastre el control deslizante para ajustar el zoom de amplitud. El valor actual se muestra a la derecha del control deslizante en el formato `N.Nx`.

| Control | Valor predeterminado | Rango válido | Clave conservada |
|---|---|---|---|
| Zoom | 1.7x (170%) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` |

Los valores más altos estiran las señales pequeñas verticalmente, lo que hace que los artefactos de recorte aparezcan antes. El control deslizante usa el estilo de control deslizante principal del tema actual.

## Control Deslizante de FPS

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante FPS. El control deslizante tiene el nombre de objeto `waveFpsSlider` y el nombre accesible "WAVE FPS".
3. Arrastre el control deslizante para ajustar la tasa de actualización. El valor actual se muestra a la derecha del control deslizante en el formato `N fps`.

| Control | Valor predeterminado | Rango válido | Clave conservada |
|---|---|---|---|
| FPS | 25 Hz | 5–60 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la carga de la CPU en sistemas lentos. El rango superior se ha extendido a 60 Hz para usuarios que desean una respuesta de alcance más rápida. El valor predeterminado de 25 fps proporciona una cadencia tranquila y de baja sobrecarga que coincide con la tasa habitual del panadapter de radio. Los usuarios que guardaron previamente un valor de FPS explícito conservan su configuración existente; el valor predeterminado solo se aplica cuando la clave de configuración está ausente.

La configuración no tiene efecto en la captura de audio ni en la precisión del nivel. El control deslizante usa el estilo de control deslizante principal del tema actual.

## Control Deslizante de Ventana

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante Ventana en la parte inferior del panel. El control deslizante tiene el nombre de objeto `waveWindowSlider` y el nombre accesible "WAVE window".
3. Arrastre el control deslizante para seleccionar una ventana de tiempo para la pantalla de forma de onda.

| Control | Valor predeterminado | Rango válido | Clave conservada |
|---|---|---|---|
| Window | 200 ms | 10–500 ms | `WaveApplet_TimeWindowMs` |

El control deslizante utiliza pasos discretos de la matriz de pasos de ventana. El valor actual se muestra a la derecha del control deslizante. El control deslizante usa el estilo de control deslizante principal del tema actual.

Establecer una ventana más corta le permite ver detalles finos en la forma de onda. Establecer una ventana más larga muestra más historia con resolución reducida.

**Nota de migración:** Si configuró previamente una ventana de tiempo usando la configuración anterior `WaveApplet_TimeWindowSec`, se convierte automáticamente al paso discreto disponible más cercano en el primer uso. La clave anterior se elimina entonces de la configuración.

## Consejos

- Un valor de 5–10 fps es suficiente para monitorear niveles promedio y detectar recortes. Use valores más altos solo cuando necesite rastrear transitorios rápidos visualmente.
- El control deslizante FPS usa un paso único de 5 y un paso de página de 10, por lo que presionar las teclas de flecha o Re Pág/Av Pág en el control deslizante lo mueve en esos incrementos.
- Las configuraciones de zoom, FPS y ventana son independientes: cambiar una no afecta a las otras.
- Use la función de pausa (un clic en la pantalla) para congelar la forma de onda para una inspección detallada de un transitorio o anomalía.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
