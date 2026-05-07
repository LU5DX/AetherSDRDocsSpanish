# Cambiar a un perfil de transmisión guardado

Cargue un perfil de transmisión previamente guardado en la radio. Esto aplica un conjunto almacenado de parámetros de TX en un solo paso, reemplazando la configuración de transmisión actual.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión en la radio. Si la lista de perfiles está vacía, guarde un perfil primero.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Transmit** para cambiar a la lista de perfiles de transmisión.
3. Haga clic en el perfil que desea cargar en la **Profile list**. El perfil activo se resalta.
4. Haga clic en **Load**.

Alternativamente, haga doble clic en cualquier entrada de la **Profile list** para cargarla sin hacer clic en **Load**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Transmit (tab)** | Pestaña | Cambia el diálogo a la vista de perfiles de transmisión. | — |
| **Profile list** | Lista | Muestra todos los perfiles de transmisión almacenados en la radio. El perfil actualmente activo está resaltado. | — |
| **Profile name** | Campo de texto | Se completa automáticamente al seleccionar un elemento en la lista. Se usa al guardar; no es necesario para cargar. | — |
| **Load** | Botón | Envía el perfil seleccionado a la radio, reemplazando la configuración actual de TX. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual de TX de la radio con el nombre en **Profile name**. | — |
| **Delete** | Botón | Elimina el perfil seleccionado después de la confirmación. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en la configuración de TX se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |

## Consejos

- Seleccionar un perfil en la lista completa el campo **Profile name** con el nombre de ese perfil. Si luego hace clic en **Save**, el estado actual de TX sobrescribe ese perfil con el mismo nombre.
- Si desea que los cambios de TX persistan en el perfil activo sin tener que hacer clic en **Save** cada vez, active **Auto-save profile changes** en la pestaña **Auto-Save**.

## Solución de problemas

- **Load está atenuado** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo y luego haga clic en **Load**.
- **La lista de perfiles está vacía** — Aún no existen perfiles de transmisión en la radio. Use **Save** para crear uno primero.

## Relacionados

- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Profile Manager overview](overview.md)
- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
