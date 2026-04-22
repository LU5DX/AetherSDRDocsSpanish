# Revisar la lista de perfiles globales activos

El Profile Manager muestra todos los perfiles globales almacenados en el radio, con el perfil activo resaltado. Utilícelo para ver qué perfiles existen y cuál está cargado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña `Global (tab)` si no está seleccionada aún.
3. Lea la `Profile list`. Aquí se muestran todos los perfiles globales almacenados en el radio. El perfil activo aparece resaltado.

## Qué hace cada control

| Control | Descripción |
|---|---|
| `Global (tab)` | Cambia el diálogo a la gestión de perfiles globales. |
| Profile list | Muestra todos los perfiles globales del radio. El perfil activo aparece resaltado. Al seleccionar una entrada, se rellena el campo `Profile name` y se habilitan `Load` y `Delete`. |
| `Load` | Carga el perfil seleccionado en el radio. También se activa haciendo doble clic sobre un perfil de la lista. |
| `Save` | Guarda el estado actual del radio con el nombre introducido en `Profile name`. |
| `Delete` | Elimina el perfil seleccionado tras una confirmación. |
| `Profile name` | Campo de texto utilizado para asignar un nombre al perfil antes de guardarlo. Se rellena automáticamente al seleccionar un perfil de la lista. |
| `Close` | Cierra el diálogo. |

## Consejos

- La lista de perfiles se actualiza automáticamente si el radio notifica un cambio mientras el diálogo está abierto. No es necesario cerrar y volver a abrir el diálogo para ver la lista actualizada.
- El menú `Profiles` también muestra una lista dinámica de perfiles globales debajo de un separador. Cada entrada es seleccionable e indica el perfil actualmente cargado sin necesidad de abrir el Profile Manager.

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
