# Descripción general del applet de forma de onda

El applet de forma de onda es un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de RX o TX. Úselo para detectar recortes, caídas y problemas de nivel de audio de un vistazo sin necesidad de un medidor externo.

## Cómo funciona

El applet renderiza una ventana de tiempo de audio mono en desplazamiento. La duración de la ventana es ajustable de 240 ms a 10 segundos mediante un control deslizante de pasos discretos en el panel de configuración. La pantalla se alimenta continuamente con muestras del motor de audio. Cada columna de píxeles muestra la envolvente mín/máx de las muestras que caen dentro de ella, con trazas separadas de envolvente de pico y RMS superpuestas.

La línea de encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS. El pie de página muestra la frecuencia de muestreo, la duración de la ventana y el tiempo por división.

Dos búferes circulares separados (uno para RX y otro para TX) se ejecutan en paralelo. La pantalla dibuja desde el búfer que coincida con el estado de transmisión actual. Cuando cambia de recepción a transmisión, el tinte cambia y la pantalla comienza inmediatamente a dibujar desde el búfer de TX.

Para abrir o cerrar el applet, haga clic en el botón de la bandeja **WAVE** en la fila 1 de la barra lateral derecha. El applet está activado por defecto y se inserta inmediatamente después del botón EQ en la primera ejecución después de actualizar a v0.9.1.

El applet ya no impone una altura fija; se redimensiona verticalmente con el diseño.

## Función de cada control

| Control                 | Comportamiento                                                                                                                                                                                   | Notas                                                                                                                  |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Pantalla de forma de onda | Renderiza muestras de osciloscopio PCM mono float-32. Muestra la forma de onda mín/máx, envolvente RMS, marcadores de pico y resaltes de recorte en el modo de vista activo.                     | La dirección TX tiene un tinte diferente a RX para que el lado activo sea obvio sin leer una etiqueta. La lectura del encabezado muestra RX/TX, RMS dBFS y PK dBFS. |
| Un clic en la pantalla | Alterna entre vivo y pausado. Mientras está pausado, se retiene una instantánea del búfer hasta que haga clic de nuevo.                                                                          | Aparece una insignia **PAUSED** en el pie de página. El estado predeterminado es vivo.                                |
| Doble clic en la pantalla | Abre o cierra el panel de configuración.                                                                                                                                                        | No borra el búfer. Para restablecer la pantalla, use el slot WaveformWidget::clear() o reconéctese.                     |
| Vista                    | Selecciona el modo de visualización de la forma de onda: Scope (Gráfico = líneas mín/máx + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de bandas de frecuencia mediante filtro Goertzel). | Se encuentra en el panel de configuración plegable debajo de la forma de onda. Se conserva como `WaveApplet_ViewMode`.  |
| Zoom                    | Escala el eje de amplitud; los valores más altos estiran las señales pequeñas verticalmente, haciendo que los artefactos de recorte aparezcan antes.                                            | Se encuentra en el panel de configuración. Valor predeterminado 170% (1.7x). Se conserva como `WaveApplet_ZoomPercent`. |
| FPS                     | Controla la frecuencia con la que se redibuja la forma de onda; los valores más bajos reducen la carga de CPU en sistemas lentos.                                                                | Se encuentra en el panel de configuración. Se conserva como `WaveApplet_RefreshRateHz`.                                 |
| Ventana                 | Establece la duración de la ventana de tiempo. Pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s.                                                                  | Se encuentra en el panel de configuración. Se conserva como `WaveApplet_TimeWindowMs`. Valor predeterminado 1000 ms (1 s). |

### Controles del panel de configuración

El panel de configuración contiene los siguientes controles:

- **View** — Cuadro combinado. Selecciona el modo de visualización de la forma de onda. Opciones: Scope, Envelope, History, Bands. Se conserva como `WaveApplet_ViewMode`.
- **Zoom** — Control deslizante. Escalado de amplitud de 1.0x a 6.0x. Valor predeterminado 1.7x (170%). Se conserva como `WaveApplet_ZoomPercent`.
- **FPS** — Control deslizante. Frecuencia de actualización de 5 a 30 Hz. Valor predeterminado 24 Hz. Se conserva como `WaveApplet_RefreshRateHz`.
- **Window** — Control deslizante. Duración de la ventana de tiempo. Pasos: 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s. Valor predeterminado 1 s. Se conserva como `WaveApplet_TimeWindowMs`.

En el lanzamiento inicial después de actualizar desde una versión que usaba `WaveApplet_TimeWindowSec`, su configuración de ventana anterior se migra al paso disponible más cercano en el nuevo sistema de pasos discretos.

## Indicadores

- **Tinte de dirección** — La pantalla usa un tinte frío para RX y un tinte cálido para TX, de modo que la ruta de audio activa sea inequívoca sin leer la etiqueta del encabezado.
- **Resalte de recorte** — Cualquier columna de píxeles que contenga muestras en o por encima del umbral de recorte se resalta en rojo en los bordes superior e inferior del gráfico. También aparece un contador **CLIP N** en el encabezado, en negrita roja, que muestra la cantidad de muestras recortadas en la ventana actual.
- **Insignia PAUSED** — Se muestra en el pie de página cuando la pantalla está congelada en una instantánea. Sin insignia significa que la pantalla está en vivo.
- **Marcador de posición sin audio** — Si no han llegado muestras en el último segundo, o el búfer de la pantalla está vacío, un mensaje de marcador de posición reemplaza la traza vacía. Para la ruta RX, el mensaje dice "Enable PC Audio". Para la ruta TX, el mensaje dice "no TX audio".

## Consejos

- El color de la forma de onda y el grosor de la línea siguen la configuración de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` utilizada en otras partes de AetherSDR. El rango válido de grosor de línea es de 1.0 a 3.0 px; el valor predeterminado es 2.0.
- Las líneas de cuadrícula se pueden suprimir mediante `DisplayShowGrid`. Cuando está habilitado, la pantalla dibuja líneas de cuadrícula mayores y menores detrás de la traza.
- Hacer clic una vez para pausar es particularmente útil para capturar un transitorio: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada y luego haga clic de nuevo para reanudar.
- Haga doble clic en la pantalla para alternar el panel de configuración. Para borrar el búfer de forma de onda, use el slot WaveformWidget::clear() o reconéctese al motor de audio.
- El control deslizante de ventana solo proporciona pasos discretos; no permite el desplazamiento libre a través de valores en milisegundos. Use el paso más cercano que capture el intervalo de tiempo que necesita.

## Relacionado

- [Use the waveform display to monitor TX or RX audio](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pause and clear the waveform display](pause-and-clear-the-waveform-display.md)
