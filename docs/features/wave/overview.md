# Descripción general del applet Waveform

El applet Waveform es un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio RX o TX activa. Úselo para detectar recortes, interrupciones y problemas de nivel de audio de un vistazo sin necesidad de un medidor externo.

## Cómo funciona

El applet renderiza una ventana de tiempo de 100 ms de audio mono que se desplaza. La pantalla se alimenta continuamente con muestras del motor de audio. Cada columna de píxeles muestra la envolvente min/máx de las muestras que caen dentro de ella, con trazas de envolvente de pico y RMS separadas dibujadas encima.

La línea del encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel de pico en dBFS. El pie de página muestra la frecuencia de muestreo, la duración de la ventana y el tiempo por división.

Dos búferes circulares separados —uno para RX y otro para TX— se ejecutan en paralelo. La pantalla dibuja desde el búfer que coincida con el estado de transmisión actual. Cuando cambia de recepción a transmisión, el tinte cambia y la pantalla comienza inmediatamente a dibujar desde el búfer TX.

Para abrir o cerrar el applet, haga clic en el botón de bandeja **WAVE** en la fila 1 de la barra lateral derecha. El applet está habilitado de forma predeterminada e se inserta inmediatamente después del botón EQ en la primera ejecución después de actualizar a v0.9.1.

El applet ya no aplica una altura fija; se redimensiona verticalmente con el diseño.

## Qué hace cada control

| Control                    | Comportamiento                                                                                                                                                                                   | Notas                                                                                                                   |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Pantalla de forma de onda  | Renderiza la envolvente min/máx por columna de píxeles con trazas de envolvente de pico y RMS en una ventana fija de 100 ms.                                                                   | Sin clave de configuración persistida.                                                                                  |
| Un clic en la pantalla     | Alterna entre en vivo y pausado. Mientras está pausado, se mantiene una instantánea del búfer hasta que haga clic de nuevo.                                                                     | Aparece una insignia **PAUSED** en el pie de página. El estado predeterminado es en vivo.                               |
| Doble clic en la pantalla  | Alterna el cajón de configuración abierto o cerrado.                                                                                                                                            | No borra el búfer. Para reiniciar la pantalla, use la ranura WaveformWidget::clear() o reconecte.                      |
| View                       | Selecciona el modo de visualización de la forma de onda: Scope (Graph = líneas min/máx + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontal), Bands (barras de banda de frecuencia mediante filtro Goertzel). | Ubicado en el cajón de configuración contraíble debajo de la forma de onda. Persistido como 'Graph', 'Envelope', 'History' o 'Bands'. |
| Zoom                      | Escala el eje de amplitud; valores más altos estiran señales pequeñas verticalmente, causando que los artefactos de recorte aparezcan antes.                                                    | Ubicado en el cajón de configuración. Predeterminado 170% (1,7x).                                                      |
| FPS                        | Controla con qué frecuencia se redibuja la forma de onda; valores más bajos reducen la carga de CPU en sistemas lentos.                                                                         | Ubicado en el cajón de configuración.                                                                                  |

## Indicadores

- **Tinte de dirección** — La pantalla utiliza un tinte frío para RX y un tinte cálido para TX, de modo que la ruta de audio activa es inequívoca sin leer la etiqueta del encabezado.
- **Resaltado de recorte** — Cualquier columna de píxeles que contenga muestras en o por encima del umbral de recorte se resalta en rojo en los bordes superior e inferior de la gráfica. Un recuento de **CLIP** también aparece en el encabezado, en rojo en negrita, mostrando el número de muestras recortadas en la ventana actual.
- **Insignia PAUSED** — Se muestra en el pie de página cuando la pantalla está congelada en una instantánea. Sin insignia significa que la pantalla está en vivo.
- **Marcador de posición sin audio** — Si no han llegado muestras en el último segundo o el búfer de pantalla está vacío, un mensaje de marcador de posición reemplaza la traza vacía.

## Consejos

- El color de la forma de onda y el ancho de línea siguen la configuración de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` utilizadas en otros lugares en AetherSDR. El rango de ancho de línea válido es 1,0 a 3,0 px; el predeterminado es 2,0.
- Las líneas de cuadrícula se pueden suprimir mediante `DisplayShowGrid`. Cuando está habilitado, la pantalla dibuja líneas de cuadrícula mayores y menores detrás de la traza.
- Un clic para pausar es particularmente útil para capturar un transitorio: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada y luego haga clic de nuevo para reanudar.
- Haga doble clic en la pantalla para alternar el cajón de configuración. Para borrar el búfer de forma de onda, use la ranura WaveformWidget::clear() o reconecte al motor de audio.

## Relacionado

- [Usar la pantalla de forma de onda para monitorear el audio TX o RX](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pausar y borrar la pantalla de forma de onda](pause-and-clear-the-waveform-display.md)
