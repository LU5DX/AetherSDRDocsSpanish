# Resolver un conflicto entre la Entrada A y la Entrada B de la antena

Se produce un conflicto cuando tanto la Entrada A como la Entrada B están asignadas a la misma antena. AetherSDR señala el conflicto visualmente para que pueda reasignar una de las entradas antes de transmitir.

## Antes de comenzar

- AetherSDR ha descubierto un dispositivo ShackSwitch y el applet de ShackSwitch es visible en el Applet Panel.
- El dispositivo ShackSwitch tiene al menos dos puertos de antena disponibles (la tarjeta INPUT B no se muestra en los dispositivos R4 de un solo puerto, por lo que no es posible un conflicto en estos).

## Pasos

1. Observe las filas de antenas en el applet de ShackSwitch. Cuando existe un conflicto, el botón `[A]` y el botón `[B]` en la misma fila de antena parpadean en ámbar.
2. Decida qué entrada mover. Haga clic en el botón `[A]` de una fila de antena diferente para reasignar la Entrada A, o haga clic en el botón `[B]` de una fila de antena diferente para reasignar la Entrada B.
3. Confirme que el parpadeo se detiene. La tarjeta INPUT A y la tarjeta INPUT B deben mostrar cada una un nombre de antena diferente, y ningún botón debe parpadear.

## Función de cada control

| Control | Comportamiento | Clave de ajuste |
|---|---|---|
| Botón `[A]` (por fila de antena) | Selecciona esa antena para la Entrada A. Al hacer clic en una antena ya seleccionada, se anula su selección. Parpadea en ámbar cuando la Entrada A y la Entrada B están asignadas a la misma antena. | — |
| Botón `[B]` (por fila de antena) | Selecciona esa antena para la Entrada B. Al hacer clic en una antena ya seleccionada, se anula su selección. Parpadea en ámbar cuando hay conflicto. Cuando hay una carga ficticia configurada y la Entrada B se enruta automáticamente allí, el botón `[B]` de la fila prevista parpadea en ámbar y el botón `[B]` de la fila de carga ficticia parpadea en naranja. | — |
| Tarjeta INPUT A | Muestra la banda y el nombre de la antena actuales asignados al Puerto A. Muestra — cuando no hay ninguna antena seleccionada. | — |
| Tarjeta INPUT B | Muestra la banda y el nombre de la antena actuales asignados al Puerto B. Muestra — cuando no hay ninguna antena seleccionada. Oculto en dispositivos R4 de un solo puerto. | — |
| Selector de carga ficticia | Asigna una antena como carga ficticia. Cuando está configurada, el Puerto B se enruta automáticamente a la carga ficticia, lo que puede provocar el parpadeo ámbar en la fila de antena prevista. | `SS_DummyLoadAnt` |

## Consejos

- Si el conflicto reaparece inmediatamente después de reasignar una entrada, verifique si hay una carga ficticia configurada. Cuando se establece `SS_DummyLoadAnt`, el Puerto B se enruta automáticamente a la antena de carga ficticia. Si esa antena es la misma asignada a la Entrada A, el conflicto persistirá hasta que cambie la selección de la Entrada A o reconfigure la carga ficticia.
- Al hacer clic en un botón `[A]` o `[B]` ya activo, se anula la selección de esa entrada por completo, dejando la tarjeta correspondiente mostrando —. Esta es una forma válida de eliminar un lado del conflicto si tiene la intención de dejar esa entrada sin asignar.

## Solución de problemas

- **Los botones siguen parpadeando después de la reasignación** — Es posible que una carga ficticia esté enrutando automáticamente la Entrada B de vuelta a la antena en conflicto. Abra el selector de carga ficticia y verifique qué antena está configurada. Seleccione una antena diferente o elija None para eliminarla.
- **La tarjeta INPUT B no es visible** — El dispositivo conectado es un ShackSwitch R4 de un solo puerto. La Entrada B no está disponible en este dispositivo; no puede ocurrir un conflicto de dos entradas.

## Relacionados

- [Configure a dummy load antenna to protect the transmit path](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Select an antenna for ShackSwitch Input A](select-an-antenna-for-shackswitch-input-a.md)
- [Select an antenna for ShackSwitch Input B](select-an-antenna-for-shackswitch-input-b.md)
- [ShackSwitch overview](overview.md)
