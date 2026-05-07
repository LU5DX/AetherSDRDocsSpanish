# Resumen del applet Waveform

El applet Waveform es un osciloscopio de audio que muestra la forma de onda en el dominio del tiempo de la ruta de audio activa de RX o TX. Úselo para detectar recortes, caídas y problemas de nivel de audio de un vistazo, sin necesidad de un medidor externo.

## Cómo funciona

El applet renderiza una ventana de tiempo desplazable de 100 ms de audio mono. La pantalla se alimenta continuamente con muestras del motor de audio. Cada columna de píxeles muestra la envolvente mín/máx de las muestras que caen dentro de ella, con trazas separadas de envolvente de pico y RMS superpuestas.

La línea de encabezado muestra la dirección actual (RX o TX), el nivel RMS en dBFS y el nivel de pico en dBFS. El pie de página muestra la frecuencia de muestreo, la duración de la ventana y el tiempo por división.

Dos búferes circulares separados (uno para RX y otro para TX) se ejecutan en paralelo. La pantalla dibuja desde el búfer que coincida con el estado de transmisión actual. Cuando cambia de recepción a transmisión, el tinte cambia y la pantalla comienza inmediatamente a dibujar desde el búfer de TX.

Para abrir o cerrar el applet, haga clic en el botón de la bandeja **WAVE** en la fila 1 de la barra lateral derecha. El applet está activado por defecto y se inserta inmediatamente después del botón EQ en la primera ejecución después de actualizar a v0.9.1.

El applet ya no impone una altura fija; se redimensiona verticalmente con el diseño.

## Qué hace cada control

| Control                 | Comportamiento                                                                                                                                                                                          | Notas                                                                                                                     |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Pantalla de forma de onda | Renderiza la envolvente mín/máx por columna de píxeles con trazas de envolvente de pico y RMS sobre una ventana fija de 100 ms.                                                                          | Sin clave de ajuste persistente.                                                                                          |
| Un clic en la pantalla | Alterna entre activo y pausado. Mientras está pausado, se mantiene una instantánea del búfer hasta que haga clic de nuevo.                                                                              | Aparece una insignia **PAUSED** en el pie de página. El estado predeterminado es activo.                                  |
| Doble clic en la pantalla | Alterna el panel de configuración abierto o cerrado.                                                                                                                                                   | No borra el búfer. Para restablecer la pantalla, use el slot WaveformWidget::clear() o reconéctese.                      |
| Vista                    | Selecciona el modo de visualización de la forma de onda: Scope (Gráfico = líneas mín/máx + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de banda de frecuencia mediante filtro Goertzel). | Ubicado en el panel de configuración colapsable debajo de la forma de onda. Se persiste como 'Graph', 'Envelope', 'History' o 'Bands'. |
| Zoom                     | Escala el eje de amplitud; los valores más altos estiran verticalmente las señales pequeñas, haciendo que los artefactos de recorte aparezcan antes.                                                      | Ubicado en el panel de configuración. Valor predeterminado 170% (1,7x).                                                   |
| FPS                      | Controla la frecuencia con la que se vuelve a dibujar la forma de onda; los valores más bajos reducen la carga de la CPU en sistemas lentos.                                                            | Ubicado en el panel de configuración.                                                                                     |

## Indicadores

- **Tinte de dirección** — La pantalla usa un tinte frío para RX y un tinte cálido para TX, de modo que la ruta de audio activa sea inequívoca sin leer la etiqueta del encabezado.
- **Resaltado de recorte** — Cualquier columna de píxeles que contenga muestras en o por encima del umbral de recorte se resalta en rojo en los bordes superior e inferior del gráfico. También aparece un contador **CLIP** en el encabezado, en negrita roja, que muestra el número de muestras recortadas en la ventana actual.
- **Insignia PAUSED** — Se muestra en el pie de página cuando la pantalla está congelada en una instantánea. Sin insignia significa que la pantalla está activa.
- **Marcador de posición sin audio** — Si no han llegado muestras en el último segundo, o el búfer de la pantalla está vacío, un mensaje de marcador de posición reemplaza la traza vacía.

## Consejos

- El color de la forma de onda y el grosor de la línea siguen los ajustes de pantalla `DisplayFftFillColor` y `DisplayFftLineWidth` utilizados en otras partes de AetherSDR. El rango válido de grosor de línea es de 1.0 a 3.0 px; el valor predeterminado es 2.0.
- Las líneas de cuadrícula se pueden suprimir mediante `DisplayShowGrid`. Cuando está habilitado, la pantalla dibuja líneas de cuadrícula principales y secundarias detrás de la traza.
- Un solo clic para pausar es particularmente útil para capturar un transitorio: haga clic inmediatamente después del evento, inspeccione la forma de onda congelada y luego haga clic de nuevo para reanudar.
- El doble clic en la pantalla alterna el panel de configuración. Para borrar el búfer de la forma de onda, use el slot WaveformWidget::clear() o reconéctese al motor de audio.

## Relacionados

- [Use the waveform display to monitor TX or RX audio](use-the-waveform-display-to-monitor-tx-or-rx-audio.md)
- [Pause and clear the waveform display](pause-and-clear-the-waveform-display.md)
