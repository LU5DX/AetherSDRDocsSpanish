# Seleccionar la antena RX o TX para este slice

El applet RX Controls permite elegir qué puerto de antena usa el FLEX-8600 para recibir y transmitir en cada slice de forma independiente. Utilícelo cuando tenga varias antenas conectadas y necesite enrutar un slice específico a un puerto específico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de antena no están disponibles sin una conexión activa.
- La lista de antenas se obtiene de la configuración de puertos del propio radio. Confirme que sus antenas estén conectadas y reconocidas por el radio antes de cambiar estos ajustes.

## Pasos

1. Abra el applet RX Controls. Si no está visible, haga clic en el botón **RX** de la bandeja en la barra lateral derecha.
2. Si tiene más de un slice, haga clic en la pestaña del slice (de A a H) correspondiente al slice que desea modificar.
3. **Para cambiar la antena RX:** Haga clic en la etiqueta de antena azul cerca de la parte superior del applet (muestra la antena RX actual, por ejemplo, **ANT1**). Aparece un menú con todos los puertos de antena disponibles. Haga clic en el puerto deseado. Una marca de verificación indica la selección actual.
4. **Para cambiar la antena TX:** Haga clic en la etiqueta de antena roja junto a la etiqueta de antena RX (también muestra la antena TX actual, por ejemplo, **ANT1**). Aparece un menú con los puertos de antena habilitados para transmisión. Haga clic en el puerto deseado.

## Qué hace cada control

| Control | Valor predeterminado | Valores válidos | Comportamiento |
|---|---|---|---|
| **ANT1** (antena RX, etiqueta azul) | ANT1 | Puertos de antena de la ant_list del radio | Abre un menú; al seleccionar una entrada se establece la antena RX para este slice. |
| **ANT1** (antena TX, etiqueta roja) | ANT1 | Puertos habilitados para TX de la ant_list del radio | Abre un menú; al seleccionar una entrada se establece la antena TX para este slice. Los puertos cuyos nombres comienzan con `RX` quedan excluidos. |

## Consejos

- La etiqueta de antena RX se muestra en azul; la etiqueta de antena TX se muestra en rojo. Esta es la única distinción visual entre los dos controles, ya que aparecen uno al lado del otro en la fila del encabezado.
- Los puertos de antena cuyos nombres comienzan con `RX` se excluyen del menú de antena TX. Seguirán apareciendo en el menú de antena RX.
- Cada slice tiene su propia asignación independiente de antena RX y TX. Cambiar la antena en el slice A no afecta al slice B.

## Solución de problemas

- **Un puerto de antena esperado no aparece en el menú** — La lista proviene directamente de la ant_list del radio. Verifique que el puerto esté configurado y reconocido en los ajustes del propio radio. AetherSDR no puede agregar puertos que el radio no haya informado.
- **El menú de antena TX no muestra un puerto que sí aparece en el menú de antena RX** — Los puertos cuyos nombres comienzan con `RX` se excluyen intencionalmente del menú de antena TX porque el radio los trata como exclusivos para recepción.
- **Ambas etiquetas aparecen atenuadas o no responden** — AetherSDR no está conectado al radio. Vuelva a conectarse mediante `Settings > Connect to Radio...`.

## Relacionado

- [Descripción general de RX Controls](overview.md)
- [Cambiar entre múltiples slices usando la fila de pestañas A..H](switch-between-multiple-slices-using-the-a-h-tab-row.md)
- [Comprensión de slices y VFOs](../../getting-started/concepts/understanding-slices.md)
