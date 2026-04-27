# Cambiar el nombre o eliminar un perfil de micrófono

El Administrador de perfiles (Profile Manager) le permite cambiar el nombre de un perfil de micrófono guardando el estado actual del radio con un nombre nuevo, y eliminar los perfiles que ya no necesita. Úselo para mantener ordenada su lista de perfiles de micrófono a medida que cambia su configuración.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Identifique el perfil que desea renombrar o eliminar. El perfil activo aparece resaltado en la lista.

## Pasos

### Para cambiar el nombre de un perfil de micrófono

No existe un comando de cambio de nombre directo. El proceso consta de dos pasos: guardar con el nuevo nombre y luego eliminar el nombre anterior.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea renombrar en la lista **Profile list**. Su nombre aparece en el campo **Profile name**.
4. Borre el campo **Profile name** y escriba el nuevo nombre.
5. Haga clic en **Save**. El radio guarda el estado actual del micrófono con el nuevo nombre y la lista se actualiza.
6. Haga clic en el nombre del perfil original en la lista **Profile list**.
7. Haga clic en **Delete**. Aparece un cuadro de confirmación con el mensaje "Delete profile "*nombre*"?".
8. Haga clic en **Yes**. El perfil se elimina de la lista.
9. Haga clic en **Close**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea eliminar en la lista **Profile list**.
4. Haga clic en **Delete**. Aparece un cuadro de confirmación con el mensaje "Delete profile "*nombre*"?".
5. Haga clic en **Yes**. El perfil se elimina de la lista.
6. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña **Microphone** | Pestaña | Cambia el cuadro de diálogo para administrar perfiles de micrófono. |
| **Profile name** | Campo de texto | Contiene el nombre que se usa al guardar un nuevo perfil. Se rellena automáticamente al seleccionar un perfil de la lista. |
| **Profile list** | Lista | Muestra todos los perfiles de micrófono del radio. El perfil activo aparece resaltado. |
| **Load** | Botón | Carga el perfil seleccionado en el radio. Se habilita únicamente cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual del micrófono con el nombre indicado en **Profile name**. Si el campo está vacío, usa el elemento seleccionado en la lista. |
| **Delete** | Botón | Elimina el perfil seleccionado tras la confirmación. Se habilita únicamente cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el cuadro de diálogo Profile Manager. |

## Sugerencias

- Al seleccionar un perfil en la lista **Profile list**, el campo **Profile name** se rellena automáticamente. Para cambiar el nombre, simplemente sobrescriba ese texto antes de hacer clic en **Save**.
- Los botones Load y Delete permanecen deshabilitados hasta que seleccione un perfil en la lista. Si alguno de los botones aparece en gris, primero haga clic en el nombre de un perfil.
- La lista se actualiza automáticamente cuando el radio notifica un cambio. No es necesario volver a abrir el cuadro de diálogo después de guardar o eliminar.

## Solución de problemas

- **Delete aparece en gris** — No hay ningún perfil seleccionado en la lista **Profile list**. Haga clic en el nombre de un perfil para seleccionarlo y luego haga clic en **Delete**.
- **El perfil renombrado no aparece en la lista** — El radio envía las actualizaciones de la lista de forma asíncrona. Espere un momento para que la lista se actualice. Si no se actualiza, cierre y vuelva a abrir el Profile Manager.
- **El nombre del perfil anterior sigue apareciendo tras eliminarlo** — Es posible que haya hecho clic en **No** en el cuadro de confirmación. Repita los pasos 3 a 5 y haga clic en **Yes** para confirmar.

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Crear un perfil de micrófono independiente para cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre se conserven](turn-on-auto-save-so-tx-tweaks-always-persist.md)
