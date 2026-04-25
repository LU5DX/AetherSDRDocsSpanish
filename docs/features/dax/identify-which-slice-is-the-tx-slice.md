# Identificar cuál slice es el slice de TX

El applet DAX Audio muestra un indicador en vivo de asignación de TX que le indica qué slice tiene actualmente los privilegios de TX. Úselo cuando necesite confirmar qué slice maneja el flujo DAX TX antes de transmitir audio digital.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El indicador de TX requiere una conexión de radio activa.
- El applet DAX debe estar visible. Si no lo ve, haga clic en el botón DAX del panel lateral derecho para abrirlo.

## Pasos

1. Haga clic en el botón **DAX** del panel lateral derecho para abrir el applet DAX Audio.
2. Observe la fila **TX:** en la parte inferior del applet.
3. Lea el indicador de estado inmediatamente a la derecha de la etiqueta **TX:**.
   - Si un slice tiene privilegios de TX, el indicador muestra **Slice A** hasta **Slice H**, correspondiendo a la letra asignada a ese slice.
   - Si ningún slice tiene actualmente privilegios de TX, el indicador muestra **—**.

## Qué hace cada control

| Control | Descripción | Estados | Clave persistida |
|---|---|---|---|
| Indicador de asignación de TX | Muestra qué slice tiene actualmente los privilegios de TX y maneja el flujo DAX TX. Se actualiza automáticamente cuando el TX cambia entre slices. | **—** (ninguno) o **Slice A–H** | None |
| Ganancia+medidor de TX | Medidor de nivel y control deslizante de ganancia combinados para el flujo DAX TX. | 0.0–1.0 (valor predeterminado 0.5) | `DaxTxGain` |

## Consejos

- El indicador de TX se actualiza de inmediato cada vez que los privilegios de TX se transfieren a un slice diferente. No es necesario actualizar ni volver a abrir el applet.
- Las filas de RX por encima de la fila **TX:** muestran qué slice está enrutado a cada canal DAX (DAX 1 al DAX 4). Esos indicadores siguen el mismo formato **Slice A–H** o **—** y son independientes del indicador de TX.

## Relacionado

- [Ver qué slice está utilizando cada canal DAX](see-which-slice-is-currently-using-each-dax-channel.md)
- [Configurar la ganancia DAX TX](set-dax-tx-gain.md)
- [Habilitar DAX para enrutar el audio del slice a WSJT-X / FLDigi / otro software digital](enable-dax-to-route-slice-audio-to-wsjt-x-fldigi-other-digital-software.md)
- [Descripción general de DAX Audio](overview.md)
