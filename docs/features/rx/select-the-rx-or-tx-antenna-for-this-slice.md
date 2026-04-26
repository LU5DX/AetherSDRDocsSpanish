# Seleccionar la antena RX o TX para este slice

El applet RX Controls le permite elegir qué puerto de antena utiliza el radio para recibir y transmitir en cada slice de forma independiente. Cambie estos ajustes cuando tenga antenas separadas para diferentes bandas o cuando desee recibir en un puerto dedicado solo para RX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos del propio radio. Confirme que sus antenas estén físicamente conectadas y nombradas en el radio antes de continuar.

## Pasos

1. Abra el applet RX Controls. Siempre es visible en el Panel de Applets (barra lateral derecha). Si no está visible, haga clic en el botón de bandeja `RX` en la barra lateral derecha para mostrarlo.
2. Si tiene más de un slice, haga clic en la pestaña de slice correcta (A hasta H) en la parte superior del applet para vincularlo al slice que desea cambiar.
3. En la fila de encabezado, localice las dos pequeñas etiquetas de antena. La etiqueta azul corresponde a la antena RX; la etiqueta roja, a la antena TX. Ambas tienen `ANT1` como valor predeterminado.
4. **Para cambiar la antena RX:** haga clic en la etiqueta de antena azul (p. ej., `ANT1`). Se abre un menú con todos los puertos de antena disponibles. El puerto actualmente seleccionado tiene una marca de verificación. Haga clic en el puerto que desea usar para recibir.
5. **Para cambiar la antena TX:** haga clic en la etiqueta de antena roja (p. ej., `ANT1`). Se abre un menú con los puertos habilitados para TX. Los puertos cuyos nombres comienzan con `RX` están excluidos porque son de solo recepción. Haga clic en el puerto que desea usar para transmitir.
6. La etiqueta se actualiza de inmediato para mostrar la antena recién seleccionada. El radio aplica el cambio al slice activo.

## Qué hace cada control

| Control | Color | Predeterminado | Opciones válidas | Comportamiento |
|---|---|---|---|---|
| Etiqueta de antena RX | Azul | `ANT1` | Todos los puertos de la lista de antenas del radio | Haga clic para abrir un menú; al seleccionar una entrada se establece la antena de recepción para este slice. |
| Etiqueta de antena TX | Rojo | `ANT1` | Todos los puertos excepto los que tienen el prefijo `RX` | Haga clic para abrir un menú; al seleccionar una entrada se establece la antena de transmisión para este slice. Los puertos de solo recepción se filtran. |

## Consejos

- Las antenas RX y TX se configuran por slice. Al cambiar a una pestaña de slice diferente se modifica el slice que controla el applet; las etiquetas de antena se actualizan para reflejar las selecciones actuales de ese slice.
- Si el nombre de un puerto comienza con `RX` (por ejemplo, `RXANT` o `RX2`), aparece en el menú RX pero está oculto en el menú TX.

## Solución de problemas

- **El menú de antenas muestra menos puertos de los esperados** — La lista se obtiene del `ant_list` del radio. Los puertos que el firmware del radio no reporta no aparecerán. Verifique que el puerto esté habilitado en la configuración del propio radio y que el firmware 4.1.5 esté en ejecución.
- **En la etiqueta de antena TX falta un puerto que sí aparece en el menú RX** — Es probable que el nombre del puerto comience con `RX`. Los puertos de solo recepción se excluyen intencionalmente del menú de selección de TX.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprender los slices y los VFO](../../getting-started/concepts/understanding-slices.md)
