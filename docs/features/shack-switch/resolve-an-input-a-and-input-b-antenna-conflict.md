# Resolver un conflicto entre la Entrada A y la Entrada B de antena

Se produce un conflicto cuando tanto la Entrada A como la Entrada B están asignadas a la misma antena. AetherSDR señala el conflicto visualmente para que pueda reasignar una entrada antes de transmitir.

## Antes de comenzar

- AetherSDR ha descubierto un dispositivo ShackSwitch y el applet ShackSwitch es visible en el Panel de applets.
- El dispositivo ShackSwitch tiene al menos dos puertos de antena disponibles (la tarjeta INPUT B no se muestra en dispositivos R4 de un solo puerto, por lo que no es posible un conflicto en esos casos).

## Pasos

1. Observe las filas de antena en el applet ShackSwitch. Cuando existe un conflicto, el botón `[A]` y el botón `[B]` en la misma fila de antena parpadean en ámbar.
2. Decida qué entrada mover. Haga clic en el botón `[A]` en una fila de antena diferente para reasignar la Entrada A, o haga clic en el botón `[B]` en una fila de antena diferente para reasignar la Entrada B.
3. Confirme que el parpadeo se detiene. La tarjeta INPUT A y la tarjeta INPUT B deben mostrar cada una un nombre de antena diferente, y ningún botón debe parpadear.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| Etiqueta de estado | Muestra la dirección IP del dispositivo conectado y la versión del firmware, o un mensaje de desconexión. | — |
| Botón `[A]` (por fila de antena) | Selecciona esa antena para la Entrada A. Hacer clic en una antena ya seleccionada la deselecciona. Parpadea en ámbar cuando la Entrada A y la Entrada B están asignadas a la misma antena. | — |
| Botón `[B]` (por fila de antena) | Selecciona esa antena para la Entrada B. Hacer clic en una antena ya seleccionada la deselecciona. Parpadea en ámbar cuando hay conflicto. Cuando se configura una carga ficticia y la Entrada B se enruta automáticamente allí, el botón `[B]` de la fila prevista parpadea en ámbar y el botón `[B]` de la fila de la carga ficticia parpadea en naranja. | — |
| Tarjeta INPUT A | Muestra la banda actual y el nombre de la antena asignada al Puerto A. Muestra — cuando no hay ninguna antena seleccionada. Resaltada en cian. | — |
| Tarjeta INPUT B | Muestra la banda actual y el nombre de la antena asignada al Puerto B. Muestra — cuando no hay ninguna antena seleccionada. Resaltada en naranja. Oculta en dispositivos R4 de un solo puerto. | — |
| Selector de carga ficticia | Selecciona o deselecciona una antena como carga ficticia. Cuando está configurada, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena durante la transmisión. | `SS_DummyLoadAnt` |
| Botón de Configuración | Abre la interfaz de configuración web del dispositivo ShackSwitch en el navegador del sistema. Utiliza la dirección del peer activo cuando está conectado; como fallback usa `SS_ManualIp`. El puerto se determina por `SS_WebPort`, el beacon `webPort` o el valor predeterminado 5000. | — |

## Consejos

- Si el conflicto reaparece inmediatamente después de reasignar una entrada, verifique si hay una carga ficticia configurada. Cuando `SS_DummyLoadAnt` está establecido, el Puerto B se enruta automáticamente a la antena de carga ficticia. Si esa antena es la misma asignada a la Entrada A, el conflicto persistirá hasta que cambie la selección de la Entrada A o reconfigurar la carga ficticia.
- Hacer clic en un botón `[A]` o `[B]` ya activo deselecciona esa entrada por completo, dejando la tarjeta correspondiente mostrando —. Esta es una forma válida de limpiar un lado del conflicto si tiene la intención de dejar esa entrada sin asignar.

## Solución de problemas

- **Los botones siguen parpadeando después de la reasignación** — Una carga ficticia puede estar enrutando automáticamente la Entrada B de vuelta a la antena en conflicto. Abra el selector de carga ficticia y verifique qué antena está configurada. Seleccione una antena diferente o elija Ninguna para limpiarla.
- **La tarjeta INPUT B no es visible** — El dispositivo conectado es un ShackSwitch R4 de un solo puerto. La Entrada B no está disponible en este dispositivo; no puede ocurrir un conflicto de dos entradas.

## Relacionado

- [Configure a dummy load antenna to protect the transmit path](configure-a-dummy-load-antenna-to-protect-the-transmit-path.md)
- [Select an antenna for ShackSwitch Input A](select-an-antenna-for-shackswitch-input-a.md)
- [Select an antenna for ShackSwitch Input B](select-an-antenna-for-shackswitch-input-b.md)
- [ShackSwitch overview](overview.md)
