# Cambiar a un perfil de transmisión guardado

Cargue un perfil de transmisión previamente guardado en el radio. Esto aplica un conjunto almacenado de parámetros de TX en un solo paso, reemplazando la configuración de transmisión actual.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Debe existir al menos un perfil de transmisión en el radio. Si la lista de perfiles está vacía, guarde un perfil primero.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Transmit (tab)** para cambiar a la lista de perfiles de transmisión.
3. Haga clic en el perfil que desea cargar en la **Profile list**. El perfil activo aparece resaltado.
4. Haga clic en **Load**.

De forma alternativa, haga doble clic en cualquier entrada de la **Profile list** para cargarlo sin necesidad de hacer clic en **Load**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Transmit (tab)** | Pestaña | Cambia el diálogo a la vista de perfiles de transmisión. | — |
| **Profile list** | Lista | Muestra todos los perfiles de transmisión almacenados en el radio. El perfil activo aparece resaltado. | — |
| **Profile name** | Campo de texto | Se completa automáticamente al seleccionar un elemento de la lista. Se usa al guardar; no es necesario para cargar. | — |
| **Load** | Botón | Envía el perfil seleccionado al radio, reemplazando la configuración de TX actual. Solo se activa cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado de TX actual del radio con el nombre indicado en **Profile name**. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras confirmación. Solo se activa cuando hay un perfil seleccionado. | — |
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en la configuración de TX se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |

## Consejos

- Al seleccionar un perfil en la lista, el campo **Profile name** se completa con el nombre de ese perfil. Si luego hace clic en **Save**, el estado de TX actual sobreescribe ese perfil con el mismo nombre.
- Si desea que los cambios de TX persistan en el perfil activo sin tener que hacer clic en **Save** manualmente cada vez, active **Auto-save profile changes** en la pestaña **Auto-Save (tab)**.

## Solución de problemas

- **Load aparece atenuado** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en el nombre de un perfil para seleccionarlo y, a continuación, haga clic en **Load**.
- **La Profile list está vacía** — Aún no existen perfiles de transmisión en el radio. Use **Save** para crear uno primero.

## Relacionado

- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Descripción general del Profile Manager](overview.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
