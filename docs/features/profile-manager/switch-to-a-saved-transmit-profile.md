# Cambiar a un perfil de transmisión guardado

Cargue un perfil de transmisión previamente guardado en la radio. Esto aplica un conjunto de parámetros de TX almacenados en un solo paso, reemplazando la configuración de transmisión actual.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión en la radio. Si la lista de perfiles está vacía, cree un perfil primero.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Transmit** para cambiar a la lista de perfiles de transmisión.
3. Haga clic en el perfil que desea cargar en la **lista de perfiles**. El perfil activo se resalta.
4. Haga clic en **Load**.

Alternativamente, haga doble clic en cualquier entrada de la **lista de perfiles** para cargarla sin usar el botón **Load**.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Global (tab)** | Pestaña | Cambia el diálogo a la vista de perfil global. | — |
| **Transmit (tab)** | Pestaña | Cambia el diálogo a la vista de perfiles de transmisión. | — |
| **Microphone (tab)** | Pestaña | Cambia el diálogo a la vista de perfiles de micrófono. | — |
| **Auto-Save (tab)** | Pestaña | Cambia el diálogo a la vista de configuración de guardado automático. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un nuevo perfil. | — |
| **Profile list** | Lista | Muestra todos los perfiles de la categoría seleccionada almacenados en la radio. El perfil activo actual se resalta. | — |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre ingresado. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras la confirmación. Solo se habilita cuando hay un perfil seleccionado. | — |
| **Auto-save profile changes** | Casilla de verificación | Cuando está activada, los cambios de TX se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |
| **Close** | Botón | Cierra el diálogo. | — |

## Notas

- El botón para guardar perfiles se etiqueta **Save**, no **Create**. Para actualizar un perfil existente, active **Auto-save profile changes** en la pestaña **Auto-Save** — los cambios al perfil activo se capturarán automáticamente.
- La casilla **Auto-save profile changes** se sincroniza automáticamente con la radio. Los cambios realizados fuera del diálogo (por clientes TCI, carga de perfiles o clientes SmartSDR remotos) actualizarán el estado de la casilla.
- Si intenta guardar un perfil con un nombre que ya existe y el guardado automático está desactivado, un diálogo le ofrecerá activar el guardado automático para que los cambios futuros al perfil se capturen.

## Consejos

- Al seleccionar un perfil en la lista, el campo **Profile name** se rellena con el nombre de ese perfil. Si ingresa un nombre diferente y hace clic en **Save**, se crea un nuevo perfil con ese nombre.
- Para persistir los cambios de TX al perfil de transmisión activo sin guardado manual, active **Auto-save profile changes** en la pestaña **Auto-Save**.

## Solución de problemas

- **Load está atenuado** — No hay ningún perfil seleccionado en la **lista de perfiles**. Haga clic en un nombre de perfil para seleccionarlo, luego haga clic en **Load**.
- **La lista de perfiles está vacía** — Aún no existen perfiles para la categoría seleccionada en la radio. Use **Save** para crear uno primero.
- **Al hacer clic en Save no ocurre nada para un nombre existente** — La radio no puede sobrescribir perfiles directamente. Active el guardado automático para que sus cambios se capturen automáticamente, o realice cambios manualmente mientras el perfil está activo y el guardado automático está encendido.

## Relacionados

- [Activar el guardado automático para que los ajustes de TX persistan siempre](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Visión general del Administrador de perfiles](overview.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
