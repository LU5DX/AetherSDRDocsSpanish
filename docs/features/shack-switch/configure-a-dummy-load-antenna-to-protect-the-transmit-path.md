# Configure una antena de carga ficticia para proteger la ruta de transmisión

Use el selector de carga ficticia para designar un puerto de antena como carga ficticia. Una vez configurado, el Puerto B se enruta automáticamente a ese puerto para proteger su antena de una transmisión no intencionada.

## Antes de comenzar

- Un dispositivo ShackSwitch debe estar descubierto en la LAN o conectado a través de la pestaña Periféricos en Configuración de Radio. El applet ShackSwitch aparece automáticamente cuando un dispositivo está activo.
- El applet ShackSwitch debe estar visible. Si no lo está, haga clic en el botón de la bandeja SS en la barra lateral derecha.
- Debe haber al menos una antena presente en la lista de antenas antes de poder asignar una carga ficticia.

## Pasos

1. Abra el applet ShackSwitch en el Panel de Applets.
2. Haga clic en el botón "Dummy Load: None" cerca de la parte inferior del applet. Aparece un menú que lista None y todos los nombres de antena disponibles.
3. Haga clic en el nombre de la antena que desea designar como carga ficticia. Aparece una marca de verificación junto a la antena seleccionada y la etiqueta del botón se actualiza para mostrar el nombre de la antena elegida.
4. Para eliminar la asignación de carga ficticia, haga clic en el botón nuevamente y seleccione None.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---|---|---|---|
| Botón selector de carga ficticia | Abre un menú para asignar o limpiar la antena de carga ficticia. Cuando se asigna una antena, el Puerto B se enruta automáticamente a ella. La etiqueta del botón refleja la asignación actual. | None | `SS_DummyLoadAnt` |

`SS_DummyLoadAnt` almacena el ID entero de la antena de la carga ficticia asignada. Un valor de `-1` significa que no hay carga ficticia configurada.

## Consejos

- Cuando una carga ficticia está configurada y el Puerto B se enruta automáticamente a ella, el botón [B] en la fila de la antena prevista parpadea en ámbar y el botón [B] en la fila de la carga ficticia parpadea en naranja. Esto le brinda una indicación visual de que B se ha estacionado en la carga ficticia en lugar de en la antena que seleccionó.
- La asignación de carga ficticia persiste entre sesiones a través de `SS_DummyLoadAnt`. No es necesario reconfigurarla cada vez que se conecta.

## Solución de problemas

- **La lista de antenas en el menú está vacía** — El dispositivo ShackSwitch aún no ha informado ningún puerto de antena. Confirme que el dispositivo esté conectado y que la etiqueta de estado muestre una dirección IP válida y una versión de firmware en lugar de un mensaje de desconexión.
- **El Puerto B no se está enrutando a la carga ficticia** — Verifique que `SS_DummyLoadAnt` esté configurado con un ID de antena válido (no `-1`) comprobando que el botón selector de carga ficticia muestre un nombre de antena en lugar de "Dummy Load: None".

## Relacionado

- [ShackSwitch overview](overview.md)
- [Select an antenna for ShackSwitch Input B](select-an-antenna-for-shackswitch-input-b.md)
- [Resolve an Input A and Input B antenna conflict](resolve-an-input-a-and-input-b-antenna-conflict.md)
