# Pausar la forma de onda para inspeccionar un transitorio

Al hacer clic una vez en la pantalla de forma de onda se congela una instantánea del búfer de audio actual, lo que le permite examinar un transitorio, un evento de recorte o una pérdida de señal sin que la traza continúe desplazándose.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para abrirlo.
- Debe haber flujo de audio (RX o TX) para que haya algo que valga la pena congelar. Si no llegan muestras en 1 segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza.
  - Para audio de RX, el marcador de posición muestra "no RX audio".
  - Para audio de TX, el marcador de posición muestra "no TX audio".

## Pasos

1. Observe la pantalla de forma de onda para localizar el transitorio que desea examinar.
2. Haga clic una vez en cualquier lugar de la pantalla de forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparece una insignia **PAUSED** en el pie de la pantalla de forma de onda.
4. Examine la traza congelada. El encabezado continúa mostrando la dirección RX/TX, y los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Haga clic una vez más en la pantalla de forma de onda para reanudar las actualizaciones en vivo. La insignia **PAUSED** desaparece.

## Función de cada control

| Control | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Clic en la pantalla | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la pantalla en vivo en el segundo clic. El intervalo de discriminación de clic se lee de la configuración de radio en el momento del clic, por lo que los cambios en esa configuración surten efecto de inmediato sin necesidad de reiniciar la aplicación. | En vivo | En vivo / En pausa | — |
| Vista | Selecciona el modo de visualización que se muestra mientras está en pausa. | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` |
| Zoom | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas, lo que facilita la visualización de transitorios sutiles mientras están en pausa. | 1.7x (170) | 100–600 (1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| FPS | Controla la frecuencia de repintado mientras está en vivo. No tiene efecto mientras está en pausa. | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` |
| Estado del cajón de configuración | Persiste el estado expandido/contraído del cajón de configuración entre reinicios de la aplicación. Alterne haciendo doble clic en la pantalla de forma de onda o abriendo/cerrando el cajón manualmente. | Expandido (Verdadero) | Expandido / Contraído | `WaveApplet_DrawerExpanded` |

## Consejos

- El clic se distingue de un doble clic mediante un intervalo corto. Si la pantalla no se congela en su primer clic, haga clic una vez y espere, en lugar de hacer clic rápidamente.
- El intervalo de discriminación de clic se lee del diálogo **Radio Setup** en el momento en que hace clic. Si ajusta esa configuración, se aplica de inmediato sin reiniciar AetherSDR.
- El doble clic abre o cierra el cajón de configuración en lugar de pausar. Si abre el cajón accidentalmente, haga doble clic nuevamente para cerrarlo y luego haga clic una vez para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta de TX tiene un tinte diferente al de la ruta de RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado.
- Si no llegan muestras de audio de RX en 1 segundo, el mensaje de marcador de posición muestra "no RX audio". Para audio de TX, el marcador de posición muestra "no TX audio".
- El estado del cajón de configuración (expandido o contraído) se guarda cuando lo cierra y se restaura la próxima vez que abra el applet de forma de onda.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de hacer clic una vez en el área de la forma de onda en sí, no en el cajón de configuración debajo de ella. Un segundo clic rápido reanudará la pantalla de inmediato; haga clic una vez y espere antes de volver a hacer clic.
- **Aparece la insignia PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento en que hizo clic. Esto ocurre cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca audio y luego vuelva a hacer clic.
- **La pantalla se reanuda por sí sola** — Pausar solo congela la visualización visual; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.
- **El mensaje de marcador de posición muestra "no RX audio"** — Esto indica que no se han recibido muestras de audio de RX. Habilite PC Audio en la configuración de la radio para recibir audio de la radio.
- **El cajón de configuración no recuerda su estado** — El estado del cajón se guarda cuando lo cierra. Si AetherSDR se bloquea antes de que se complete el guardado, el estado puede revertirse a expandido en el próximo inicio.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
