# Identificar cuál slice es el slice de TX

El applet DAX Audio muestra un indicador de asignación de TX que permite saber de un vistazo qué slice (canal de recepción/transmisión) tiene actualmente los privilegios de TX. Úselo cuando necesite confirmar que el slice correcto está controlando el flujo DAX TX antes de transmitir desde un software de modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El indicador de TX solo se muestra cuando hay una conexión de radio activa.
- El applet DAX Audio debe estar visible. Si no lo está, haga clic en el botón DAX del panel lateral derecho para abrirlo.

## Pasos

1. Haga clic en el botón DAX del panel lateral derecho para abrir el applet DAX Audio.
2. Busque la fila etiquetada **TX:** cerca de la parte inferior del applet.
3. Lea el indicador a la derecha de la etiqueta **TX:**. Muestra `—` (ningún slice de TX asignado) o `Slice A` hasta `Slice H` (el slice que tiene actualmente los privilegios de TX).

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Notas |
|---|---|---|---|
| Indicador de asignación de TX | Muestra qué slice tiene actualmente los privilegios de TX. Se actualiza automáticamente cuando el TX cambia entre slices. | `—` | Solo visualización; no es configurable aquí. |
| Medidor y ganancia de TX | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. Arrastre para ajustar. | 0.5 (rango 0.0–1.0) | Se guarda como `DaxTxGain`. |

## Consejos

- El indicador de TX se actualiza automáticamente cada vez que el TX pasa a un slice diferente — no es necesario actualizar ni volver a abrir el applet.
- Si el indicador muestra `—` y se espera que un slice esté transmitiendo, verifique que el radio tenga un slice activo con TX habilitado.
- Las filas de RX ubicadas sobre la fila de TX tienen su propio indicador de asignación de slice que muestra `Slice A`–`Slice H` o `—`. Compárelas con la fila de TX para comprender el panorama completo del enrutamiento.

## Solución de problemas

- **El indicador de TX muestra `—` aunque hay un slice activo** — Es posible que la conexión con el radio no esté completamente establecida, o que ningún slice tenga actualmente los privilegios de TX. Verifique el estado de la conexión y asegúrese de que al menos un slice esté configurado para TX en el radio.

## Temas relacionados

- [Ver qué slice está usando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Ajustar la ganancia DAX TX](set-dax-tx-gain.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software de modos digitales](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Descripción general de DAX Audio](overview.md)
