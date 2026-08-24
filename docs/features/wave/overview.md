# Descripción general del applet de forma de onda

El applet de forma de onda es un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio RX o TX activa en uno de cuatro modos de vista (Scope, Envelope, History bars, Bands spectrum). Úselo para detectar recortes, pérdidas de señal y problemas de nivel de audio de un vistazo, sin necesidad de un medidor externo.

## Cómo funciona

El applet representa una ventana de tiempo desplazable de audio mono. La duración de la ventana es ajustable de 10 ms a 500 ms mediante un control deslizante en el panel de ajustes. La pantalla recibe continuamente muestras del motor de audio. Cada columna de píxeles muestra la envolvente mín/máx de las muestras que caen dentro de ella, con trazas separadas de envolvente RMS y pico dibujadas encima.

La línea de encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel de pico en dBFS.

Dos buffers circulares separados (uno para RX y otro para TX) funcionan en paralelo. La pantalla dibuja desde el buffer que coincida con el estado de transmisión actual. Cuando cambia de recepción a transmisión, el tinte cambia y la pantalla comienza a dibujar inmediatamente desde el buffer TX.

Para abrir o cerrar el applet, haga clic en el botón **WAVE** de la bandeja en la fila 1 de la barra lateral derecha. El applet está activado por defecto y se inserta inmediatamente después del botón EQ en la primera ejecución tras actualizar a v0.9.1.

El applet ya no impone una altura fija; se redimensiona verticalmente con el diseño.

## Qué hace cada control

| Control                 | Comportamiento                                                                                                                                                                                                                                   | Notas                                                                                                                                                                                                     |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pantalla de forma de onda | Muestra muestras PCM mono de coma flotante de 32 bits. Representa la forma de onda mín/máx, la envolvente RMS, los marcadores de pico y los resaltados de recorte en el modo de vista activo.                                                     | La dirección TX se tiñe de forma diferente a la RX para que el lado activo sea obvio sin leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS.                                   |
| Un clic en la pantalla     | Alterna entre activo y pausado. Mientras está pausado, se mantiene una instantánea del buffer hasta que haga clic de nuevo.                                                                                                                       | Aparece una insignia **PAUSED** en el pie de página. El estado predeterminado es activo.                                                                                                                  |
| Doble clic en la pantalla  | Alterna el panel de ajustes abierto o cerrado.                                                                                                                                                                                                   | No limpia el buffer. Para restablecer la pantalla, use el slot `WaveformWidget::clear()` o reconéctese.                                                                                                   |
| View                    | Selecciona el modo de visualización de la forma de onda: Scope (Graph = líneas mín/máx + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de bandas de frecuencia mediante filtro Goertzel). | Ubicado en el panel de ajustes plegable debajo de la forma de onda. Se persiste como `WaveApplet_ViewMode`.                                                                                                |
| Zoom                    | Escala el eje de amplitud; los valores más altos estiran las señales pequeñas verticalmente, lo que hace que los artefactos de recorte aparezcan antes.                                                                                          | Ubicado en el panel de ajustes. Valor predeterminado 170% (1.7x). Se persiste como `WaveApplet_ZoomPercent`.                                                                                               |
| FPS                     | Controla la frecuencia con la que se repinta la forma de onda; los valores más bajos reducen la carga de CPU en sistemas lentos.                                                                                                                 | Ubicado en el panel de ajustes. Rango de 5 a 30 Hz. Valor predeterminado 24 Hz. Se persiste como `WaveApplet_RefreshRateHz`.                                                                               |
| Window                  | Controla la ventana de tiempo mostrada en la pantalla de forma de onda, en milisegundos. Los valores más grandes muestran más historial con resolución reducida.                                                                                  | Ubicado en el panel de ajustes. Rango de 10 a 500 ms. Valor predeterminado 200 ms. Se persiste como `WaveApplet_TimeWindowMs`.                                                                             |

### Controles del panel de ajustes

