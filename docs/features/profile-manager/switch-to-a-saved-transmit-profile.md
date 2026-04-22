# Cambiar a un perfil de transmisión guardado

Use el Profile Manager para recuperar un perfil de transmisión guardado previamente y aplicarlo al radio. Esto reemplaza la configuración de transmisión actual del radio con la almacenada en el perfil seleccionado.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión de radio activa.
- Debe existir al menos un perfil de transmisión en el radio. Si la lista de perfiles está vacía, guarde un perfil primero.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña `Transmit (tab)`.
3. En la lista de perfiles, haga clic en el perfil que desea cargar. El nombre del perfil aparece resaltado y el campo `Profile name` se rellena con su nombre.
4. Haga clic en `Load`. El perfil seleccionado se aplica al radio de inmediato.

De forma alternativa, haga doble clic en un perfil de la lista para cargarlo sin necesidad de hacer clic en `Load`.

5. Haga clic en `Close` para cerrar el diálogo.

## Qué hace cada control

| Control | Descripción | Configuración persistente |
|---|---|---|
| `Transmit (tab)` | Muestra todos los perfiles de transmisión almacenados en el radio. El perfil activo actualmente aparece resaltado. | — |
| `Profile name` | Muestra el nombre del perfil seleccionado. Se puede editar al guardar un nuevo perfil. | — |
| Lista de perfiles | Enumera todos los perfiles de transmisión disponibles. Haga clic en una fila para seleccionarla; el perfil activo aparece resaltado. | — |
| `Load` | Aplica el perfil seleccionado al radio. Está deshabilitado hasta que se selecciona un perfil. | — |
| `Save` | Guarda el estado de transmisión actual del radio con el nombre indicado en `Profile name`. No carga un perfil. | — |
| `Delete` | Elimina el perfil seleccionado tras una confirmación. Está deshabilitado hasta que se selecciona un perfil. | — |
| `Close` | Cierra el diálogo Profile Manager. | — |

## Consejos

- Al seleccionar un perfil en la lista se rellena automáticamente el campo `Profile name`. Si luego hace clic en `Save`, el estado actual del radio sobreescribe ese perfil con el mismo nombre. Haga clic en `Load` si solo desea recuperar el perfil sin modificarlo.
- Para que los cambios de transmisión se escriban automáticamente en el perfil activo después de cargarlo, active `Auto-save profile changes` en la pestaña `Auto-Save (tab)`. Esto controla la configuración `AutoSaveTransmitProfile`.

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
