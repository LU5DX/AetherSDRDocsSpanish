# Activar el squelch desde el panel VFO

El squelch silencia el audio de un slice cuando la señal recibida cae por debajo de un umbral establecido. Úselo para eliminar el ruido de fondo en modos FM, AM o digitales cuando no hay señal presente.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El panel VFO del slice de destino debe estar abierto. Si no lo está, haga clic en la bandera marcadora del VFO en la pantalla del espectro correspondiente a ese slice.
- Si el panel VFO está contraído a la banda de solo frecuencia, haga clic una vez para expandirlo.

## Pasos

1. Abra el panel VFO haciendo clic en la bandera marcadora del VFO en la pantalla del espectro del slice que desea configurar.
2. Haga clic en la pestaña **Audio** dentro del panel VFO.
3. Haga clic en el **Squelch button** para activar el squelch. El botón se activa y el squelch se aplica al slice de inmediato.
4. Arrastre el control deslizante de squelch adyacente hacia la izquierda o la derecha para establecer el umbral. El rango válido es 0–100.

Para desactivar el squelch, haga clic en el **Squelch button** nuevamente.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Squelch button | Desactivado | Activado / Desactivado | Activa o desactiva el squelch para este slice. |
| Squelch slider | — | 0–100 | Establece el umbral del squelch. Los valores más altos requieren una señal más fuerte para abrir el squelch. |

Ni el estado del botón ni la posición del control deslizante se guardan como clave de AppSettings de AetherSDR — ambos reflejan el estado en vivo de la radio.

## Consejos

- Ajuste el control deslizante justo por encima del piso de ruido para evitar que el audio se corte con señales débiles.
- El umbral del squelch interactúa con la configuración del AGC. Si cambia el modo AGC usando el **AGC combo**, es posible que deba reajustar el control deslizante del squelch.

## Relacionado

- [Ajustar la ganancia AF y el balance desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silenciar el audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Descripción general del panel VFO](overview.md)
