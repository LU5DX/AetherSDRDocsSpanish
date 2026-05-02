# Asignar un canal DAX desde el panel VFO

DAX (Digital Audio Exchange) enruta el audio recibido de un slice (canal de recepción) hacia un canal de audio con nombre en su computadora. Use este procedimiento para asignar o cambiar el canal DAX de cualquier slice directamente desde su panel VFO.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel VFO requiere una conexión activa con el radio.
- El puente de audio DAX debe estar en ejecución. Si no lo está, habilítelo mediante `Settings > Autostart DAX with AetherSDR` y reinicie AetherSDR, o inícielo manualmente.
- El panel VFO del slice de destino debe estar abierto y expandido. Si está contraído mostrando solo la tira de frecuencia, haga clic en cualquier parte de él para expandirlo.

## Pasos

1. Haga clic en la bandera marcadora VFO del display de espectro correspondiente al slice que desea configurar. El panel VFO se abre anclado a la izquierda del marcador.
2. Haga clic en la pestaña **DAX** dentro del panel VFO.
3. Haga clic en el **combo de canal DAX** y seleccione un canal de la lista desplegable.
4. Para deshabilitar el enrutamiento DAX para este slice, seleccione **Off**.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Clave de configuración persistida |
|---|---|---|---|
| Combo de canal DAX | Off | Off, 1–8 | — |

El combo de canal DAX asigna un canal de audio DAX al slice actual. Al seleccionar un canal numerado, el audio recibido del slice se enruta hacia ese canal DAX. Al seleccionar **Off** se elimina la asignación. Esta configuración refleja el estado en vivo del radio y AetherSDR no la persiste localmente.

## Consejos

- Cada canal DAX solo puede asignarse a un slice a la vez. Si asigna un canal que ya está en uso por otro slice, el radio trasladará la asignación.
- Si el panel VFO quedara recortado por el borde de la ventana, se desplaza automáticamente al lado derecho del marcador.

## Solución de problemas

- **El combo de canal DAX no tiene efecto / el audio no aparece en el sistema** — Confirme que el puente de audio DAX está en ejecución. Verifique `Settings > Autostart DAX with AetherSDR`. En sistemas macOS y PipeWire, el puente debe estar activo para que los canales DAX aparezcan como dispositivos de audio.
- **La pestaña DAX no es visible** — Es posible que el panel VFO esté contraído. Haga clic en la tira contraída para expandirlo y luego seleccione la pestaña DAX.

## Relacionado

- [Descripción general del panel VFO](overview.md)
- [Ajustar la ganancia AF y el paneo desde el panel VFO](adjust-af-gain-and-pan-from-the-vfo-panel.md)
- [Silenciar el audio de un slice desde el panel VFO](mute-audio-for-a-slice-from-the-vfo-panel.md)
- [Contraer el panel VFO a la vista solo de frecuencia](collapse-the-vfo-panel-to-frequency-only-view.md)
