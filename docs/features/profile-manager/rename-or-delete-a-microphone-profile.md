# Cambiar el nombre o eliminar un perfil de micrófono

El Administrador de perfiles le permite cambiar el nombre de un perfil de micrófono guardando el estado actual de la radio con un nombre nuevo, y eliminar perfiles que ya no necesite. Utilice esta función para mantener ordenada su lista de perfiles de micrófono a medida que su configuración cambia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Sepa qué perfil desea renombrar o eliminar. El perfil activo está resaltado en la lista.

## Pasos

### Para renombrar un perfil de micrófono

No existe un comando de renombrar en el lugar. Renombrar es un proceso de dos pasos: cree un perfil nuevo con el nombre deseado, luego elimine el antiguo.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea renombrar en la **Profile list**. Su nombre aparece en el campo **Profile name**.
4. Borre el campo **Profile name** y escriba el nombre nuevo.
5. Haga clic en **Save**. La radio crea un perfil de micrófono nuevo con el nombre nuevo y la lista se actualiza.
6. Haga clic en el nombre del perfil original en la **Profile list**.
7. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación que pregunta "Delete profile "*nombre*"?".
8. Haga clic en **Yes**. El perfil se elimina de la lista.
9. Haga clic en **Close**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea eliminar en la **Profile list**.
4. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación que pregunta "Delete profile "*nombre*"?".
5. Haga clic en **Yes**. El perfil se elimina de la lista.
6. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña **Global** | Pestaña | Cambia el diálogo para gestionar perfiles globales. |
| Pestaña **Transmit** | Pestaña | Cambia el diálogo para gestionar perfiles de transmisión. |
| Pestaña **Microphone** | Pestaña | Cambia el diálogo para gestionar perfiles de micrófono. |
| Pestaña **Auto-Save** | Pestaña | Cambia el diálogo para controlar el guardado automático de perfiles. |
| **Profile name** | Campo de texto | Contiene el nombre que se usará al guardar un perfil nuevo. Se completa automáticamente al seleccionar un perfil de la lista. |
| **Profile list** | Lista | Muestra todos los perfiles de la categoría seleccionada en la radio. El perfil activo está resaltado. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo está habilitado cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre que está en **Profile name**. |
| **Delete** | Botón | Elimina el perfil seleccionado tras la confirmación. Solo está habilitado cuando hay un perfil seleccionado. |
| **Auto-save profile changes** | Casilla de verificación | Cuando está activada, los cambios de transmisión se escriben automáticamente en el perfil de transmisión activo. Clave de configuración: `AutoSaveTransmitProfile`. |
| **Close** | Botón | Cierra el diálogo del Administrador de perfiles. |

## Consejos

- Al seleccionar un perfil en la **Profile list**, el campo **Profile name** se completa automáticamente. Para renombrar, simplemente sobrescriba ese texto antes de hacer clic en **Save**.
- Load y Delete están deshabilitados hasta que seleccione un perfil en la lista. Si alguno de los botones aparece atenuado, haga clic primero en un nombre de perfil.
- La lista se actualiza automáticamente cuando la radio reporta un cambio. No necesita volver a abrir el diálogo después de crear o eliminar.
- Los perfiles de micrófono no se pueden sobrescribir directamente. Para actualizar un perfil de micrófono existente, active **Auto-save profile changes** en la pestaña **Auto-Save** y luego realice sus cambios mientras el perfil está activo.
- La casilla **Auto-save profile changes** se mantiene sincronizada con la radio: si el guardado automático se activa o desactiva desde otro cliente o mediante el proceso de carga de perfil, la casilla se actualiza automáticamente.

## Solución de problemas

- **Delete está atenuado** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo, luego haga clic en **Delete**.
- **Save aparece, pero el perfil nuevo no se muestra en la lista** — La radio envía las actualizaciones de la lista de forma asíncrona. Espere un momento para que la lista se refresque. Si no se actualiza, cierre y vuelva a abrir el Administrador de perfiles.
- **Aparece un diálogo "Profile already exists"** — Intentó crear un perfil de micrófono con un nombre que ya existe. La radio no puede sobrescribir perfiles de micrófono. Haga clic en **Enable Auto-Save** en el diálogo para activar el guardado automático de perfiles, luego cargue el perfil existente y realice sus cambios para actualizarlo.
- **El nombre del perfil antiguo aún está presente después de eliminar** — Es posible que haya hecho clic en **No** en el mensaje de confirmación. Repita los pasos 3 a 5 y haga clic en **Yes** para confirmar.

## Relacionado

- [Descripción general del Administrador de perfiles](overview.md)
- [Crear un perfil de micrófono separado por cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
