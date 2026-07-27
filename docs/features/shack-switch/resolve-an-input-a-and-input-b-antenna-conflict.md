# Resolver un conflicto entre la Entrada A y la Entrada B de antena

Se produce un conflicto cuando tanto la Entrada A como la Entrada B están asignadas a la misma antena. AetherSDR señala el conflicto visualmente para que pueda reasignar una de las entradas antes de transmitir.

## Antes de comenzar

- AetherSDR ha descubierto un dispositivo ShackSwitch y el applet ShackSwitch está visible en el Panel de applets.
- El dispositivo ShackSwitch tiene al menos dos puertos de antena disponibles (la tarjeta INPUT B no se muestra en los dispositivos R4 de un solo puerto, por lo que no es posible un conflicto en esos).

## Pasos

1. Observe las filas de antenas en el applet ShackSwitch. Cuando existe un conflicto, el botón `[A]` y el botón `[B]` en la misma fila de antena parpadean en ámbar.
2. Decida qué entrada mover. Haga clic en el botón `[A]` de una fila de antena diferente para reasignar la Entrada A, o haga clic en el botón `[B]` de una fila de antena diferente para reasignar la Entrada B.
3. Verifique que el parpadeo se detenga. La tarjeta INPUT A y la tarjeta INPUT B deben mostrar cada una un nombre de antena diferente, y ningún botón debe parpadear.

## Función de cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión del firmware, o un mensaje de desconexión. | — |
| Botón `[A]` (por fila de antena) | Selecciona esa antena para la Entrada A. Al hacer clic en una antena ya seleccionada, se anula la selección. Parpadea en ámbar cuando la Entrada A y la Entrada B están asignadas a la misma antena. | — |
| Botón `[B]` (por fila de antena) | Selecciona esa antena para la Entrada B. Al hacer clic en una antena ya seleccionada, se anula la selección. Parpadea en ámbar cuando hay conflicto. Cuando se configura una carga ficticia y la Entrada B se enruta automáticamente hacia allí, el botón `[B]` de la fila prevista parpadea en ámbar y el botón `[B]` de la fila de carga ficticia parpadea en naranja. | — |
| Tarjeta INPUT A | Muestra la banda actual y el nombre de la antena asignada al Puerto A. Muestra — cuando no hay antena seleccionada. Resaltada en cian. | — |
| Tarjeta INPUT B | Muestra la banda actual y el nombre de la antena asignada al Puerto B. Muestra — cuando no hay antena seleccionada. Resaltada en naranja. Oculto en dispositivos R4 de un solo puerto. | — |
| Selector de carga ficticia | Selecciona o anula la selección de una antena como carga ficticia. Cuando está configurada, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |
| Botón de configuración | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Utiliza la dirección del par activo cuando está conectado; de lo contrario, usa `SS_ManualIp`. El puerto se determina mediante `SS_WebPort`, la baliza `webPort` o el valor predeterminado 5000. | — |

## Consejos

- Si el conflicto reaparece inmediatamente después de reasignar una entrada, verifique si hay una carga ficticia configurada. Cuando `SS_DummyLoadAnt` está establecido, el Puerto B se enruta automáticamente a la antena de carga ficticia. Si esa antena es la misma asignada a la Entrada A, el conflicto persistirá hasta que cambie la selección de la Entrada A o reconfigure la carga ficticia.
- Al hacer clic en un botón `[A]` o `[B]` ya activo, se anula la selección de esa entrada por completo, dejando la tarjeta correspondiente mostrando —. Esta es una forma válida de eliminar un lado del conflicto si tiene la intención de dejar esa entrada sin asignar.

## Solución de problemas

- **Los botones siguen parpadeando después de la reasignación** — Es posible que una carga ficticia esté redirigiendo automáticamente la Entrada B a la antena en conflicto. Abra el selector de carga ficticia y verifique qué antena está configurada. Seleccione una antena diferente o elija Ninguna para eliminarla.
- **La tarjeta INPUT B no es visible** — El dispositivo conectado es un ShackSwitch R4 de un solo puerto. La Entrada B no está disponible en este dispositivo; no puede ocurrir un conflicto de dos entradas.

## Relacionados

- [Configurar una antena de carga ficticia para proteger la ruta de transmisión](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Seleccionar una antena para la Entrada A del ShackSwitch](select-an-antenna-for-shackswitch-input-a.md)
- [Seleccionar una antena para la Entrada B del ShackSwitch](select-an-antenna-for-shackswitch-input-b.md)
- [Descripción general de ShackSwitch](overview.md)
