# Pausar la forma de onda para inspeccionar un transitorio

Un solo clic en la pantalla de forma de onda congela una instantánea del búfer de audio actual, permitiéndole examinar un transitorio, un evento de recorte o una pérdida de señal sin que la traza continúe desplazándose.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón de bandeja WAVE en la barra lateral derecha para abrirlo.
- Debe haber flujo de audio (RX o TX) para que haya algo que valga la pena congelar. Si no llegan muestras en 1 segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza.
  - Para audio RX, el marcador indica "no RX audio".
  - Para audio TX, el marcador indica "no TX audio".

## Pasos

1. Observe la pantalla de forma de onda en busca del transitorio que desea examinar.
2. Haga un solo clic en cualquier lugar de la pantalla de forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparece una insignia **PAUSED** en el pie de la pantalla de forma de onda.
4. Examine la traza congelada. El encabezado continúa mostrando la dirección RX/TX, los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Vuelva a hacer un solo clic en la pantalla de forma de onda para reanudar las actualizaciones en vivo. La insignia **PAUSED** desaparece.

## Qué hace cada control

| Control               | Comportamiento                                                                                                                                                                                                                                                  | Valor predeterminado                                                                                                   |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| Clic en la pantalla   | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la visualización en vivo en el segundo clic. El intervalo de discriminación del clic se lee de Configuración de radio en el momento del clic, por lo que los cambios en esa configuración surten efecto de inmediato sin reiniciar la aplicación. | En vivo                                                                                                               |
| Vista                 | Selecciona el modo de visualización que se muestra mientras está en pausa.                                                                                                                                                                                      | Scope                                                                                                                 |
| Zoom                  | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas, lo que facilita la visualización de transitorios sutiles mientras está en pausa.                                                                                   | 1.7x (170)                                                                                                            |
| FPS                   | Controla la velocidad de repintado en modo en vivo. No tiene efecto mientras está en pausa.                                                                                                                                                                    | 25                                                                                                                    |
| Estado del panel de configuración | Conserva el estado expandido/contraído del panel de configuración al reiniciar la aplicación. Alterne haciendo doble clic en la pantalla de forma de onda o abriendo/cerrando el panel manualmente.                                                                | Expandido (Verdadero)                                                                                                 |
| Ventana               | Controla la ventana de tiempo que se muestra en la pantalla de forma de onda, en milisegundos. Los valores más grandes muestran más historial con resolución reducida.                                                                                          | Se encuentra en el panel de configuración. La clave heredada WaveApplet_TimeWindowSec se migró a WaveApplet_TimeWindowMs en el primer inicio. |

## Consejos

- El clic se distingue de un doble clic por un intervalo breve. Si la pantalla no se congela en su primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El intervalo de discriminación del clic se lee del cuadro de diálogo **Radio Setup** en el momento en que hace clic. Si ajusta esa configuración, se aplica de inmediato sin reiniciar AetherSDR.
- El doble clic abre o cierra el panel de configuración en lugar de pausar. Si abre el panel accidentalmente, haga doble clic nuevamente para cerrarlo y luego un solo clic para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta TX tiene un tinte diferente al de la ruta RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado.
- Si no llegan muestras de audio RX en 1 segundo, el mensaje de marcador dice "no RX audio". Para audio TX, el marcador dice "no TX audio".
- El estado del panel de configuración (expandido o contraído) se guarda al cerrarlo y se restaura la próxima vez que abra el applet de forma de onda.
- El botón de bandeja WAVE ya no controla el modo lean. El applet de forma de onda siempre actualiza su pantalla cuando está visible; ocultar el applet conserva recursos de forma natural.
- El rango del control deslizante FPS ahora se extiende hasta 60 Hz para los usuarios que desean un osciloscopio más rápido. El valor predeterminado es 25 Hz, que coincide con la tasa de actualización típica del panadapter.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de hacer clic una vez en el área de la forma de onda, no en el panel de configuración debajo de ella. Un segundo clic rápido reanudará la pantalla inmediatamente; haga clic una vez y pause antes de volver a hacer clic.
- **Aparece la insignia PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento en que hizo clic. Esto ocurre cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca el audio y luego haga clic nuevamente.
- **La pantalla se reanuda por sí sola** — Pausar solo congela la visualización; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.
- **El mensaje de marcador muestra "no RX audio"** — Esto indica que no se han recibido muestras de audio RX. Habilite PC Audio en la configuración de radio para recibir audio de la radio.
- **El panel de configuración no recuerda su estado** — El estado del panel se guarda al cerrarlo. Si AetherSDR se bloquea antes de que se complete el guardado, el estado puede revertirse a expandido en el próximo inicio.

## Relacionado

- [Waveform overview](overview.md)
- [Monitor TX or RX audio on the waveform display](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Adjust waveform amplitude zoom](adjust-waveform-amplitude-zoom.md)
- [Switch the waveform view mode (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
