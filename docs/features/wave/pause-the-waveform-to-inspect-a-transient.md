# Pausar la forma de onda para inspeccionar un transitorio

Al hacer un solo clic en la visualización de la forma de onda se congela una instantánea del búfer de audio actual para que pueda examinar un transitorio, un evento de recorte o una interrupción sin que la traza continúe desplazándose.

## Antes de comenzar

- El applet de forma de onda debe estar visible. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para abrirlo.
- Debe haber flujo de audio (RX o TX) para que haya algo que valga la pena congelar. Si no llegan muestras durante 1 segundo, la pantalla muestra un mensaje de marcador de posición en lugar de una traza.
  - Para audio de RX, el marcador muestra "Enable PC Audio".
  - Para audio de TX, el marcador muestra "no TX audio".

## Pasos

1. Observe la visualización de la forma de onda para detectar el transitorio que desea examinar.
2. Haga clic una vez en cualquier parte de la visualización de la forma de onda en el momento en que aparezca el evento.
3. Confirme que la pantalla está congelada: aparece una etiqueta **PAUSED** en el pie de la visualización de la forma de onda.
4. Examine la traza congelada. El encabezado continúa mostrando la dirección RX/TX, y los valores RMS dBFS y PK dBFS que se capturaron en el momento del clic.
5. Vuelva a hacer un solo clic en la visualización de la forma de onda para reanudar las actualizaciones en vivo. La etiqueta **PAUSED** desaparece.

## Función de cada control

| Control | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Clic en la pantalla | Alterna la pausa: congela una instantánea del búfer en el primer clic; reanuda la visualización en vivo en el segundo clic. El intervalo de discriminación de clic se lee desde Radio Setup en el momento del clic, por lo que los cambios en esa configuración tienen efecto inmediato sin necesidad de reiniciar la aplicación. | En Vivo | En Vivo / En Pausa | — |
| View | Selecciona el modo de visualización que se muestra mientras está en pausa. | Scope | Scope, Envelope, History, Bands | `WaveApplet_ViewMode` |
| Zoom | Escala el eje de amplitud. Los valores más altos estiran verticalmente las señales pequeñas, lo que facilita la visualización de transitorios sutiles mientras está en pausa. | 1.7x (170) | 100–600 (1.0x–6.0x) | `WaveApplet_ZoomPercent` |
| FPS | Controla la frecuencia de repintado mientras está en vivo. No tiene efecto mientras está en pausa. | 24 | 5–30 Hz | `WaveApplet_RefreshRateHz` |
| Estado del panel de configuración | Persiste el estado expandido/contraído del panel de configuración entre reinicios de la aplicación. Alterne haciendo doble clic en la visualización de la forma de onda o abriendo/cerrando el panel manualmente. | Expandido (True) | Expandido / Contraído | `WaveApplet_DrawerExpanded` |

## Consejos

- El clic se distingue de un doble clic mediante un intervalo corto. Si la pantalla no se congela en su primer clic, haga clic una vez y espere en lugar de hacer clic rápidamente.
- El intervalo de discriminación de clic se lee del cuadro de diálogo **Radio Setup** en el momento en que hace clic. Si ajusta esa configuración, se aplica inmediatamente sin necesidad de reiniciar AetherSDR.
- El doble clic abre o cierra el panel de configuración en lugar de pausar. Si abre el panel accidentalmente, vuelva a hacer doble clic para cerrarlo y luego un solo clic para pausar.
- Aumentar el Zoom antes de pausar puede hacer que los transitorios de bajo nivel sean más visibles en el fotograma congelado.
- La ruta de TX está teñida de manera diferente a la ruta de RX, por lo que puede confirmar qué dirección de audio representa la instantánea congelada sin leer el encabezado.
- Si no llegan muestras de audio de RX durante 1 segundo, el mensaje de marcador muestra "Enable PC Audio" para recordarle que el audio de PC debe estar habilitado para la recepción. Para audio de TX, el marcador muestra "no TX audio".
- El estado del panel de configuración (expandido o contraído) se guarda cuando lo cierra y se restaura la próxima vez que abra el applet de forma de onda.

## Solución de problemas

- **El clic no pausa la pantalla** — Asegúrese de estar haciendo clic una vez en el área de la forma de onda en sí, no en el panel de configuración debajo de ella. Un segundo clic rápido reanudará la pantalla inmediatamente; haga clic una vez y pause antes de volver a hacer clic.
- **Aparece la etiqueta PAUSED pero la traza está en blanco** — El búfer estaba vacío en el momento en que hizo clic. Esto ocurre cuando no ha llegado audio durante el último segundo. Reanude el modo en vivo, espere a que aparezca audio y luego vuelva a hacer clic.
- **La pantalla se reanuda por sí sola** — Pausar solo congela la visualización visual; una reconexión o un reinicio del motor de audio borra el búfer y restaura la vista en vivo.
- **El mensaje de marcador muestra "Enable PC Audio"** — Esto indica que no se han recibido muestras de audio de RX. Habilite PC Audio en la configuración de la radio para recibir audio de la radio.
- **El panel de configuración no recuerda su estado** — El estado del panel se guarda cuando lo cierra. Si AetherSDR se bloquea antes de que se complete el guardado, el estado puede volver a expandido en el próximo inicio.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la visualización de la forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
- [Cambiar el modo de vista de la forma de onda (Scope, Envelope, History, Bands)](switch-the-waveform-view-mode-scope-envelope-history-bands.md)
