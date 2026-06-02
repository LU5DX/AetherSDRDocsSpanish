# Configurar una antena de carga ficticia para proteger la ruta de transmisión

Utilice el selector de carga ficticia para designar un puerto de antena como carga ficticia. Una vez configurado, el Puerto B se enruta automáticamente a ese puerto para proteger su antena de una transmisión no deseada.

## Antes de comenzar

- Un dispositivo ShackSwitch debe estar descubierto en la LAN o conectado mediante la pestaña Periféricos en Configuración de Radio. El applet ShackSwitch aparece automáticamente cuando un dispositivo está activo.
- El applet ShackSwitch debe estar visible. Si no lo está, haga clic en el botón SS de la barra lateral derecha.
- Debe haber al menos una antena presente en la lista de antenas antes de poder asignar una carga ficticia.

## Pasos

1. Abra el applet ShackSwitch en el Panel de Applets.
2. Haga clic en el botón selector de Carga Ficticia cerca de la parte inferior del applet. Selecciona o anula la selección de una antena como carga ficticia. Una vez configurado, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena al transmitir.
3. Para eliminar la asignación de carga ficticia, haga clic nuevamente en el botón para anular la selección.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| Selector de carga ficticia | Selecciona o anula la selección de una antena como carga ficticia. Una vez configurado, el Puerto B se enruta automáticamente a la carga ficticia para proteger la antena al transmitir. | -1 (sin carga ficticia configurada) | `SS_DummyLoadAnt` |

`SS_DummyLoadAnt` almacena el ID entero de la antena asignada como carga ficticia. Un valor de `-1` indica que no hay ninguna carga ficticia configurada.

## Consejos

- Cuando se configura una carga ficticia y el Puerto B se enruta automáticamente a ella, el botón [B] en la fila de la antena prevista parpadea en ámbar y el botón [B] de la fila de la carga ficticia parpadea en naranja. Esto le proporciona una indicación visual de que B se ha estacionado en la carga ficticia en lugar de en la antena que seleccionó.
- La asignación de carga ficticia persiste entre sesiones mediante `SS_DummyLoadAnt`. No es necesario reconfigurarla cada vez que se conecta.

## Solución de problemas

- **La lista de antenas para la selección de carga ficticia no muestra opciones** — El dispositivo ShackSwitch aún no ha informado de ningún puerto de antena. Confirme que el dispositivo está conectado y que la etiqueta de estado muestra una dirección IP y una versión de firmware válidas, en lugar de un mensaje de desconexión.
- **El Puerto B no se está enrutando a la carga ficticia** — Verifique que `SS_DummyLoadAnt` esté configurado con un ID de antena válido (no `-1`) comprobando que el selector de carga ficticia muestre un nombre de antena en lugar de estar en estado anulado.

## Relacionado

- [Descripción general de ShackSwitch](overview.md)
- [Seleccionar una antena para la Entrada B de ShackSwitch](select-an-antenna-for-shackswitch-input-b.md)
- [Resolver un conflicto de antena entre la Entrada A y la Entrada B](resolve-an-input-a-and-input-b-antenna-conflict.md)
