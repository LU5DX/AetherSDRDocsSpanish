# Cambiar el nombre o eliminar un perfil de micrófono

El Administrador de perfiles le permite cambiar el nombre de un perfil de micrófono guardando el estado actual de la radio con un nombre nuevo y eliminar los perfiles que ya no necesite. Utilícelo para mantener ordenada su lista de perfiles de micrófono a medida que cambia su configuración.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Sepa qué perfil desea renombrar o eliminar. El perfil activo está resaltado en la lista.

## Pasos

### Para cambiar el nombre de un perfil de micrófono

No existe un comando para renombrar directamente. Renombrar es un proceso de dos pasos: guardar con el nombre nuevo y luego eliminar el anterior.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea renombrar en la **Profile list**. Su nombre aparece en el campo **Profile name**.
4. Borre el campo **Profile name** y escriba el nombre nuevo.
5. Haga clic en **Save**. La radio guarda el estado actual del micrófono con el nombre nuevo y la lista se actualiza.
6. Haga clic en el nombre del perfil original en la **Profile list**.
7. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación preguntando "Delete profile "*name*"?".
8. Haga clic en **Yes**. El perfil se elimina de la lista.
9. Haga clic en **Close**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea eliminar en la **Profile list**.
4. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación preguntando "Delete profile "*name*"?".
5. Haga clic en **Yes**. El perfil se elimina de la lista.
6. Haga clic en **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña **Microphone** | Pestaña | Cambia el cuadro de diálogo para administrar perfiles de micrófono. |
| **Profile name** | Campo de texto | Contiene el nombre que se usa al guardar un perfil nuevo. Se completa automáticamente al seleccionar un perfil de la lista. |
| **Profile list** | Lista | Muestra todos los perfiles de micrófono en la radio. El perfil activo está resaltado. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual del micrófono con el nombre indicado en **Profile name**. Usa el elemento seleccionado en la lista si el campo está vacío. |
| **Delete** | Botón | Elimina el perfil seleccionado después de la confirmación. Solo se habilita cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el cuadro de diálogo del Administrador de perfiles. |

## Consejos

- Al seleccionar un perfil en la **Profile list**, se completa automáticamente el campo **Profile name**. Para renombrar, simplemente sobrescriba ese texto antes de hacer clic en **Save**.
- Load y Delete están deshabilitados hasta que seleccione un perfil en la lista. Si alguno de los botones aparece atenuado, haga clic primero en un nombre de perfil.
- La lista se actualiza automáticamente cuando la radio informa un cambio. No es necesario volver a abrir el cuadro de diálogo después de guardar o eliminar.

## Solución de problemas

- **Delete está atenuado** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo y luego haga clic en **Delete**.
- **El perfil renombrado no aparece en la lista** — La radio envía las actualizaciones de la lista de forma asíncrona. Espere un momento para que la lista se refresque. Si no se actualiza, cierre y vuelva a abrir el Administrador de perfiles.
- **El nombre del perfil anterior aún está presente después de eliminar** — Es posible que haya hecho clic en **No** en el mensaje de confirmación. Repita los pasos 3 a 5 y haga clic en **Yes** para confirmar.

## Relacionado

- [Profile Manager overview](overview.md)
- [Create a separate mic profile per microphone](create-a-separate-mic-profile-per-microphone.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
