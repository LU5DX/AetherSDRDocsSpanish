# Descripción general del applet Waveform

El applet Waveform es un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de RX o TX. Úselo para detectar recorte, pérdidas y problemas de nivel de audio de un vistazo sin necesidad de un medidor externo.

## Cómo funciona

El applet renderiza una ventana de tiempo desplazable de audio mono. La duración de la ventana es ajustable desde 240 ms hasta 10 segundos mediante un control deslizante de pasos discretos en el panel de configuración. La pantalla se alimenta continuamente con muestras del motor de audio. Cada columna de píxeles muestra la envolvente mín/máx de las muestras que caen dentro de ella, con trazos separados de envolvente RMS y de pico superpuestos.

La línea de encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel de pico en dBFS. El pie de página muestra la tasa de muestreo, la duración de la ventana y el tiempo por división.

Dos búferes circulares separados (uno para RX y otro para TX) se ejecutan en paralelo. La pantalla dibuja desde el búfer que coincida con el estado de transmisión actual. Cuando cambia de recepción a transmisión, el tinte cambia y la pantalla comienza inmediatamente a dibujar desde el búfer de TX.

Para abrir o cerrar el applet, haga clic en el botón de la bandeja **WAVE** en la fila 1 de la barra lateral derecha. El applet está activado por defecto y se inserta inmediatamente después del botón EQ en la primera ejecución después de actualizar a v0.9.1.

El applet ya no impone una altura fija; se redimensiona verticalmente con el diseño.

## Función de cada control

| Control                 | Comportamiento                                                                                                                                                                                         | Notas                                                                                                                   |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Pantalla de forma de onda | Renderiza muestras de osciloscopio PCM mono float-32. Muestra la forma de onda mín/máx, la envolvente RMS, los marcadores de pico y los destaques de recorte en el modo de vista activo. | La dirección TX tiene un tinte diferente al de RX para que el lado activo sea obvio sin leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS. |
| Un clic en la pantalla | Alterna entre activo y pausado. Mientras está en pausa, se mantiene una instantánea del búfer hasta que haga clic de nuevo. | Aparece una insignia **PAUSED** en el pie de página. El estado predeterminado es activo. |
| Doble clic en la pantalla | Abre o cierra el panel de configuración. | No borra el búfer. Para restablecer la pantalla, use el slot WaveformWidget::clear() o vuelva a conectar. |
| Vista (View)            | Selecciona el modo de visualización de la forma de onda: Scope (Gráfico = líneas mín/máx + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de banda de frecuencia mediante filtro Goertzel). | Se encuentra en el panel de configuración colapsable debajo de la forma de onda. Se conserva como `WaveApplet_ViewMode`. |
| Zoom                    | Escala el eje de amplitud; los valores más altos estiran las señales pequeñas verticalmente, haciendo que los artefactos de recorte aparezcan antes. | Se encuentra en el panel de configuración. Valor predeterminado 170% (1.7x). Se conserva como `WaveApplet_ZoomPercent`. |
| FPS                     | Controla la frecuencia con la que se vuelve a pintar la forma de onda; los valores más bajos reducen la carga de CPU en sistemas lentos. | Se encuentra en el panel de configuración. Se conserva como `WaveApplet_RefreshRateHz`. |
| Ventana (Window)        | Establece la duración de la ventana de tiempo. Pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s. | Se encuentra en el panel de configuración. Se conserva como `WaveApplet_TimeWindowMs`. Valor predeterminado 1000 ms (1 s). |

### Controles del panel de configuración

El panel de configuración contiene los siguientes controles:

- Cuadro combinado **View** — Selecciona el modo de visualización de la forma de onda. Opciones: Scope, Envelope, History, Bands. Se conserva como `WaveApplet_ViewMode`.
- Control deslizante **Zoom** — Escalado de amplitud de 1.0x a 6.0x. Valor predeterminado 1.7x (170%). Se conserva como `WaveApplet_ZoomPercent`.
- Control deslizante **FPS** — Frecuencia de actualización de 5 a 30 Hz. Valor predeterminado 24 Hz. Se conserva como `WaveApplet_RefreshRateHz`.
- Control deslizante **Window** — Duración de la ventana de tiempo. Pasos: 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s. Valor predeterminado 1 s. Se conserva como `WaveApplet_TimeWindowMs`.

En el inicio inicial después de actualizar desde una versión que usaba `WaveApplet_TimeWindowSec`, su configuración de ventana anterior se migra al paso disponible más cercano en el nuevo sistema de pasos discretos.

### Estado del panel de configuración

El panel de configuración recuerda si estaba abierto o cerrado la última vez que cerró el applet. Si cierra el applet con el panel abierto, se abrirá la próxima vez que abra el applet. Si cierra el applet con el panel cerrado, permanecerá cerrado en el próximo inicio. El estado se conserva como `WaveApplet_DrawerExpanded`.

## Indicadores

- **Tinte de dirección** — La pantalla usa un tinte frío para RX y un tinte cálido para TX para que la ruta de audio activa sea inequívoca sin leer la etiqueta del encabezado.
- **Destacado de recorte** — Cualquier columna de píxeles que contenga muestras en o por encima del umbral de recorte se destaca en rojo en los bordes superior e inferior del gráfico. También aparece un contador **CLIP N** en el encabezado, en negrita roja, que muestra el número de muestras recortadas en la ventana actual.
- **Insignia PAUSED** — Se muestra en el pie de página cuando la pantalla está congelada en una instantánea. Sin insignia significa que la pantalla está activa.
- **Marcador de posición sin audio** — Si no han llegado muestras en el último segundo, o el búfer de la pantalla está vacío, un mensaje de marcador de posición reemplaza el trazo vacío. Para la ruta RX, el mensaje dice "Enable PC Audio". Para la ruta TX, el mensaje dice "no TX audio".

## Consejos

- El color de la forma de onda y el ancho de línea siguen las configuraciones de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` utilizadas en otras partes de AetherSDR. El rango válido de ancho de línea es de 1.0 a 3.0 px; el valor predeterminado es 2.0.
- Las líneas de cuadrícula se pueden suprimir mediante `DisplayShowGrid`. Cuando está habilitado, la pantalla dibuja líneas de cuadrícula principales y secundarias detrás del trazo.
- Un solo clic para pausar es particularmente útil para capturar un transitorio: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada, luego haga clic nuevamente para reanudar.
- El doble clic en la pantalla alterna el panel de configuración. Para borrar el búfer de forma de onda, use el slot WaveformWidget::clear() o vuelva a conectar al motor de audio.
- El control deslizante de ventana solo proporciona pasos discretos; no permite el desplazamiento libre a través de valores de milisegundos. Use el paso más cercano que capture el lapso de tiempo que necesita.
- El intervalo de discriminación de clic utilizado para iniciar el temporizador de alternancia de pausa se lee de la configuración del intervalo de discriminación de clic de Radio Setup. Esto le permite ajustar la sincronización de doble clic en todos los applets sin reiniciar AetherSDR.

## Relacionado

- [Use the waveform display to monitor TX or RX audio](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pause and clear the waveform display](pause-and-clear-the-waveform-display.md)
