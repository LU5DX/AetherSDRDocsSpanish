# Descripción general del applet Waveform

El applet Waveform es un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio RX o TX activa. Úselo para detectar recortes de señal (clipping), interrupciones y problemas de nivel de audio de un vistazo, sin necesidad de recurrir a un medidor externo.

## Cómo funciona

El applet renderiza una ventana temporal deslizante de 100 ms de audio mono. La pantalla recibe muestras continuamente desde el motor de audio. Cada columna de píxeles muestra la envolvente mín/máx de las muestras que caen dentro de ella, con trazas de envolvente de pico y RMS superpuestas.

La línea de encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel de pico en dBFS. El pie de página muestra la frecuencia de muestreo, la duración de la ventana y el tiempo por división.

Dos búferes circulares independientes — uno para RX y uno para TX — funcionan en paralelo. La pantalla toma datos del búfer que corresponde al estado de transmisión actual. Al cambiar de recepción a transmisión, el tono de color cambia y la pantalla comienza de inmediato a dibujar desde el búfer TX.

Para abrir o cerrar el applet, haga clic en el botón **WAVE** de la bandeja en la fila 1 de la barra lateral derecha. El applet está activado de forma predeterminada y se inserta inmediatamente después del botón EQ en el primer inicio tras actualizar a v0.9.1.

## Qué hace cada control

| Control                      | Comportamiento                                                                                                                                                                                                                              | Notas                                                                                                                                   |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| Pantalla de forma de onda    | Renderiza la envolvente mín/máx por columna de píxeles con trazas de pico y RMS sobre una ventana fija de 100 ms.                                                                                                                           | Sin clave de configuración persistida.                                                                                                  |
| Clic simple en la pantalla   | Alterna entre modo en vivo y pausado. Mientras está pausado, se retiene una instantánea del búfer hasta que haga clic de nuevo.                                                                                                              | Aparece un distintivo **PAUSED** en el pie de página. El estado predeterminado es en vivo.                                              |
| Doble clic en la pantalla    | Abre o cierra el cajón de configuración.                                                                                                                                                                                                    | No borra el búfer. Para reiniciar la pantalla, use el slot WaveformWidget::clear() o vuelva a conectar.                                 |
| View                         | Selecciona el modo de visualización de la forma de onda: Scope (Graph = líneas mín/máx + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de banda de frecuencia mediante filtro de Goertzel). | Se encuentra en el cajón de configuración desplegable debajo de la forma de onda. Se persiste como 'Graph', 'Envelope', 'History' o 'Bands'. |
| Zoom                         | Escala el eje de amplitud; los valores más altos estiran verticalmente las señales pequeñas, haciendo que los artefactos de recorte aparezcan antes.                                                                                         | Se encuentra en el cajón de configuración. Valor predeterminado: 170% (1.7x).                                                           |
| FPS                          | Controla la frecuencia de actualización de la forma de onda; los valores más bajos reducen la carga de CPU en sistemas lentos.                                                                                                               | Se encuentra en el cajón de configuración.                                                                                              |

## Indicadores

- **Tono de dirección** — La pantalla usa un tono frío para RX y un tono cálido para TX, de modo que la ruta de audio activa sea inequívoca sin necesidad de leer la etiqueta del encabezado.
- **Resaltado de recorte** — Cualquier columna de píxeles que contenga muestras en o por encima del umbral de recorte se resalta en rojo en los bordes superior e inferior del gráfico. También aparece un contador **CLIP** en el encabezado, en negrita roja, que muestra el número de muestras recortadas en la ventana actual.
- **Distintivo PAUSED** — Se muestra en el pie de página cuando la pantalla está congelada en una instantánea. Si no aparece el distintivo, la pantalla está en vivo.
- **Marcador de posición sin audio** — Si no han llegado muestras en el último segundo, o el búfer de visualización está vacío, un mensaje de marcador de posición reemplaza la traza vacía.

## Consejos

- El color de la forma de onda y el grosor de línea siguen los ajustes de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` usados en otras partes de AetherSDR. El rango válido de grosor de línea es de 1.0 a 3.0 px; el valor predeterminado es 2.0.
- Las líneas de cuadrícula se pueden ocultar mediante `DisplayShowGrid`. Cuando está habilitado, la pantalla dibuja líneas de cuadrícula mayores y menores detrás de la traza.
- El clic simple para pausar es especialmente útil para capturar un transitorio: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada y luego haga clic de nuevo para reanudar.
- El doble clic en la pantalla abre o cierra el cajón de configuración. Para borrar el búfer de la forma de onda, use el slot WaveformWidget::clear() o vuelva a conectar al motor de audio.

## Relacionados

- [Use la pantalla de forma de onda para monitorear audio TX o RX](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pause y borre la pantalla de forma de onda](pause-and-clear-the-waveform-display.md)
