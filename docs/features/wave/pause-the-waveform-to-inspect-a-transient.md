# Pausar la forma de onda para inspeccionar un transitorio

Al hacer clic una vez en la pantalla de forma de onda, se congela una instantánea del búfer de audio actual para que pueda examinar un transitorio, un evento de recorte o una caída de señal sin que la traza continúe desplazándose.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para abrirlo.
- Debe fluir audio (RX o TX) para que haya algo que valga la pena congelar. Si no ha llegado ninguna muestra en 1 segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza.
  - Para audio de RX, el marcador de posición muestra "no RX audio".
  - Para audio de TX, el marcador de posición muestra "no TX audio".

## Pasos

1. Observe la pantalla de forma de onda en busca del transitorio que desea examinar.
2. Haga clic una vez en cualquier lugar de la pantalla de forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparece una insignia **PAUSED** en el pie de la pantalla de forma de onda.
4. Examine la traza congelada. El encabezado continúa mostrando la dirección RX/TX, los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Haga clic una vez en la pantalla de forma de onda nuevamente para reanudar las actualizaciones en vivo. La insignia **PAUSED** desaparece.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| Clic en la pantalla | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la pantalla en vivo en el segundo clic. El intervalo de discriminación de clic se lee de Radio Setup en el momento del clic, por lo que los cambios en ese ajuste surten efecto de inmediato sin necesidad de reiniciar la aplicación. | En vivo | En vivo / En pausa | — |
| Vista | Selecciona el modo de visualización que se muestra mientras está en pausa. | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` |
| Zoom | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas, lo que facilita ver transitorios sutiles mientras está en pausa. | 1.7x (170) | 100–600 (1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| FPS | Controla la velocidad de repintado mientras está en vivo. No tiene efecto mientras está en pausa. | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` |
| Estado del panel de ajustes | Persiste el estado expandido/contraído del panel de ajustes al reiniciar la aplicación. Alterne haciendo doble clic en la pantalla de forma de onda o abriendo/cerrando el panel manualmente. | Expandido (True) | Expandido / Contraído | `WaveApplet_DrawerExpanded` |

## Consejos

- El clic se diferencia de un doble clic mediante un intervalo corto. Si la pantalla no se congela en su primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El intervalo de discriminación de clic se lee del diálogo **Radio Setup** en el momento en que hace clic. Si ajusta ese parámetro, se aplica de inmediato sin reiniciar AetherSDR.
- El doble clic abre o cierra el panel de ajustes en lugar de pausar. Si abre accidentalmente el panel, haga doble clic nuevamente para cerrarlo, luego haga un solo clic para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta TX está teñida de manera diferente a la ruta RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado.
- Si no han llegado muestras de audio RX en 1 segundo, el mensaje de marcador de posición muestra "no RX audio". Para audio TX, el marcador de posición muestra "no TX audio".
- El estado del panel de ajustes (expandido o contraído) se guarda al cerrarlo y se restaura la próxima vez que abra el applet de forma de onda.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de hacer clic una vez en el área de la forma de onda en sí, no en el panel de ajustes debajo de ella. Un segundo clic rápido reanudará la pantalla inmediatamente; haga clic una vez y pause antes de volver a hacer clic.
- **Aparece la insignia PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento de hacer clic. Esto ocurre cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca el audio y luego haga clic nuevamente.
- **La pantalla se reanuda por sí sola** — La pausa solo congela la pantalla visual; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.
- **El mensaje de marcador de posición muestra "no RX audio"** — Esto indica que no se han recibido muestras de audio RX. Habilite PC Audio en la configuración de la radio para recibir audio de la radio.
- **El panel de ajustes no recuerda su estado** — El estado del panel se guarda al cerrarlo. Si AetherSDR se bloquea antes de que se complete el guardado, el estado puede volver a expandido en el próximo inicio.
- **El applet de forma de onda está oculto y no responde** — El applet puede estar en modo lean, que deshabilita completamente el osciloscopio. Haga clic en el botón WAVE de la bandeja para mostrar el applet y habilitarlo. En modo lean, la transmisión del osciloscopio se descarta y el applet se oculta para conservar recursos.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
