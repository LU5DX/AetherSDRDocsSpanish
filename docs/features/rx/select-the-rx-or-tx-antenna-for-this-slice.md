# Seleccionar la antena RX o TX para este slice

Cada slice tiene una antena RX y una antena TX independientes. Use el applet RX Controls para cambiar cualquiera de ellas sin afectar los demás slices.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. Los controles de antena requieren una conexión activa con la radio.
- Abra el applet RX Controls. Siempre está visible en el panel de applets (barra lateral derecha). Si el panel está oculto, haga clic en el botón `RX` de la bandeja en la barra lateral derecha para mostrarlo.
- Si tiene más de un slice, seleccione el correcto usando la fila de pestañas A–H en la parte superior del applet.

## Pasos

### Cambiar la antena RX

1. Localice la etiqueta de antena azul en la fila de encabezado del applet RX Controls. Muestra la antena RX actual (por ejemplo, `ANT1`).
2. Haga clic en la etiqueta azul. Se abre un menú con todas las antenas que reporta la radio.
3. Haga clic en la antena que desea usar para recepción. Aparece una marca de verificación junto a la selección actual.

### Cambiar la antena TX

1. Localice la etiqueta de antena roja en la fila de encabezado, inmediatamente a la derecha de la etiqueta de antena RX azul. Muestra la antena TX actual (por ejemplo, `ANT1`).
2. Haga clic en la etiqueta roja. Se abre un menú con las antenas habilitadas para transmisión. Los puertos de antena cuyos nombres comienzan con `RX` no se muestran, ya que son solo de recepción.
3. Haga clic en la antena que desea usar para transmisión.

## Qué hace cada control

| Control | Color | Predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| Botón de antena RX | Etiqueta azul | ANT1 | Nombres de antena del `ant_list` de la radio | Abre un menú; al seleccionar una entrada se establece la antena RX para este slice. |
| Botón de antena TX | Etiqueta roja | ANT1 | Nombres de antena del `ant_list` de la radio, excluyendo los puertos con prefijo `RX` | Abre un menú; al seleccionar una entrada se establece la antena TX para este slice. Los puertos solo de recepción quedan filtrados. |

## Consejos

- Las selecciones de antena RX y TX son por slice. Cambiar la antena en el slice A no afecta al slice B.
- Los nombres de antena disponibles provienen del `ant_list` reportado por la radio. Si falta una antena esperada, verifique la conexión física y el firmware de la radio.
- Los puertos solo de recepción (aquellos cuyos nombres comienzan con `RX`) aparecen en el menú de antena RX, pero quedan excluidos del menú de antena TX.

## Solución de problemas

- **Una antena que espero no aparece en la lista** — La lista se obtiene del `ant_list` de la radio en el momento de la conexión. Reconéctese a la radio y verifique que el puerto de antena esté habilitado en la configuración propia de la radio.
- **Un puerto que quiero usar para TX no aparece en el menú TX** — Los puertos cuyos nombres comienzan con `RX` quedan filtrados del menú de antena TX. Estos puertos son solo de recepción a nivel de hardware y no pueden transmitir.

## Relacionados

- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
