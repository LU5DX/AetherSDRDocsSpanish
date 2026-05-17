# Cambiar a un perfil de transmisión guardado

Cargue un perfil de transmisión previamente guardado en la radio. Esto aplica un conjunto almacenado de parámetros de TX en un solo paso, reemplazando la configuración de transmisión actual.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión en la radio. Si la lista de perfiles está vacía, cree un perfil primero.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Transmit** para cambiar a la lista de perfiles de transmisión.
3. Haga clic en el perfil que desea cargar en la **Profile list**. El perfil activo se resalta.
4. Haga clic en **Load**.

Alternativamente, haga doble clic en cualquier entrada de la **Profile list** para cargarla sin hacer clic en **Load**.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Transmit (tab)** | Pestaña | Cambia el cuadro de diálogo a la vista de perfiles de transmisión. | — |
| **Profile list** | Lista | Muestra todos los perfiles de transmisión almacenados en la radio. El perfil activo se resalta. | — |
| **Profile name** | Campo de texto | Se completa automáticamente al seleccionar un elemento de la lista. Se usa al crear un nuevo perfil. | — |
| **Load** | Botón | Envía el perfil seleccionado a la radio, reemplazando la configuración de TX actual. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Create** | Botón | Crea un nuevo perfil de transmisión con el nombre ingresado en **Profile name**. No sobrescribe un perfil existente; use Auto-Save para capturar cambios en un perfil existente. | — |
| **Delete** | Botón | Elimina el perfil seleccionado después de la confirmación. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en la configuración de TX se guardan automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |

## Notas

- El botón para crear perfiles de transmisión se llama **Create**, no **Save**. La API de FlexRadio no permite sobrescribir directamente un perfil de transmisión existente. Para actualizar un perfil existente, active **Auto-save profile changes** en la pestaña **Auto-Save (tab)**; los cambios en el perfil activo se capturarán automáticamente.
- Si hace clic en **Create** con un nombre que ya existe, un cuadro de diálogo explica que la sobrescritura no es compatible. Puede activar Auto-Save desde ese cuadro de diálogo para que los cambios futuros en el perfil se capturen.

## Consejos

- Seleccionar un perfil en la lista llena el campo **Profile name** con el nombre de ese perfil. Si ingresa un nombre diferente y hace clic en **Create**, se crea un nuevo perfil con ese nombre.
- Para guardar cambios de TX en el perfil de transmisión activo sin guardar manualmente, active **Auto-save profile changes** en la pestaña **Auto-Save (tab)**.

## Solución de problemas

- **Load está atenuado** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo, luego haga clic en **Load**.
- **La Profile list está vacía** — Aún no existen perfiles de transmisión en la radio. Use **Create** para crear uno primero.
- **Hacer clic en Create no hace nada para un nombre existente** — La radio no puede sobrescribir perfiles de transmisión. Active Auto-Save para que los cambios se capturen automáticamente, o realice cambios manualmente mientras el perfil está activo y Auto-Save está activado.

## Relacionado

- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Profile Manager overview](overview.md)
- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
