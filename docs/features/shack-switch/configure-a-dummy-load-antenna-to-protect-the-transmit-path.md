# Configurar una antena de carga fantasma para proteger la ruta de transmisión

Use el selector de carga fantasma para designar un puerto de antena como carga fantasma. Cuando está configurado, el Puerto B se enruta automáticamente a ese puerto para proteger su antena de transmisiones no deseadas.

## Antes de comenzar

- Un dispositivo ShackSwitch debe estar detectado en la LAN o conectado mediante la pestaña Peripherals en Radio Setup. El applet de ShackSwitch aparece automáticamente cuando un dispositivo está activo.
- El applet de ShackSwitch debe estar visible. Si no lo está, haga clic en el botón SS del panel lateral derecho.
- Debe haber al menos una antena en la lista de antenas antes de poder asignar una carga fantasma.

## Pasos

1. Abra el applet de ShackSwitch en el Applet Panel.
2. Haga clic en el botón "Dummy Load: None" cerca de la parte inferior del applet. Aparece un menú con la opción None y todos los nombres de antenas disponibles.
3. Haga clic en el nombre de la antena que desea designar como carga fantasma. Aparece una marca de verificación junto a la antena seleccionada y la etiqueta del botón se actualiza para mostrar el nombre elegido.
4. Para eliminar la asignación de carga fantasma, haga clic en el botón nuevamente y seleccione None.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Botón selector de carga fantasma | Abre un menú para asignar o borrar la antena de carga fantasma. Cuando se asigna una antena, el Puerto B se enruta automáticamente a ella. La etiqueta del botón refleja la asignación actual. | None | `SS_DummyLoadAnt` |

`SS_DummyLoadAnt` almacena el ID de antena entero de la carga fantasma asignada. Un valor de `-1` significa que no hay ninguna carga fantasma configurada.

## Consejos

- Cuando se configura una carga fantasma y el Puerto B se enruta automáticamente a ella, el botón [B] de la fila de la antena deseada parpadea en ámbar y el botón [B] de la fila de la carga fantasma parpadea en naranja. Esto le proporciona una indicación visual de que B ha sido redirigido a la carga fantasma en lugar de a la antena que seleccionó.
- La asignación de carga fantasma persiste entre sesiones mediante `SS_DummyLoadAnt`. No es necesario reconfigurarla cada vez que se conecta.

## Resolución de problemas

- **La lista de antenas en el menú está vacía** — El dispositivo ShackSwitch aún no ha reportado ningún puerto de antena. Confirme que el dispositivo está conectado y que la etiqueta de estado muestra una dirección IP y versión de firmware válidas en lugar de un mensaje de desconexión.
- **El Puerto B no se enruta a la carga fantasma** — Verifique que `SS_DummyLoadAnt` esté establecido en un ID de antena válido (no `-1`) comprobando que el botón selector de carga fantasma muestre un nombre de antena en lugar de "Dummy Load: None".

## Relacionados

- [Descripción general de ShackSwitch](overview.md)
- [Seleccionar una antena para la entrada B de ShackSwitch](select-an-antenna-for-shackswitch-input-b.md)
- [Resolver un conflicto entre la antena de la entrada A y la entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
