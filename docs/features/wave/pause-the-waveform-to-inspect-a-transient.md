# Pausar la forma de onda para inspeccionar un transitorio

Al hacer clic una vez en la pantalla de la forma de onda se congela una instantánea del búfer de audio actual para que pueda examinar un transitorio, un evento de recorte o una interrupción sin que la traza siga desplazándose.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para abrirlo.
- Debe haber flujo de audio (RX o TX) para que haya algo que valga la pena congelar. Si no llegan muestras en 1 segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza.
  - Para audio de RX, el marcador de posición dice "Enable PC Audio".
  - Para audio de TX, el marcador de posición dice "no TX audio".

## Pasos

1. Observe la pantalla de la forma de onda en busca del transitorio que desea examinar.
2. Haga clic una vez en cualquier lugar de la pantalla de la forma de onda en el momento en que aparece el evento.
3. Confirme que la pantalla está congelada: aparece una insignia **PAUSED** en el pie de la pantalla de la forma de onda.
4. Examine la traza congelada. El encabezado continúa mostrando la dirección RX/TX, los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Haga clic una vez en la pantalla de la forma de onda nuevamente para reanudar las actualizaciones en vivo. La insignia **PAUSED** desaparece.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Clic en la pantalla | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la pantalla en vivo en el segundo clic. | En vivo | En vivo / En pausa | — |
| View | Selecciona el modo de visualización que se muestra mientras está en pausa. | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` |
| Zoom | Escala el eje de amplitud. Los valores más altos estiran las señales pequeñas verticalmente, lo que facilita ver transitorios sutiles mientras está en pausa. | 1.7x (170) | 100–600 (1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| FPS | Controla la velocidad de repintado mientras está en vivo. No tiene efecto mientras está en pausa. | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` |

## Consejos

- El clic se distingue de un doble clic mediante un intervalo breve. Si la pantalla no se congela con su primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El doble clic abre o cierra el cajón de configuración en lugar de pausar. Si abre accidentalmente el cajón, haga doble clic nuevamente para cerrarlo y luego haga clic una vez para pausar.
- Aumentar Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta TX se tiñe de manera diferente a la ruta RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado.
- Si no llegan muestras de audio de RX en 1 segundo, el mensaje de marcador de posición dice "Enable PC Audio" para recordarle que el audio de PC debe estar habilitado para la recepción. Para audio de TX, el marcador de posición dice "no TX audio".

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de estar haciendo clic una vez en el área de la forma de onda, no en el cajón de configuración debajo de ella. Un segundo clic rápido reanudará la pantalla inmediatamente; haga clic una vez y espere antes de volver a hacer clic.
- **Aparece la insignia PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento en que hizo clic. Esto sucede cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca el audio y luego haga clic nuevamente.
- **La pantalla se reanuda por sí sola** — La pausa solo congela la pantalla visual; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.
- **El mensaje de marcador de posición muestra "Enable PC Audio"** — Esto indica que no se han recibido muestras de audio de RX. Habilite PC Audio en la configuración de la radio para recibir audio de la radio.

## Relacionado

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
