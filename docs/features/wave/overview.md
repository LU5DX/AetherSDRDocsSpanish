# Descripción general del applet de forma de onda

El applet de forma de onda es un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de RX o TX. Úselo para detectar recorte, pérdidas y problemas de nivel de audio de un vistazo, sin necesidad de un medidor externo.

## Cómo funciona

El applet representa una ventana de tiempo desplazable de audio mono. La duración de la ventana es ajustable de 240 ms a 10 segundos mediante un control deslizante de pasos discretos en el panel de configuración. La pantalla recibe continuamente muestras del motor de audio. Cada columna de píxeles muestra la envolvente mín./máx. de las muestras que caen dentro de ella, con trazas de envolvente de pico y RMS superpuestas.

La línea de encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel pico en dBFS. El pie de página muestra la frecuencia de muestreo, la duración de la ventana y el tiempo por división.

Dos búferes circulares separados (uno para RX y otro para TX) se ejecutan en paralelo. La pantalla dibuja desde el búfer que coincida con el estado de transmisión actual. Cuando cambia de recepción a transmisión, el tono de color cambia y la pantalla comienza inmediatamente a dibujar desde el búfer de TX.

Para abrir o cerrar el applet, haga clic en el botón de bandeja **WAVE** en la fila 1 de la barra lateral derecha. El applet está activado por defecto y se inserta inmediatamente después del botón EQ en la primera ejecución después de actualizar a v0.9.1.

El applet ya no impone una altura fija; se redimensiona verticalmente con el diseño.

## Función de cada control

| Control                     | Comportamiento                                                                                                                                                                                | Notas                                                                                                              |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Pantalla de forma de onda   | Renderiza la envolvente mín./máx. por columna de píxeles con trazas de envolvente de pico y RMS sobre la ventana de tiempo configurada.                                                       | Sin clave de configuración persistente.                                                                            |
| Un clic en la pantalla      | Alterna entre vivo y pausado. Mientras está en pausa, se mantiene una captura del búfer hasta que haga clic de nuevo.                                                                        | Aparece una insignia **PAUSED** en el pie de página. El estado predeterminado es vivo.                              |
| Doble clic en la pantalla   | Abre o cierra el panel de configuración.                                                                                                                                                     | No borra el búfer. Para restablecer la pantalla, use el método WaveformWidget::clear() o reconéctese.               |
| Vista (View)                | Selecciona el modo de visualización de la forma de onda: Scope (Gráfico = líneas mín./máx. + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de bandas de frecuencia mediante filtro Goertzel). | Ubicado en el panel de configuración plegable debajo de la forma de onda. Persistido como `WaveApplet_ViewMode`.   |
| Zoom                        | Escala el eje de amplitud; los valores más altos estiran verticalmente las señales pequeñas, haciendo que los artefactos de recorte aparezcan más pronto.                                    | Ubicado en el panel de configuración. Valor predeterminado 170% (1.7x). Persistido como `WaveApplet_ZoomPercent`.  |
| FPS                         | Controla la frecuencia con la que se repinta la forma de onda; los valores más bajos reducen la carga de CPU en sistemas lentos.                                                            | Ubicado en el panel de configuración. Persistido como `WaveApplet_RefreshRateHz`.                                  |
| Ventana (Window)            | Establece la duración de la ventana de tiempo. Pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 s hasta 10 s.                                                                   | Ubicado en el panel de configuración. Persistido como `WaveApplet_TimeWindowMs`. Valor predeterminado 1000 ms (1 s). |

### Controles del panel de configuración

El panel de configuración contiene los siguientes controles:

- **View** (cuadro combinado): selecciona el modo de visualización de la forma de onda. Opciones: Scope, Envelope, History, Bands. Persistido como `WaveApplet_ViewMode`.
- **Zoom** (control deslizante): escalado de amplitud de 1.0x a 6.0x. Valor predeterminado 1.7x (170%). Persistido como `WaveApplet_ZoomPercent`.
- **FPS** (control deslizante): frecuencia de actualización de 5 a 30 Hz. Valor predeterminado 24 Hz. Persistido como `WaveApplet_RefreshRateHz`.
- **Window** (control deslizante): duración de la ventana de tiempo. Pasos: 240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s. Valor predeterminado 1 s. Persistido como `WaveApplet_TimeWindowMs`.

En el lanzamiento inicial después de actualizar desde una versión que usaba `WaveApplet_TimeWindowSec`, su configuración de ventana anterior se migra al paso disponible más cercano en el nuevo sistema de pasos discretos.

## Indicadores

- **Tono de dirección**: la pantalla usa un tono frío para RX y un tono cálido para TX, de modo que la ruta de audio activa sea inequívoca sin leer la etiqueta del encabezado.
- **Resalte de recorte**: cualquier columna de píxeles que contenga muestras en o por encima del umbral de recorte se resalta en rojo en los bordes superior e inferior del gráfico. También aparece un contador **CLIP** en el encabezado, en negrita roja, que muestra la cantidad de muestras recortadas en la ventana actual.
- **Insignia PAUSED**: se muestra en el pie de página cuando la pantalla está congelada en una captura. Sin insignia significa que la pantalla está en vivo.
- **Marcador de posición sin audio**: si no han llegado muestras en el último segundo, o si el búfer de la pantalla está vacío, aparece un mensaje de marcador de posición que reemplaza la traza vacía.

## Consejos

- El color de la forma de onda y el ancho de línea siguen la configuración de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` utilizada en otras partes de AetherSDR. El rango válido de ancho de línea es de 1.0 a 3.0 px; el valor predeterminado es 2.0.
- Las líneas de cuadrícula se pueden suprimir mediante `DisplayShowGrid`. Cuando está habilitado, la pantalla dibuja líneas de cuadrícula mayores y menores detrás de la traza.
- Un clic para pausar es particularmente útil para capturar un transitorio: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada y luego haga clic de nuevo para reanudar.
- Haga doble clic en la pantalla para abrir o cerrar el panel de configuración. Para borrar el búfer de forma de onda, use el método WaveformWidget::clear() o reconéctese al motor de audio.
- El control deslizante de ventana solo proporciona pasos discretos; no permite el desplazamiento libre a través de valores de milisegundos. Use el paso más cercano que capture el intervalo de tiempo que necesita.

## Relacionado

- [Use the waveform display to monitor TX or RX audio](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pause and clear the waveform display](pause-and-clear-the-waveform-display.md)
