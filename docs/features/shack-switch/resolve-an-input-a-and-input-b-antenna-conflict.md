# Resolver un conflicto entre la antena de Input A y la de Input B

Un conflicto ocurre cuando tanto Input A como Input B están asignados a la misma antena. AetherSDR señala el conflicto visualmente para que pueda reasignar una entrada antes de transmitir.

## Antes de comenzar

- AetherSDR ha detectado un dispositivo ShackSwitch y el applet de ShackSwitch es visible en el Panel de Applets.
- El dispositivo ShackSwitch tiene al menos dos puertos de antena disponibles (la tarjeta INPUT B no se muestra en los dispositivos R4 de un solo puerto, por lo que en esos dispositivos no es posible un conflicto).

## Pasos

1. Observe las filas de antenas en el applet de ShackSwitch. Cuando existe un conflicto, el botón `[A]` y el botón `[B]` en la misma fila de antena parpadean en ámbar.
2. Decida qué entrada mover. Haga clic en el botón `[A]` de una fila de antena diferente para reasignar Input A, o haga clic en el botón `[B]` de una fila de antena diferente para reasignar Input B.
3. Confirme que el parpadeo se detiene. La tarjeta INPUT A y la tarjeta INPUT B deben mostrar cada una un nombre de antena diferente, y ningún botón debe parpadear.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Botón `[A]` (por fila de antena) | Selecciona esa antena para Input A. Al hacer clic en una antena ya seleccionada, se deselecciona. Parpadea en ámbar cuando Input A e Input B están asignados a la misma antena. | — |
| Botón `[B]` (por fila de antena) | Selecciona esa antena para Input B. Al hacer clic en una antena ya seleccionada, se deselecciona. Parpadea en ámbar cuando hay conflicto. Cuando hay una carga ficticia configurada e Input B se enruta automáticamente hacia ella, el botón `[B]` de la fila deseada parpadea en ámbar y el botón `[B]` de la fila de carga ficticia parpadea en naranja. | — |
| Tarjeta INPUT A | Muestra la banda actual y el nombre de antena asignados al Puerto A. Muestra — cuando no hay ninguna antena seleccionada. | — |
| Tarjeta INPUT B | Muestra la banda actual y el nombre de antena asignados al Puerto B. Muestra — cuando no hay ninguna antena seleccionada. Oculta en dispositivos R4 de un solo puerto. | — |
| Selector de carga ficticia | Asigna una antena como carga ficticia. Cuando está configurado, el Puerto B se enruta automáticamente a la carga ficticia, lo que puede provocar el parpadeo ámbar en la fila de antena deseada. | `SS_DummyLoadAnt` |

## Consejos

- Si el conflicto reaparece inmediatamente después de reasignar una entrada, verifique si hay una carga ficticia configurada. Cuando `SS_DummyLoadAnt` está establecido, el Puerto B se enruta automáticamente a la antena de carga ficticia. Si esa antena es la misma que está asignada a Input A, el conflicto persistirá hasta que cambie la selección de Input A o reconfigure la carga ficticia.
- Al hacer clic en un botón `[A]` o `[B]` ya activo, se deselecciona completamente esa entrada, dejando la tarjeta correspondiente mostrando —. Esta es una forma válida de eliminar uno de los lados del conflicto si desea dejar esa entrada sin asignar.

## Solución de problemas

- **Los botones siguen parpadeando después de reasignar** — Es posible que una carga ficticia esté enrutando automáticamente Input B de vuelta a la antena en conflicto. Abra el selector de carga ficticia y verifique qué antena está configurada. Seleccione una antena diferente o elija None para borrarla.
- **La tarjeta INPUT B no es visible** — El dispositivo conectado es un ShackSwitch R4 de un solo puerto. Input B no está disponible en este dispositivo; no puede ocurrir un conflicto de dos entradas.

## Temas relacionados

- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Seleccionar una antena para ShackSwitch Input A](select-an-antenna-for-shackswitch-input-a.md)
- [Seleccionar una antena para ShackSwitch Input B](select-an-antenna-for-shackswitch-input-b.md)
- [Descripción general de ShackSwitch](overview.md)
