# Seleccionar la antena RX o TX para este slice

Esta página explica cómo cambiar la antena de recepción o transmisión asignada a un slice (receptor virtual). Puede hacerlo para alternar entre una antena direccional y una vertical, o para dirigir puertos de antena exclusivos de recepción únicamente hacia el camino RX.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet RX Controls no mostrará las listas de antenas sin una conexión activa.
- La lista de antenas la proporciona el radio. Cualquier puerto de antena que no aparezca en el `ant_list` del radio no estará disponible como opción.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (A, B, C … H) que desea configurar.
3. En la fila de encabezado, localice las dos pequeñas etiquetas de antena. La etiqueta **azul** es la antena RX actual; la etiqueta **roja** es la antena TX actual. Ambas tienen **ANT1** como valor predeterminado.
4. Para cambiar la **antena RX**: haga clic en la etiqueta azul de antena. Un menú muestra todas las antenas disponibles del radio. La selección actual aparece marcada. Haga clic en la antena deseada.
5. Para cambiar la **antena TX**: haga clic en la etiqueta roja de antena. Un menú muestra únicamente las antenas con capacidad de transmisión — los puertos cuyos nombres comienzan con **RX** quedan excluidos. Haga clic en la antena deseada.
6. La etiqueta se actualiza de inmediato para reflejar su selección. El cambio surte efecto en el radio al instante.

## Qué hace cada control

| Control | Color de etiqueta | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|---|
| Antena RX | Azul | ANT1 | Todos los puertos en el `ant_list` del radio | Establece la antena de recepción para este slice. |
| Antena TX | Rojo | ANT1 | Puertos en `ant_list` que no comienzan con `RX` | Establece la antena de transmisión para este slice. |

Ninguno de los controles tiene una clave de configuración persistente — las selecciones de antena las conserva el radio y las restaura al reconectarse.

## Consejos

- Los puertos cuyos nombres comienzan con `RX` (sin distinción entre mayúsculas y minúsculas) son exclusivamente de recepción y se filtran del menú de antena TX. Si una antena desde la que espera transmitir no aparece en la lista TX, verifique si su nombre comienza con `RX` en la configuración de antenas del radio.
- Es posible asignar antenas RX y TX diferentes a cada slice de forma independiente. Cada pestaña de slice tiene su propio par de controles de antena.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Entender los slices y los VFOs](../../getting-started/concepts/understanding-slices.md)
