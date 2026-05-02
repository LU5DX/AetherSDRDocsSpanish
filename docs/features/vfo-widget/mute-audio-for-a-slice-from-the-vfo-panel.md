# Silenciar el audio de un slice desde el panel VFO

Silencie la salida de audio de un slice individual sin modificar su ajuste de AF Gain. Use esta función cuando desee suprimir un slice temporalmente y restaurar su volumen anterior con un solo clic.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del slice de destino debe estar abierto. Si está colapsado en una barra de solo frecuencia, haga clic en cualquier parte de él para expandirlo primero.

## Pasos

1. Haga clic en la bandera marcadora del VFO en la pantalla del espectro correspondiente al slice que desea silenciar. El panel VFO se abre anclado al marcador.
2. Haga clic en **Audio** para seleccionar la pestaña Audio dentro del panel VFO.
3. Haga clic en **Mute**. El botón se activa y la salida de audio del slice se detiene. El valor del control deslizante AF Gain no cambia.
4. Para restaurar el audio, haga clic en **Mute** nuevamente. El botón se desactiva y el audio se reanuda en el nivel de AF Gain anterior.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| Botón Mute (pestaña Audio) | Botón de alternancia | Off | Silencia la salida de audio de este slice sin modificar el ajuste de AF Gain. Haga clic nuevamente para desactivar el silencio. |
| Control deslizante AF Gain (pestaña Audio) | Deslizador | 100 | Establece el nivel de salida de audio de este slice (0–100). No se ve afectado por Mute. |

## Consejos

- Silenciar un slice no restablece el control deslizante AF Gain. Al desactivar el silencio, el audio regresa al mismo nivel que tenía antes.
- Si desea silenciar un slice de forma permanente en lugar de temporal, arrastre el control deslizante AF Gain hasta 0.

## Relacionados

- [Ajustar AF Gain y panorámica desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Activar el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Colapsar el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
