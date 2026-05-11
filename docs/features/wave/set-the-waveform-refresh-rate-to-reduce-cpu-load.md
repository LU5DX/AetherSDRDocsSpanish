# Referencia de configuración del applet de forma de onda

El applet de forma de onda proporciona un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de TX o RX. Ayuda a los operadores a detectar recortes, pérdidas de señal y problemas de nivel de audio de un vistazo.

## Descripción general

La pantalla de forma de onda renderiza muestras PCM mono de punto flotante de 32 bits recibidas del motor de audio. La dirección de TX tiene un tinte diferente al de RX, lo que hace que el lado activo sea obvio sin necesidad de leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.

## Interacciones con la pantalla de forma de onda

| Interacción | Comportamiento |
|---|---|
| Un clic en la pantalla | Alterna la pausa. Se congela una instantánea del búfer hasta que se vuelve a hacer clic. Útil para inspeccionar un transitorio. Aparece una insignia "PAUSED" en el pie de página mientras está en pausa. |
| Doble clic en la pantalla | Abre o cierra el panel de configuración. No borra el búfer; use el slot WaveformWidget::clear() o reconéctese para restablecerlo. |

## Indicadores de la pantalla de forma de onda

| Indicador | Estados | Significado |
|---|---|---|
| Tinte de dirección | RX (tinte frío), TX (tinte cálido) | Distingue visualmente si la forma de onda mostrada es el monitor de recepción o la ruta de transmisión saliente. |
| Resalte de recorte | Sin recorte (traza normal), Recorte (énfasis rojo, etiqueta CLIP N) | Las columnas que contienen muestras en o por encima de ±0.98 de escala completa se resaltan; aparece un contador 'CLIP N' en el encabezado. |
| Insignia PAUSED | En vivo (sin insignia), En pausa (insignia PAUSED en el pie de página) | Indica que la pantalla muestra una instantánea congelada y no el flujo de audio en vivo. |
| Marcador de posición sin audio | Forma de onda presente, mensaje 'no RX audio' / 'no TX audio' | Cuando no llegan muestras del osciloscopio en 1 segundo, se muestra un mensaje de marcador de posición en lugar de una traza vacía. |

## Modo de visualización

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el cuadro combinado View en la parte superior del panel.
3. Seleccione uno de los siguientes modos:

| Modo | Descripción |
|---|---|
| Scope | Gráfico = líneas de mín/máx + RMS |
| Envelope | Área rellena de pico/RMS |
| History | Barras de nivel horizontales |
| Bands | Barras de bandas de frecuencia mediante filtro Goertzel |

La configuración se persiste como `WaveApplet_ViewMode` con los valores 'Graph', 'Envelope', 'History' o 'Bands'.

## Deslizador de zoom

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el deslizador Zoom.
3. Arrastre el deslizador para ajustar el zoom de amplitud. El valor actual se muestra a la derecha del deslizador en el formato `N.Nx`.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Zoom | 1.7x (170%) | 1.0x–6.0x (100–600) | `WaveApplet_ZoomPercent` |

Los valores más altos estiran las señales pequeñas verticalmente, lo que hace que los artefactos de recorte aparezcan antes.

## Deslizador de FPS

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el deslizador FPS.
3. Arrastre el deslizador para ajustar la velocidad de actualización. El valor actual se muestra a la derecha del deslizador en el formato `N fps`.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| FPS | 24 Hz | 5–30 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la carga de la CPU en sistemas lentos. El ajuste no tiene efecto en la captura de audio ni en la precisión del nivel.

## Deslizador de ventana

1. Haga doble clic en la pantalla de forma de onda para abrir el panel de configuración.
2. Localice el deslizador Window en la parte inferior del panel.
3. Arrastre el deslizador para seleccionar una ventana de tiempo para la pantalla de forma de onda.

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Window | 1 s | 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s | `WaveApplet_TimeWindowMs` |

El deslizador utiliza pasos discretos. Las primeras tres posiciones son submilisegundo (240 ms, 480 ms, 1 s), luego incrementos de 1 segundo de 1 a 10 segundos. El valor actual se muestra a la derecha del deslizador.

Establecer una ventana más corta permite ver detalles finos en la forma de onda. Establecer una ventana más larga muestra la tendencia general y facilita la detección de eventos poco frecuentes.

**Nota de migración:** Si anteriormente configuró una ventana de tiempo usando el ajuste anterior `WaveApplet_TimeWindowSec`, se convierte automáticamente al paso discreto disponible más cercano en el primer uso. La clave anterior se elimina entonces de la configuración.

## Consejos

- Un valor de 5–10 fps es suficiente para monitorear niveles promedio y detectar recortes. Use valores más altos solo cuando necesite rastrear transitorios rápidos visualmente.
- El deslizador FPS utiliza un paso único de 5 y un paso de página de 10, por lo que al presionar las teclas de flecha o Re Pág/Av Pág en el deslizador, se mueve en esos incrementos.
- Los ajustes de zoom, FPS y ventana son independientes: cambiar uno no afecta a los demás.
- Use la función de pausa (un clic en la pantalla) para congelar la forma de onda e inspeccionar de cerca un transitorio o anomalía.

## Relacionados

- [Descripción general de forma de onda](overview.md)
- [Monitorear audio de TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
