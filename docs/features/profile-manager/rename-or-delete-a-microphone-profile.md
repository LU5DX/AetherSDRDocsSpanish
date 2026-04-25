# Renombrar o eliminar un perfil de micrófono

El Profile Manager permite renombrar un perfil de micrófono guardando el estado actual del equipo con un nombre nuevo, y eliminar los perfiles que ya no necesite. Utilícelo cuando desee ordenar la lista de perfiles de micrófono o corregir el nombre de un perfil.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El Profile Manager requiere una conexión activa con el equipo.
- Conozca el nombre del perfil que desea renombrar o eliminar.

## Pasos

### Para renombrar un perfil de micrófono

No existe un comando dedicado para renombrar. Renombre un perfil guardándolo con un nombre nuevo y luego eliminando el anterior.

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea renombrar en la lista **Profile list**. El nombre aparece en el campo **Profile name**.
4. Borre el campo **Profile name** y escriba el nombre nuevo.
5. Haga clic en **Save**. El equipo guarda la configuración actual del micrófono con el nombre nuevo y la lista **Profile list** se actualiza.
6. Haga clic en el nombre anterior del perfil en la lista **Profile list**.
7. Haga clic en **Delete**. Aparece un diálogo de confirmación con el mensaje "Delete profile "*nombre*"?".
8. Haga clic en **Yes**.

### Para eliminar un perfil de micrófono

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea eliminar en la lista **Profile list**.
4. Haga clic en **Delete**. Aparece un diálogo de confirmación con el mensaje "Delete profile "*nombre*"?".
5. Haga clic en **Yes**.
6. Haga clic en **Close** cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Pestaña **Microphone** | Pestaña | Muestra la lista de perfiles de micrófono y sus controles. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un perfil. Se rellena automáticamente al seleccionar un perfil de la lista. | — |
| **Profile list** | Lista | Todos los perfiles de micrófono en el equipo; el perfil activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en el equipo. Se activa únicamente cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual del micrófono del equipo con el nombre indicado en **Profile name**. Si el campo está vacío, utiliza el elemento seleccionado en la lista. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras confirmación. Se activa únicamente cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo del Profile Manager. | — |

## Consejos

- Al seleccionar un perfil en la lista **Profile list**, el campo **Profile name** se rellena automáticamente, lo que facilita copiar el nombre antes de editarlo para renombrarlo.
- Los botones Load y Delete permanecen desactivados hasta que seleccione un perfil en la lista **Profile list**.
- La lista de perfiles se actualiza automáticamente cuando el equipo envía una lista actualizada; no es necesario cerrar y volver a abrir el diálogo.

## Solución de problemas

- **Delete aparece en gris** — No hay ningún perfil seleccionado en la lista **Profile list**. Haga clic en el nombre de un perfil para seleccionarlo y, a continuación, haga clic en **Delete**.
- **La lista Profile list está vacía** — Aún no existen perfiles de micrófono en el equipo. Consulte [Crear un perfil de micrófono independiente por micrófono](create-a-separate-mic-profile-per-microphone.md).
- **El perfil guardado no aparece en la lista** — El equipo envía la lista actualizada de forma asíncrona. Espere un momento; la lista se actualizará sin necesidad de cerrar el diálogo.

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Crear un perfil de micrófono independiente por micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
