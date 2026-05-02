# Ajustar la tasa de refresco de la forma de onda para reducir la carga de CPU

El applet Waveform se repinta a un máximo de 30 fotogramas por segundo de forma predeterminada. En sistemas más lentos, reducir la tasa de fotogramas disminuye el uso de CPU sin afectar los datos de audio que se están monitoreando.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón WAVE de la bandeja en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la pantalla de la forma de onda, haga doble clic en la pantalla para abrir el cajón.

## Pasos

1. Haga doble clic en la pantalla de la forma de onda para abrir el cajón de configuración.
2. Localice la fila FPS en la parte inferior del cajón.
3. Arrastre el control deslizante FPS hacia la izquierda para disminuir la tasa de fotogramas o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del control deslizante en el formato `N fps`.
4. Suelte el control deslizante. La nueva tasa entra en vigor de inmediato y se guarda automáticamente en `WaveApplet_RefreshRateHz`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| FPS | 24 Hz | 5–30 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la frecuencia con la que se repinta la forma de onda. Los valores más altos producen un movimiento más fluido. Esta configuración no tiene efecto sobre la captura de audio ni sobre la precisión de los niveles.

## Consejos

- Un valor de 5–10 fps es suficiente para monitorear niveles promedio y detectar saturación (clipping). Use valores más altos solo cuando necesite rastrear transitorios rápidos visualmente.
- El control deslizante FPS usa un paso simple de 5 y un paso de página de 10, por lo que al presionar las teclas de flecha o Page Up/Page Down sobre el control deslizante, este se desplaza en esos incrementos.
- Reducir el FPS no afecta los demás ajustes del cajón. El modo de vista (`WaveApplet_ViewMode`) y el zoom (`WaveApplet_ZoomPercent`) permanecen independientes.

## Temas relacionados

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio TX o RX en la pantalla de forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
