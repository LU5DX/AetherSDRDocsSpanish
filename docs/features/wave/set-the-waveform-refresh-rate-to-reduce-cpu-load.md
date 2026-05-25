# Referencia de Configuración del Applet de Forma de Onda

El applet de Forma de Onda proporciona un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de TX o RX. Ayuda a los operadores a detectar rápidamente recortes, caídas y problemas de nivel de audio.

## Descripción General

La visualización de forma de onda renderiza muestras PCM mono float-32 recibidas del motor de audio. La dirección TX se tiñe de forma diferente a RX, lo que hace obvio el lado actual sin necesidad de leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.

## Interacciones con la Visualización de Forma de Onda

| Interacción | Comportamiento |
|---|---|
| Un clic en la visualización | Alterna la pausa. Una captura del búfer se congela hasta que se hace clic nuevamente. Útil para inspeccionar un transitorio. Aparece una insignia "PAUSED" en el pie de página mientras está en pausa. |
| Doble clic en la visualización | Abre o cierra el panel de configuración. No borra el búfer — use el slot WaveformWidget::clear() o reconecte para reiniciar. |

El intervalo de discriminación de un clic se lee de la configuración de discriminación de clic de Radio Setup. Si ajusta este valor en Radio Setup, surte efecto inmediatamente sin necesidad de reiniciar la aplicación.

## Indicadores de la Visualización de Forma de Onda

| Indicador | Estados | Significado |
|---|---|---|
| Tinte de dirección | RX (tinte frío), TX (tinte cálido) | Desambigua visualmente si la forma de onda mostrada es el monitor de recepción o la ruta de transmisión saliente. |
| Resalte de recorte | Sin recorte (traza normal), Recorte (énfasis rojo, etiqueta CLIP N) | Las columnas que contienen muestras en o por encima de ±0.98 de escala completa se resaltan; aparece un contador 'CLIP N' en el encabezado. |
| Insignia PAUSED | En vivo (sin insignia), En pausa (insignia PAUSED en el pie de página) | Indica que la visualización muestra una captura congelada y no el flujo de audio en vivo. |
| Marcador de posición sin audio | Forma de onda presente, mensaje 'Enable PC Audio' / 'no TX audio' | Cuando no llegan muestras del alcance dentro de 1 segundo, se muestra un mensaje de marcador de posición en lugar de una traza vacía. Para RX, el mensaje dice "Enable PC Audio". Para TX, dice "no TX audio". |

## Panel de Configuración

El panel de configuración se puede abrir o cerrar haciendo doble clic en la visualización de forma de onda. Su estado expandido se conserva entre sesiones usando la configuración `WaveApplet_DrawerExpanded`. Cuando cierra el panel y reinicia AetherSDR, permanece cerrado hasta que haga doble clic en la visualización para reabrirlo.

## Modo de Vista

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el cuadro combinado View en la parte superior del panel.
3. Seleccione uno de los siguientes modos:

| Modo | Descripción |
|---|---|
| Scope | Gráfico = líneas mín/máx + RMS |
| Envelope | Área rellena pico/RMS |
| History | Barras de nivel horizontales |
| Bands | Barras de bandas de frecuencia mediante filtro Goertzel |

La configuración se conserva como `WaveApplet_ViewMode` con los valores 'Graph', 'Envelope', 'History' o 'Bands'.

## Control Deslizante de Zoom

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante Zoom.
3. Arrastre el control deslizante para ajustar el zoom de amplitud. El valor actual se muestra a la derecha del control deslizante en el formato `N.Nx`.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 1.7x (170%) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` |

Los valores más altos estiran las señales pequeñas verticalmente, lo que hace que los artefactos de recorte aparezcan antes.

## Control Deslizante de FPS

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante FPS.
3. Arrastre el control deslizante para ajustar la tasa de actualización. El valor actual se muestra a la derecha del control deslizante en el formato `N fps`.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| FPS | 24 Hz | 5–30 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la carga de la CPU en sistemas lentos. La configuración no tiene efecto en la captura de audio ni en la precisión del nivel.

## Control Deslizante de Ventana

1. Haga doble clic en la visualización de forma de onda para abrir el panel de configuración.
2. Localice el control deslizante Window en la parte inferior del panel.
3. Arrastre el control deslizante para seleccionar una ventana de tiempo para la visualización de forma de onda.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El control deslizante utiliza pasos discretos. Las primeras tres posiciones son sub-segundo (240 ms, 480 ms, 1 s), luego incrementos de 1 segundo desde 1 a 10 segundos. El valor actual se muestra a la derecha del control deslizante.

Establecer una ventana más corta le permite ver detalles finos en la forma de onda. Establecer una ventana más larga muestra la tendencia general y facilita la detección de eventos poco frecuentes.

**Nota de migración:** Si previamente estableció una ventana de tiempo usando la configuración anterior `WaveApplet_TimeWindowSec`, se convierte automáticamente al paso discreto disponible más cercano en el primer uso. La clave anterior se elimina entonces de la configuración.

## Consejos

- Un valor de 5–10 fps es suficiente para monitorear niveles promedio y detectar recortes. Use valores más altos solo cuando necesite rastrear transitorios rápidos visualmente.
- El control deslizante FPS utiliza un paso simple de 5 y un paso de página de 10, por lo que presionar las teclas de flecha o Re Pág/Av Pág en el control deslizante lo mueve en esos incrementos.
- Las configuraciones de zoom, FPS y ventana son independientes — cambiar una no afecta a las otras.
- Use la función de pausa (un clic en la visualización) para congelar la forma de onda e inspeccionar de cerca un transitorio o anomalía.

## Relacionado

- [Descripción general de forma de onda](overview.md)
- [Monitorear audio TX o RX en la visualización de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de forma de onda](adjust-waveform-amplitude-zoom.md)
