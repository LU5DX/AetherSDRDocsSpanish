# Revisar la lista de perfiles globales activos

El Administrador de perfiles muestra todos los perfiles globales almacenados en la radio y resalta el que está en uso actualmente. Utilícelo cuando desee confirmar qué perfiles existen o identificar el perfil activo antes de cargarlo o eliminarlo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Global** si no está seleccionada.
3. Revise la **Lista de perfiles**. El perfil activo aparece resaltado.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Global** | Pestaña | Muestra la lista de perfiles globales de la radio conectada. |
| **Transmit** | Pestaña | Muestra la lista de perfiles de transmisión de la radio conectada. |
| **Microphone** | Pestaña | Muestra la lista de perfiles de micrófono de la radio conectada. |
| **Auto-Save** | Pestaña | Controla el guardado automático de perfiles de transmisión y micrófono. |
| **Lista de perfiles** | Lista | Muestra todos los perfiles de la pestaña seleccionada. El perfil activo aparece resaltado. |
| **Profile name** | Campo de texto | Nombre que se usa al guardar o crear un nuevo perfil. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. |
| **Save** / **Create** | Botón | En la pestaña **Global**, guarda el estado actual de la radio con el nombre indicado en **Profile name**. En las pestañas **Transmit** o **Microphone**, crea un perfil nuevo; no sobrescribe uno existente. |
| **Delete** | Botón | Elimina el perfil seleccionado después de una confirmación. Solo se habilita cuando hay un perfil seleccionado. |
| **Auto-save profile changes** | Casilla de verificación | Al activarla, los cambios en TX y micrófono se guardan automáticamente en el perfil activo. Clave de configuración: `AutoSaveTransmitProfile`. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- La **Lista de perfiles** se actualiza automáticamente si la radio envía una nueva lista de perfiles mientras el diálogo está abierto. No es necesario cerrar y volver a abrir el diálogo para ver los cambios.
- El perfil activo aparece resaltado en la lista. Si ningún elemento está resaltado, significa que no hay ningún perfil de ese tipo cargado actualmente en la radio.
- En las pestañas **Transmit** y **Microphone**, el botón **Save** se etiqueta como **Create** porque la radio no puede sobrescribir directamente los perfiles de transmisión o micrófono existentes. Las actualizaciones de perfiles existentes se capturan mediante el guardado automático mientras el perfil está activo. Active **Auto-save profile changes** en la pestaña **Auto-Save** para que los cambios sigan al perfil activo.
- Si intenta crear un perfil de transmisión o micrófono con un nombre que ya existe y el guardado automático está desactivado, AetherSDR le pedirá que active el guardado automático para capturar los cambios en ese perfil.
- El menú `Profiles` también muestra una lista dinámica seleccionable de perfiles globales debajo del separador. Allí puede ver el perfil activo de un vistazo sin abrir el Administrador de perfiles.

## Relacionado

- [Descripción general del Administrador de perfiles](overview.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