El panel de ajustes contiene los siguientes controles:

- **View** cuadro combinado: selecciona el modo de visualización de la forma de onda. Opciones: Scope, Envelope, History, Bands. Se persiste como `WaveApplet_ViewMode`.
- **Zoom** control deslizante: escala de amplitud de 1.0x a 6.0x. Valor predeterminado 1.7x (170%). Se persiste como `WaveApplet_ZoomPercent`. Los cambios se guardan inmediatamente en la configuración.
- **FPS** control deslizante: frecuencia de actualización de 5 a 30 Hz. Valor predeterminado 24 Hz. Se persiste como `WaveApplet_RefreshRateHz`. Los cambios se guardan inmediatamente en la configuración.
- **Window** control deslizante: duración de la ventana de tiempo de 10 a 500 ms. Valor predeterminado 200 ms. Se persiste como `WaveApplet_TimeWindowMs`.

En el lanzamiento inicial tras actualizar desde una versión que usaba `WaveApplet_TimeWindowSec`, su ajuste de ventana anterior se migra al valor en milisegundos disponible más cercano.

Los estilos de los controles deslizantes ahora son sensibles al tema: la ranura, la subpágina y los colores del controlador se adaptan al tema activo en lugar de usar la paleta fija `#203040`/`#00b4d8`/`#c8d8e8`. Los colores de las etiquetas también siguen los tokens `color.text.primary` y `color.text.secondary` del tema.

### Estado del panel de ajustes

El panel de ajustes recuerda si estaba abierto o cerrado la última vez que cerró el applet. Si cierra el applet con el panel abierto, estará abierto la próxima vez que abra el applet. Si cierra el applet con el panel cerrado, permanecerá cerrado en el siguiente lanzamiento. El estado se persiste como `WaveApplet_DrawerExpanded`.

## Indicadores

- **Tinte de dirección**: la pantalla usa un tinte frío para RX y un tinte cálido para TX, de modo que la ruta de audio activa sea inequívoca sin leer la etiqueta del encabezado.
- **Resaltado de recorte**: cualquier columna de píxeles que contenga muestras en o por encima del umbral de recorte se resalta en rojo en los bordes superior e inferior del gráfico. También aparece un contador **CLIP N** en el encabezado, en rojo negrita, que muestra el número de muestras recortadas en la ventana actual.
- **Insignia PAUSED**: se muestra en el pie de página cuando la pantalla está congelada en una instantánea. Sin insignia significa que la pantalla está activa.
- **Marcador de posición sin audio**: si no han llegado muestras en el último segundo, o si el buffer de la pantalla está vacío, un mensaje de marcador de posición reemplaza la traza vacía. Para la ruta RX, el mensaje dice "no RX audio". Para la ruta TX, el mensaje dice "no TX audio".

## Consejos

- El color y el grosor de línea de la forma de onda siguen los ajustes de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` utilizados en otras partes de AetherSDR. El rango válido de grosor de línea es de 1.0 a 3.0 px; el valor predeterminado es 2.0.
- Las líneas de cuadrícula se pueden suprimir mediante `DisplayShowGrid`. Cuando está habilitado, la pantalla dibuja líneas de cuadrícula mayores y menores detrás de la traza.
- Un clic para pausar es particularmente útil para capturar un transitorio: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada y luego haga clic de nuevo para reanudar.
- El doble clic en la pantalla alterna el panel de ajustes. Para limpiar el buffer de la forma de onda, use el slot `WaveformWidget::clear()` o reconéctese al motor de audio.
- El intervalo de discriminación de clics utilizado para iniciar el temporizador de alternancia de pausa se lee del ajuste de intervalo de discriminación de clics de Radio Setup. Esto le permite ajustar la sincronización del doble clic en todos los applets sin reiniciar AetherSDR.

## Relacionado

- [Use the waveform display to monitor TX or RX audio](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pause and clear the waveform display](pause-and-clear-the-waveform-display.md)
