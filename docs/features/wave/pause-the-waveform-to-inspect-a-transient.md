# Pausar la forma de onda para inspeccionar un transitorio

Un solo clic en la pantalla de la forma de onda congela una instantánea del búfer de audio actual para que pueda examinar un transitorio, un evento de recorte o una caída de señal sin que la traza continúe desplazándose.

## Antes de comenzar

- El applet Waveform debe estar visible. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para abrirlo.
- El audio debe estar fluyendo (RX o TX) para que haya algo que valga la pena congelar. Si no llegan muestras dentro de 1 segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza.
  - Para audio RX, el marcador de posición dice "no RX audio".
  - Para audio TX, el marcador de posición dice "no TX audio".

## Pasos

1. Observe la pantalla de la forma de onda en busca del transitorio que desea examinar.
2. Haga un solo clic en cualquier lugar de la pantalla de la forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparece una insignia **PAUSED** en el pie de la pantalla de la forma de onda.
4. Examine la traza congelada. El encabezado continúa mostrando la dirección RX/TX y los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Haga un solo clic nuevamente en la pantalla de la forma de onda para reanudar las actualizaciones en vivo. La insignia **PAUSED** desaparece.

## Qué hace cada control

| Control               | Comportamiento                                                                                                                                                                                                                                                        | Predeterminado                                                                                                      |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| Clic en la pantalla   | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la visualización en vivo en el segundo clic. El intervalo de discriminación de clic se lee de Radio Setup en el momento del clic, por lo que los cambios en esa configuración surten efecto de inmediato sin reiniciar la aplicación. | En vivo                                                                                                             |
| Doble clic en la pantalla | Alterna el panel de configuración abierto/cerrado (emite settingsDrawerToggleRequested). No borra el búfer — use el slot WaveformWidget::clear() o reconéctese para restablecer.                                                                                   | —                                                                                                                   |
| View                  | Selecciona el modo de visualización de la forma de onda: Scope (Graph = líneas de min/max + RMS), Envelope (área rellena de pico/RMS), History (barras de nivel horizontales), Bands (barras de bandas de frecuencia mediante filtro Goertzel).                            | Scope                                                                                                               |
| Zoom                  | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas, lo que facilita ver transitorios sutiles mientras está en pausa y hace que los artefactos de recorte aparezcan antes.                                                      | 1.7x (170)                                                                                                          |
| FPS                   | Controla la frecuencia con la que se repinta la forma de onda; los valores más bajos reducen la carga de CPU en sistemas lentos. No tiene efecto mientras está en pausa.                                                                                              | 24 Hz                                                                                                               |
| Window                | Controla la ventana de tiempo que se muestra en la pantalla de la forma de onda, en milisegundos. Los valores más grandes muestran más historial con resolución reducida.                                                                                              | 200 ms                                                                                                              |
| Estado del panel de configuración | Conserva el estado expandido/contraído del panel de configuración entre reinicios de la aplicación. Alterne haciendo doble clic en la pantalla de la forma de onda o abriendo/cerrando el panel manualmente.                                                       | Expandido (True)                                                                                                    |

## Consejos

- El clic se distingue de un doble clic mediante un intervalo corto. Si la pantalla no se congela con su primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El intervalo de discriminación de clic se lee desde el diálogo **Radio Setup** en el momento en que hace clic. Si ajusta esa configuración, se aplica de inmediato sin reiniciar AetherSDR.
- El doble clic abre o cierra el panel de configuración en lugar de pausar. Si abre el panel accidentalmente, haga doble clic nuevamente para cerrarlo y luego un solo clic para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el cuadro congelado.
- La ruta TX tiene un tinte diferente al de la ruta RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado. RX usa un tinte frío; TX usa un tinte cálido.
- Si no llegan muestras de audio RX dentro de 1 segundo, el mensaje de marcador de posición dice "no RX audio". Para audio TX, el marcador de posición dice "no TX audio".
- El estado del panel de configuración (expandido o contraído) se guarda al cerrarlo y se restaura la próxima vez que abra el applet Waveform. La clave de configuración es `WaveApplet_DrawerExpanded`.
- El botón de la bandeja WAVE ya no controla el modo lean. El applet de forma de onda siempre actualiza su pantalla cuando está visible; ocultar el applet conserva recursos de forma natural.
- El modo de vista (`WaveApplet_ViewMode`) se conserva como 'Graph', 'Envelope', 'History' o 'Bands' — la lista CSV que ve en el menú desplegable muestra Scope para Graph.
- La clave de configuración heredada `WaveApplet_TimeWindowSec` se migra a `WaveApplet_TimeWindowMs` en el primer inicio.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de hacer clic una vez en el área de la forma de onda en sí, no en el panel de configuración debajo. Un segundo clic rápido reanudará la pantalla de inmediato; haga clic una vez y pause antes de hacer clic nuevamente.
- **Aparece la insignia PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento en que hizo clic. Esto sucede cuando no ha llegado audio en el último segundo. Reanude el modo en vivo, espere a que aparezca el audio y luego haga clic nuevamente.
- **La pantalla se reanuda sola** — Pausar solo congela la visualización; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.
- **El mensaje de marcador de posición muestra "no RX audio"** — Esto indica que no se han recibido muestras de audio RX. Habilite PC Audio en la configuración de la radio para recibir audio de la radio.
- **El panel de configuración no recuerda su estado** — El estado del panel se guarda al cerrarlo. Si AetherSDR falla antes de que se complete el guardado, el estado puede revertirse a expandido en el próximo inicio.

## Relacionado

- [Resumen de la forma de onda](overview.md)
- [Monitorear audio TX o RX en la pantalla de la forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
