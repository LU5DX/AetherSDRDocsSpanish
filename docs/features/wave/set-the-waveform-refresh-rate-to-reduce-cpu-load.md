# Cómo ajustar la frecuencia de actualización de la forma de onda para reducir la carga de la CPU

El applet Waveform se redibuja hasta 30 fotogramas por segundo de forma predeterminada. En sistemas más lentos, reducir la frecuencia de fotogramas disminuye el uso de la CPU sin afectar los datos de audio que se están monitoreando.

## Antes de comenzar

- El applet WAVE debe estar visible en el panel de applets. Si no lo está, haga clic en el botón de la bandeja WAVE en la barra lateral derecha para mostrarlo.
- El cajón de configuración debe estar abierto. Si solo ve la visualización de la forma de onda, haga doble clic en ella para abrir el cajón.

## Pasos

1. Haga doble clic en la visualización de la forma de onda para abrir el cajón de configuración.
2. Localice la fila FPS en la parte inferior del cajón.
3. Arrastre el control deslizante FPS hacia la izquierda para disminuir la frecuencia de fotogramas o hacia la derecha para aumentarla. El valor actual se muestra a la derecha del control deslizante en el formato `N fps`.
4. Suelte el control deslizante. La nueva frecuencia surte efecto de inmediato y se guarda automáticamente en `WaveApplet_RefreshRateHz`.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|
| FPS | 24 Hz | 5–30 Hz | `WaveApplet_RefreshRateHz` |

Los valores más bajos reducen la frecuencia con la que se redibuja la forma de onda. Los valores más altos proporcionan un movimiento más suave. Esta configuración no afecta la captura de audio ni la precisión del nivel.

## Consejos

- Un valor de 5–10 fps es suficiente para monitorear niveles promedio y detectar recortes. Use valores más altos solo cuando necesite rastrear visualmente transitorios rápidos.
- El control deslizante FPS utiliza un paso simple de 5 y un paso de página de 10, por lo que al presionar las teclas de flecha o Av Pág/Re Pág en el control deslizante, este se mueve en esos incrementos.
- Reducir los FPS no afecta las demás configuraciones del cajón. El modo de visualización (`WaveApplet_ViewMode`) y el zoom (`WaveApplet_ZoomPercent`) permanecen independientes.

## Relacionado

- [Descripción general de la forma de onda](overview.md)
- [Monitorear audio de TX o RX en la visualización de la forma de onda](monitor-tx-or-rx-audio-on-the-waveform-display.md)
- [Ajustar el zoom de amplitud de la forma de onda](adjust-waveform-amplitude-zoom.md)
