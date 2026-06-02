# Revisar la lista de perfiles globales activos

El Administrador de Perfiles muestra todos los perfiles globales almacenados en la radio y resalta el que está en uso actualmente. Úselo cuando desee confirmar qué perfiles existen o identificar el activo antes de cargarlo o eliminarlo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de Perfiles requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo del Administrador de Perfiles.
2. Haga clic en la pestaña **Global (tab)** si aún no está seleccionada.
3. Revise la **Profile list**. El perfil activo aparece resaltado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Global (tab)** | Pestaña | Muestra la lista de perfiles globales de la radio conectada. |
| **Transmit (tab)** | Pestaña | Muestra la lista de perfiles de transmisión de la radio conectada. |
| **Microphone (tab)** | Pestaña | Muestra la lista de perfiles de micrófono de la radio conectada. |
| **Auto-Save (tab)** | Pestaña | Controla el guardado automático de perfiles de transmisión y micrófono. |
| **Profile list** | Lista | Muestra todos los perfiles de la pestaña seleccionada. El perfil activo actual aparece resaltado. |
| **Profile name** | Campo de texto | Nombre que se usa al guardar o crear un nuevo perfil. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo está habilitado cuando hay un perfil seleccionado. |
| **Save** / **Create** | Botón | En la pestaña **Global (tab)**, guarda el estado actual de la radio con el nombre que aparece en **Profile name**. En las pestañas **Transmit (tab)** o **Microphone (tab)**, crea un nuevo perfil; no sobrescribe uno existente. |
| **Delete** | Botón | Elimina el perfil seleccionado después de un mensaje de confirmación. Solo está habilitado cuando hay un perfil seleccionado. |
| **Auto-save profile changes** | Casilla de verificación | Cuando está activada, los cambios de TX y micrófono se escriben automáticamente en el perfil activo. Clave de configuración: `AutoSaveTransmitProfile`. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

## Consejos

- La **Profile list** se actualiza automáticamente si la radio envía una nueva lista de perfiles mientras el diálogo está abierto. No es necesario cerrar y volver a abrir el diálogo para ver los cambios.
- El perfil activo se muestra resaltado en la lista. Si no aparece ningún elemento resaltado, significa que no hay ningún perfil de ese tipo cargado actualmente en la radio.
- En las pestañas **Transmit (tab)** y **Microphone (tab)**, el botón **Save** se llama **Create** porque la radio no puede sobrescribir directamente los perfiles de transmisión o micrófono existentes. Las actualizaciones de perfiles existentes se capturan mediante Auto-Save mientras el perfil está activo. Active **Auto-save profile changes** en la pestaña **Auto-Save (tab)** para que los cambios sigan al perfil activo.
- Si intenta crear un perfil de transmisión o micrófono con un nombre que ya existe y Auto-Save está desactivado, AetherSDR le pedirá que active Auto-Save para que se capturen sus cambios en ese perfil.
- La casilla **Auto-save profile changes** se mantiene sincronizada con el estado de Auto-Save de la radio, incluso si ese estado cambia desde fuera del diálogo. Por ejemplo, si activa Auto-Save mediante el mensaje "Enable Auto-Save" o si un cliente remoto SmartSDR o TCI lo cambia, la casilla se actualiza para coincidir.
- El menú `Profiles` también muestra una lista dinámica seleccionable de perfiles globales debajo del separador. Puede ver el perfil activo de un vistazo allí sin abrir el Administrador de Perfiles.

## Relacionados

- [Profile Manager overview](overview.md)
- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
