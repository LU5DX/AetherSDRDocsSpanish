# Pausar la forma de onda para inspeccionar un transitorio

Al hacer clic una sola vez en la pantalla de la forma de onda se congela una instantánea del búfer de audio actual, lo que permite examinar un transitorio, un evento de recorte o una interrupción sin que la traza continúe desplazándose.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón WAVE del panel lateral derecho para abrirlo.
- El audio debe estar fluyendo (RX o TX) para que haya algo que valga la pena congelar. Si no han llegado muestras en 1 segundo, la pantalla mostrará un marcador de posición "no RX audio" o "no TX audio" en lugar de una traza.

## Pasos

1. Observe la pantalla de la forma de onda esperando el transitorio que desea examinar.
2. Haga clic una sola vez en cualquier parte de la pantalla de la forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparecerá un indicador **PAUSED** en el pie de la pantalla de la forma de onda.
4. Examine la traza congelada. El encabezado sigue mostrando la dirección RX/TX y los valores RMS dBFS y PK dBFS que fueron capturados en el momento del clic.
5. Haga clic una sola vez nuevamente sobre la pantalla de la forma de onda para reanudar las actualizaciones en vivo. El indicador **PAUSED** desaparece.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Clic en la pantalla | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la visualización en vivo en el segundo clic. | Live | Live / Paused | — |
| View | Selecciona el modo de visualización que se muestra durante la pausa. | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` |
| Zoom | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales débiles, facilitando la visualización de transitorios sutiles durante la pausa. | 1.7x (170) | 100–600 (1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| FPS | Controla la tasa de refresco mientras está en vivo. No tiene efecto durante la pausa. | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` |

## Consejos

- El clic se distingue de un doble clic mediante un intervalo breve. Si la pantalla no se congela con el primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El doble clic abre o cierra el cajón de configuraciones en lugar de pausar. Si abre el cajón accidentalmente, haga doble clic nuevamente para cerrarlo y luego haga un solo clic para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta TX tiene un tinte diferente al de la ruta RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin necesidad de leer el encabezado.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de hacer clic una sola vez sobre el área de la forma de onda y no sobre el cajón de configuraciones que está debajo. Un segundo clic rápido reanudará la pantalla de inmediato; haga clic una vez y espere antes de volver a hacer clic.
- **Aparece el indicador PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento del clic. Esto ocurre cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca audio y luego haga clic nuevamente.
- **La pantalla se reanuda por sí sola** — La pausa solo congela la visualización; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.

## Relacionados

- [Descripción general de Waveform](overview.md)
- [Monitorear audio TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Cambiar el modo de visualización de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
