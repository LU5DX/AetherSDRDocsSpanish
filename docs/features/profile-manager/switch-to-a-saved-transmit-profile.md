# Cambiar a un perfil de transmisión guardado

Use esta página para aplicar un perfil de transmisión guardado anteriormente al radio. Cargar un perfil de transmisión restaura los ajustes de TX almacenados bajo el nombre de ese perfil.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Profile Manager requiere una conexión activa con el radio.
- Debe existir al menos un perfil de transmisión en el radio. Si la lista de perfiles está vacía, consulte [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md) para saber cómo crear y guardar perfiles.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña `Transmit (tab)`.
3. En la lista de perfiles, haga clic en el perfil que desea cargar. El perfil activo aparece resaltado.
4. Haga clic en `Load`.

Alternativamente, haga doble clic en el nombre de un perfil de la lista para cargarlo inmediatamente sin necesidad de hacer clic en `Load`.

5. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento | Ajuste persistente |
|---|---|---|---|
| `Transmit (tab)` | Pestaña | Muestra todos los perfiles de transmisión almacenados en el radio. | — |
| Lista de perfiles | Lista | Muestra todos los perfiles de transmisión; el perfil actualmente activo aparece resaltado. Haga clic en un nombre para seleccionarlo. | — |
| Nombre de perfil | Campo de texto | Se rellena automáticamente al seleccionar un perfil de la lista. | — |
| `Load` | Botón | Envía el perfil seleccionado al radio, reemplazando los ajustes de TX actuales. Se habilita solo cuando hay un perfil seleccionado. | — |
| `Save` | Botón | Guarda el estado de TX actual del radio bajo el nombre indicado en el campo de nombre de perfil. | — |
| `Delete` | Botón | Elimina el perfil seleccionado tras confirmación. Se habilita solo cuando hay un perfil seleccionado. | — |
| `Close` | Botón | Cierra el diálogo Profile Manager. | — |

## Sugerencias

- Al seleccionar un perfil en la lista, el campo de nombre de perfil se rellena automáticamente con el nombre de ese perfil. Si luego hace clic en `Save`, el radio sobreescribe ese perfil con el estado de TX actual.
- Para que los cambios de TX se escriban automáticamente en el perfil activo después de cargarlo, habilite `Auto-save profile changes` en la pestaña `Auto-Save (tab)`. Esto se controla mediante el ajuste `AutoSaveTransmitProfile`.

## Relacionado

- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Descripción general de Profile Manager](overview.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
