# Descripción general del applet de forma de onda

El applet de forma de onda es un osciloscopio de audio que muestra la señal en el dominio del tiempo correspondiente a la ruta de audio RX o TX activa. Úselo para detectar saturación, interrupciones y problemas de nivel de audio de un vistazo, sin necesidad de recurrir a un medidor externo.

## Cómo funciona

El applet representa una ventana temporal deslizante de 100 ms de audio mono. La pantalla recibe muestras de forma continua desde el motor de audio. Cada columna de píxeles muestra la envolvente mínima/máxima de las muestras que caen dentro de ella, con trazos de envolvente de pico y RMS superpuestos.

La línea de encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel de pico en dBFS. El pie de página muestra la frecuencia de muestreo, la duración de la ventana y el tiempo por división.

Dos búferes circulares independientes —uno para RX y otro para TX— funcionan en paralelo. La pantalla toma datos del búfer que corresponde al estado de transmisión actual. Al cambiar de recepción a transmisión, el tinte cambia y la pantalla comienza a mostrar inmediatamente el búfer TX.

Para abrir o cerrar el applet, haga clic en el botón de bandeja **WAVE** en la fila 1 de la barra lateral derecha. El applet está activado de forma predeterminada y se inserta inmediatamente después del botón EQ en el primer inicio tras actualizar a v0.9.1.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Pantalla de forma de onda | Representa la envolvente mínima/máxima por columna de píxeles con trazos de envolvente de pico y RMS sobre una ventana fija de 100 ms. | Sin clave de configuración persistente. |
| Clic simple en la pantalla | Alterna entre modo en vivo y en pausa. Durante la pausa, se conserva una instantánea del búfer hasta que haga clic de nuevo. | En el pie de página aparece un indicador **PAUSED**. El estado predeterminado es en vivo. |
| Doble clic en la pantalla | Borra el búfer circular de la dirección activa (RX o TX) y restablece la pantalla a vacío. | No afecta al búfer de la dirección opuesta. |

## Indicadores

- **Tinte de dirección** — La pantalla usa un tinte frío para RX y un tinte cálido para TX, de modo que la ruta de audio activa sea inequívoca sin necesidad de leer la etiqueta del encabezado.
- **Resaltado de saturación** — Cualquier columna de píxeles que contenga muestras en el umbral de saturación o por encima de él se resalta en rojo en los bordes superior e inferior del gráfico. En el encabezado también aparece un contador **CLIP** en negrita roja, que indica el número de muestras saturadas en la ventana actual.
- **Indicador PAUSED** — Se muestra en el pie de página cuando la pantalla está congelada en una instantánea. Si no aparece ningún indicador, la pantalla está en modo en vivo.
- **Mensaje de sustitución sin audio** — Si no han llegado muestras en el último segundo o el búfer de pantalla está vacío, un mensaje de sustitución reemplaza el trazo vacío.

## Consejos

- El color de la forma de onda y el grosor de línea siguen los ajustes de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` utilizados en otras partes de AetherSDR. El rango válido de grosor de línea es de 1.0 a 3.0 px; el valor predeterminado es 2.0.
- Las líneas de cuadrícula pueden ocultarse mediante `DisplayShowGrid`. Cuando está habilitada, la pantalla dibuja líneas de cuadrícula principales y secundarias detrás del trazo.
- El clic simple para pausar es especialmente útil para capturar transitorios: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada y luego haga clic de nuevo para reanudar.
- El doble clic solo borra el búfer de la dirección activa en ese momento. El búfer de la dirección opuesta se conserva.

## Relacionados

- [Usar la pantalla de forma de onda para supervisar el audio TX o RX](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pausar y borrar la pantalla de forma de onda](pause-and-clear-the-waveform-display.md)
