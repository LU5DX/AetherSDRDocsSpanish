# Ajustar la ganancia AF y el paneo desde el panel VFO

Use la pestaña **Audio** del panel VFO para establecer el nivel de salida de audio y la posición de paneo estéreo de cualquier slice de recepción de forma independiente a los demás slices.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El panel VFO del slice objetivo debe estar abierto. Si está contraído a una barra de solo frecuencia, haga clic en cualquier parte de la barra contraída para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora del VFO en la pantalla del espectro correspondiente al slice que desea ajustar. El panel VFO se abre anclado a la bandera.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Para establecer el nivel de salida de audio, arrastre el **AF Gain slider** hacia la izquierda o la derecha. El valor predeterminado es 100; el rango válido es 0–100.
4. Para establecer la posición estéreo, arrastre el **Pan slider** hacia la izquierda o la derecha. El valor predeterminado es 50 (centro); el rango válido es 0–100. Un valor inferior a 50 desplaza el audio hacia el canal izquierdo; superior a 50, hacia el derecho.

## Qué hace cada control

| Control | Predeterminado | Rango | Comportamiento |
|---|---|---|---|
| AF Gain slider (pestaña Audio) | 100 | 0–100 | Establece el nivel de salida de audio para este slice. No se persiste — refleja el estado en vivo del radio. |
| Pan slider (pestaña Audio) | 50 | 0–100 | Establece el paneo estéreo izquierdo/derecho para este slice. 50 = centro. |

## Consejos

- Hacer doble clic en cualquiera de los sliders lo restablece a su valor predeterminado: 100 para AF Gain y 50 para Pan.
- La ganancia AF es por slice. Ajustar un slice no afecta a ningún otro slice.
- Para silenciar un slice sin mover el **AF Gain slider**, use el **Mute button** de la pestaña Audio. El silenciamiento no modifica el valor de ganancia almacenado.

## Relacionados

- [Silenciar el audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Activar el squelch desde el panel VFO](enable-squelch-from-the-vfo-panel.md)
- [Contraer el panel VFO a la vista de solo frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
- [Descripción general del panel VFO](overview.md)
