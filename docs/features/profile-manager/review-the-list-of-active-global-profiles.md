# Revisar la lista de perfiles globales activos

El Administrador de perfiles muestra todos los perfiles globales almacenados en la radio y resalta el que está actualmente en uso. Utilícelo cuando desee confirmar qué perfiles existen o identificar el perfil activo antes de cargarlo o eliminarlo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Global (tab)** si no está seleccionada.
3. Revise la **Lista de perfiles**. El perfil activo está resaltado.

## Funciones de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Global (tab)** | Pestaña | Muestra la lista de perfiles globales de la radio conectada. |
| **Transmit (tab)** | Pestaña | Muestra la lista de perfiles de transmisión de la radio conectada. |
| **Microphone (tab)** | Pestaña | Muestra la lista de perfiles de micrófono de la radio conectada. |
| **Auto-Save (tab)** | Pestaña | Controla el guardado automático de perfiles de transmisión y micrófono. |
| **Lista de perfiles** | Lista | Muestra todos los perfiles de la pestaña seleccionada. El perfil activo actualmente está resaltado. |
| **Nombre del perfil** | Campo de texto | Nombre utilizado al guardar o crear un nuevo perfil. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. |
| **Save** / **Create** | Botón | En la pestaña **Global (tab)**, guarda el estado actual de la radio con el nombre indicado en **Nombre del perfil**. En las pestañas **Transmit (tab)** o **Microphone (tab)**, crea un nuevo perfil; no sobrescribe uno existente. |
| **Delete** | Botón | Elimina el perfil seleccionado después de un mensaje de confirmación. Solo se habilita cuando hay un perfil seleccionado. |
| **Auto-save profile changes** | Casilla de verificación | Cuando está activada, los cambios en TX y micrófono se guardan automáticamente en el perfil activo. Clave de configuración: `AutoSaveTransmitProfile`. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

## Consejos

- La **Lista de perfiles** se actualiza automáticamente si la radio envía una nueva lista de perfiles mientras el cuadro de diálogo está abierto. No es necesario cerrar y volver a abrir el cuadro de diálogo para ver los cambios.
- El perfil activo aparece resaltado en la lista. Si ningún elemento está resaltado, significa que no hay ningún perfil de ese tipo cargado actualmente en la radio.
- En las pestañas **Transmit (tab)** y **Microphone (tab)**, el botón **Save** se llama **Create** porque la radio no puede sobrescribir directamente los perfiles de transmisión o micrófono existentes. Las actualizaciones a perfiles existentes se capturan mediante el guardado automático (Auto-Save) mientras el perfil está activo. Active la opción **Auto-save profile changes** en la pestaña **Auto-Save (tab)** para que los cambios sigan al perfil activo.
- Si intenta crear un perfil de transmisión o micrófono con un nombre que ya existe y el guardado automático está desactivado, AetherSDR le pedirá que active el guardado automático para que sus cambios en ese perfil se capturen.
- La casilla **Auto-save profile changes** se mantiene sincronizada con el estado de guardado automático de la radio, incluso si ese estado cambia fuera del cuadro de diálogo. Por ejemplo, si activa el guardado automático mediante el mensaje "Enable Auto-Save" o si un cliente SmartSDR o TCI remoto lo cambia, la casilla se actualiza para coincidir.
- El menú `Profiles` también muestra una lista dinámica con casillas de verificación de los perfiles globales debajo del separador. Puede ver el perfil activo de un vistazo sin abrir el Administrador de perfiles.

## Relacionado

- [Descripción general del Administrador de perfiles](overview.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
