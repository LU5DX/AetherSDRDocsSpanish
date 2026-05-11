# Pausar la forma de onda para inspeccionar un transitorio

Al hacer clic una vez en la visualización de la forma de onda se congela una instantánea del búfer de audio actual para que pueda examinar un transitorio, un evento de recorte o una pérdida de señal sin que la traza continúe desplazándose.

## Antes de empezar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para abrirlo.
- Debe haber audio en circulación (RX o TX) para que haya algo que valga la pena congelar. Si no llegan muestras en 1 segundo, la pantalla muestra un marcador de posición "no RX audio" o "no TX audio" en lugar de una traza.

## Pasos

1. Observe la visualización de la forma de onda en busca del transitorio que desea examinar.
2. Haga clic una vez en cualquier lugar de la visualización de la forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparece una etiqueta **PAUSED** en el pie de la visualización de la forma de onda.
4. Examine la traza congelada. El encabezado continúa mostrando la dirección RX/TX, los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Haga clic una vez en la visualización de la forma de onda de nuevo para reanudar la actualización en vivo. La etiqueta **PAUSED** desaparece.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Clic en la pantalla | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la visualización en vivo en el segundo clic. | En vivo | En vivo / En pausa | — |
| View | Selecciona el modo de visualización que se muestra mientras está en pausa. | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` |
| Zoom | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas, facilitando la visualización de transitorios sutiles mientras está en pausa. | 1.7x (170) | 100–600 (1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| FPS | Controla la velocidad de repintado mientras está en vivo. No tiene efecto mientras está en pausa. | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` |
| Window | Establece la ventana de tiempo visible en la visualización de la forma de onda. Utiliza pasos discretos: 240 ms, 480 ms, 1 s, luego incrementos de 1 segundo hasta 10 s. | 1 s | 240 ms – 10 s (12 pasos) | `WaveApplet_TimeWindowMs` |

## Consejos

- El clic se distingue de un doble clic mediante un intervalo corto. Si la pantalla no se congela con su primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El doble clic abre o cierra el cajón de configuración en lugar de pausar. Si abre el cajón accidentalmente, haga doble clic de nuevo para cerrarlo y luego haga clic una vez para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta TX tiene un tinte diferente al de la ruta RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado.
- Ajuste el control deslizante Window para mostrar períodos de tiempo más cortos (240 ms, 480 ms) para un examen detallado de transitorios rápidos, o períodos más largos (2 s – 10 s) para ver patrones de audio sostenidos. Los cambios de ventana surten efecto de inmediato y se conservan entre sesiones.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de estar haciendo clic una vez en el área de la forma de onda, no en el cajón de configuración debajo de ella. Un segundo clic rápido reanudará la pantalla inmediatamente; haga clic una vez y espere antes de volver a hacer clic.
- **Aparece la etiqueta PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento en que hizo clic. Esto ocurre cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca el audio y luego haga clic de nuevo.
- **La pantalla se reanuda por sí sola** — La pausa solo congela la visualización visual; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.
- **El control deslizante Window no responde o los cambios son impredecibles** — Si actualizó desde una versión anterior, su configuración de ventana de tiempo antigua se ha migrado automáticamente al nuevo sistema de pasos discretos. Verifique que el control deslizante Window esté configurado en uno de los 12 pasos disponibles (240 ms, 480 ms, 1 s, 2 s, 3 s, 4 s, 5 s, 6 s, 7 s, 8 s, 9 s, 10 s).

## Relacionado

- [Descripción general de Waveform](overview.md)
- [Monitorear audio TX o RX en la visualización de la forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
