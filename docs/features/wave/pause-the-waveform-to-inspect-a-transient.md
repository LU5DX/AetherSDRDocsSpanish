# Pausar la forma de onda para inspeccionar un transitorio

Al hacer clic una vez en la pantalla de forma de onda se congela una instantánea del búfer de audio actual para que pueda examinar un transitorio, un evento de recorte o una pérdida de señal sin que la traza siga desplazándose.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para abrirlo.
- Debe haber flujo de audio (RX o TX) para que haya algo que valga la pena congelar. Si no llegan muestras en un segundo, la pantalla muestra un marcador de posición "sin audio de RX" o "sin audio de TX" en lugar de una traza.

## Pasos

1. Observe la pantalla de forma de onda en busca del transitorio que desea examinar.
2. Haga clic una vez en cualquier lugar de la pantalla de forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparece una insignia **PAUSED** en el pie de la pantalla de forma de onda.
4. Examine la traza congelada. El encabezado sigue mostrando la dirección RX/TX, los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Vuelva a hacer clic una vez en la pantalla de forma de onda para reanudar la actualización en vivo. La insignia **PAUSED** desaparece.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Clic en la pantalla | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la pantalla en vivo en el segundo clic. | En vivo | En vivo / En pausa | — |
| View | Selecciona el modo de visualización que se muestra mientras está en pausa. | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` |
| Zoom | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas, facilitando la visualización de transitorios sutiles mientras está en pausa. | 1.7x (170) | 100–600 (1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| FPS | Controla la frecuencia de repintado mientras está en vivo. No tiene efecto mientras está en pausa. | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` |

## Consejos

- El clic se distingue de un doble clic mediante un intervalo corto. Si la pantalla no se congela en su primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El doble clic abre o cierra el cajón de configuración en lugar de pausar. Si abre el cajón accidentalmente, vuelva a hacer doble clic para cerrarlo y luego haga clic una vez para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta TX tiene un tono diferente al de la ruta RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de estar haciendo clic una vez en el área de la forma de onda en sí, no en el cajón de configuración debajo de ella. Un segundo clic rápido reanudará la pantalla inmediatamente; haga clic una vez y pause antes de volver a hacer clic.
- **La insignia PAUSED aparece pero la traza está en blanco** — El búfer estaba vacío en el momento en que hizo clic. Esto sucede cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca el audio y luego vuelva a hacer clic.
- **La pantalla se reanuda por sí sola** — La pausa solo congela la visualización; una reconexión o un reinicio del motor de audio vacía el búfer y restaura la vista en vivo.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
