# Cambiar el nombre o eliminar un perfil de micrófono

El Administrador de perfiles le permite cambiar el nombre de un perfil de micrófono guardando el estado actual del radio con un nombre nuevo, y eliminar perfiles que ya no necesite. Utilice esta función para mantener ordenada su lista de perfiles de micrófono a medida que su configuración cambia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Administrador de perfiles requiere una conexión activa con el radio.
- Sepa qué perfil desea renombrar o eliminar. El perfil activo aparece resaltado en la lista.

## Pasos

### Para cambiar el nombre de un perfil de micrófono

No existe un comando de renombrado directo. Cambiar el nombre es un proceso de dos pasos: cree un nuevo perfil con el nombre deseado y luego elimine el anterior.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. En la **Profile list**, haga clic en el perfil que desea renombrar. Su nombre aparece en el campo **Profile name**.
4. Borre el campo **Profile name** y escriba el nombre nuevo.
5. Haga clic en **Create**. El radio crea un nuevo perfil de micrófono con el nombre nuevo y la lista se actualiza.
6. En la **Profile list**, haga clic en el nombre del perfil original.
7. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación que pregunta "Delete profile "*name*"?".
8. Haga clic en **Yes**. El perfil se elimina de la lista.
9. Haga clic en **Close**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. En la **Profile list**, haga clic en el perfil que desea eliminar.
4. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación que pregunta "Delete profile "*name*"?".
5. Haga clic en **Yes**. El perfil se elimina de la lista.
6. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña **Microphone** | Pestaña | Cambia el diálogo para administrar perfiles de micrófono. |
| **Profile name** | Campo de texto | Contiene el nombre que se usará al guardar un perfil nuevo. Se rellena automáticamente al seleccionar un perfil de la lista. El texto de marcador de posición es "New Profile Name". |
| **Profile list** | Lista | Muestra todos los perfiles de micrófono en el radio. El perfil activo aparece resaltado. |
| **Load** | Botón | Carga el perfil seleccionado en el radio. Solo se habilita cuando hay un perfil seleccionado. |
| **Create** | Botón | Crea un nuevo perfil de micrófono con el nombre indicado en **Profile name**. No sobrescribe un perfil existente. Si el campo está vacío, utiliza como respaldo el elemento seleccionado en la lista. |
| **Delete** | Botón | Elimina el perfil seleccionado después de la confirmación. Solo se habilita cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el diálogo del Administrador de perfiles. |

## Consejos

- Al seleccionar un perfil en la **Profile list**, el campo **Profile name** se rellena automáticamente. Para renombrar, simplemente sobrescriba ese texto antes de hacer clic en **Create**.
- Load y Delete están deshabilitados hasta que seleccione un perfil en la lista. Si alguno de los botones aparece atenuado, primero haga clic en un nombre de perfil.
- La lista se actualiza automáticamente cuando el radio reporta un cambio. No necesita volver a abrir el diálogo después de crear o eliminar.
- Los perfiles de micrófono no se pueden sobrescribir directamente. Para actualizar un perfil de micrófono existente, active **Auto-Save** en la pestaña **Auto-Save** y luego realice sus cambios mientras el perfil está activo.

## Solución de problemas

- **Delete aparece atenuado** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo y luego haga clic en **Delete**.
- **Create funciona pero el perfil nuevo no aparece en la lista** — El radio envía las actualizaciones de la lista de forma asíncrona. Espere un momento para que la lista se actualice. Si no se actualiza, cierre y vuelva a abrir el Administrador de perfiles.
- **Aparece un diálogo "Profile already exists"** — Intentó crear un perfil de micrófono con un nombre que ya existe. El radio no puede sobrescribir perfiles de micrófono. Haga clic en **Enable Auto-Save** en el diálogo para activar el guardado automático de perfiles, luego cargue el perfil existente y realice sus cambios para actualizarlo.
- **El nombre del perfil anterior sigue presente después de eliminar** — Es posible que haya hecho clic en **No** en el mensaje de confirmación. Repita los pasos 3 a 5 y haga clic en **Yes** para confirmar.

## Relacionados

- [Descripción general del Administrador de perfiles](overview.md)
- [Crear un perfil de micrófono separado para cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el auto-guardado para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
