# Cambiar el nombre o eliminar un perfil de micrófono

El Administrador de perfiles le permite cambiar el nombre de un perfil de micrófono guardando el estado actual de la radio con un nuevo nombre y eliminar perfiles que ya no necesite. Utilícelo para mantener ordenada su lista de perfiles de micrófono a medida que su configuración cambia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa a la radio.
- Sepa qué perfil desea renombrar o eliminar. El perfil activo está resaltado en la lista.

## Pasos

### Para cambiar el nombre de un perfil de micrófono

No existe un comando de renombrado directo. Cambiar el nombre es un proceso de dos pasos: cree un nuevo perfil con el nombre deseado y luego elimine el anterior.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea renombrar en la lista de perfiles (**Profile list**). Su nombre aparece en el campo **Profile name**.
4. Limpie el campo **Profile name** y escriba el nuevo nombre.
5. Haga clic en **Save**. La radio crea un nuevo perfil de micrófono con el nuevo nombre y la lista se actualiza.
6. Haga clic en el nombre del perfil original en la lista de perfiles (**Profile list**).
7. Haga clic en **Delete**. Aparece un diálogo de confirmación preguntando "¿Eliminar el perfil "*nombre*"?".
8. Haga clic en **Yes**. El perfil se elimina de la lista.
9. Haga clic en **Close**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea eliminar en la lista de perfiles (**Profile list**).
4. Haga clic en **Delete**. Aparece un diálogo de confirmación preguntando "¿Eliminar el perfil "*nombre*"?".
5. Haga clic en **Yes**. El perfil se elimina de la lista.
6. Haga clic en **Close**.

### Para eliminar o cargar un perfil de transmisión

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Transmit**.
3. Haga clic en el perfil que desea cargar o eliminar en la lista de perfiles (**Profile list**).
4. Haga clic en **Load** para aplicar el perfil de transmisión seleccionado a la radio.
5. Haga clic en **Delete** para eliminar el perfil de transmisión seleccionado después de la confirmación.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña **Global** | Pestaña | Cambia el diálogo para gestionar perfiles globales. |
| Pestaña **Transmit** | Pestaña | Cambia el diálogo para gestionar perfiles de transmisión. |
| Pestaña **Microphone** | Pestaña | Cambia el diálogo para gestionar perfiles de micrófono. |
| Pestaña **Auto-Save** | Pestaña | Cambia el diálogo para controlar el guardado automático de perfiles. |
| **Profile name** | Campo de texto | Contiene el nombre que se usará al guardar un nuevo perfil. Se completa automáticamente al seleccionar un perfil de la lista. |
| **Profile list** | Lista | Muestra todos los perfiles de la categoría seleccionada en la radio. El perfil activo está resaltado. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo habilitado cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre en **Profile name**. |
| **Delete** | Botón | Elimina el perfil seleccionado después de la confirmación. Solo habilitado cuando hay un perfil seleccionado. |
| **Auto-save profile changes** | Casilla de verificación | Cuando está activada, los cambios de transmisión se escriben automáticamente en el perfil de transmisión activo. Clave de configuración: `AutoSaveTransmitProfile`. |
| **Close** | Botón | Cierra el diálogo del Administrador de perfiles. |

## Consejos

- Seleccionar un perfil en la lista de perfiles (**Profile list**) completa automáticamente el campo **Profile name**. Para renombrar, simplemente sobrescriba ese texto antes de hacer clic en **Save**.
- Los botones **Load** y **Delete** están deshabilitados hasta que seleccione un perfil en la lista. Si alguno de los botones aparece atenuado, primero haga clic en un nombre de perfil.
- La lista se actualiza automáticamente cuando la radio informa un cambio. No necesita volver a abrir el diálogo después de crear o eliminar.
- Los perfiles de micrófono no se pueden sobrescribir directamente. Para actualizar un perfil de micrófono existente, active **Auto-save profile changes** en la pestaña **Auto-Save** y luego realice sus cambios mientras el perfil está activo.
- La casilla **Auto-save profile changes** se mantiene sincronizada con la radio: si el guardado automático se activa o desactiva desde otro cliente o mediante el proceso de carga de perfiles, la casilla se actualiza automáticamente.
- El botón **Load** para perfiles de transmisión ahora utiliza internamente el comando `profile tx load`. Este cambio es transparente y no afecta la forma en que interactúa con el diálogo.

## Solución de problemas

- **El botón Delete aparece atenuado** — No hay ningún perfil seleccionado en la lista de perfiles (**Profile list**). Haga clic en un nombre de perfil para seleccionarlo y luego haga clic en **Delete**.
- **El botón Save aparece pero el nuevo perfil no se muestra en la lista** — La radio envía las actualizaciones de la lista de forma asíncrona. Espere un momento a que la lista se actualice. Si no se actualiza, cierre y vuelva a abrir el Administrador de perfiles.
- **Aparece un diálogo "Profile already exists"** — Intentó crear un perfil de micrófono con un nombre que ya existe. La radio no puede sobrescribir perfiles de micrófono. Haga clic en **Enable Auto-Save** en el diálogo para activar el guardado automático de perfiles, luego cargue el perfil existente y realice sus cambios para actualizarlo.
- **El nombre del perfil antiguo aún aparece después de eliminar** — Es posible que haya hecho clic en **No** en el mensaje de confirmación. Repita los pasos 3–5 y haga clic en **Yes** para confirmar.
- **La carga del perfil de transmisión falla** — Asegúrese de que la radio esté conectada y que el nombre del perfil de transmisión sea válido. El diálogo utiliza el comando `profile tx load` para cargar perfiles de transmisión.

## Temas relacionados

- [Descripción general del Administrador de perfiles](overview.md)
- [Crear un perfil de micrófono separado para cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
