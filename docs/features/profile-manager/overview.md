# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar, renombrar y eliminar los tres tipos de perfiles almacenados en la FLEX-8600: Global, Transmit y Microphone. Úselo para guardar y restaurar estados completos de la radio, cambiar entre configuraciones operativas y controlar si los cambios de transmisión se guardan automáticamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — más un botón **Close** en la parte inferior.

**Pestañas Global, Transmit y Microphone**

Cada una de estas tres pestañas tiene la misma disposición:

- Un campo de texto **Profile name** en la parte superior. Escriba un nombre aquí antes de guardar un perfil nuevo, o seleccione un perfil existente de la lista para completar este campo automáticamente.
- Los botones **Load**, **Save** y **Delete**. Load y Delete están deshabilitados hasta que seleccione un perfil en la lista. Seleccionar un perfil también copia su nombre en el campo **Profile name**.
- Una **lista de perfiles** que muestra todos los perfiles guardados para esa categoría. El perfil activo está resaltado. Hacer doble clic en un perfil de la lista lo carga inmediatamente, equivalente a seleccionarlo y hacer clic en **Load**.

Cuando hace clic en **Save**, la radio guarda el estado actual con el nombre del campo **Profile name**. Si el campo está vacío, se usa el nombre del perfil seleccionado actualmente.

Cuando hace clic en **Delete**, aparece un diálogo de confirmación antes de que se elimine el perfil.

La lista de perfiles se actualiza automáticamente cuando la radio reporta un cambio, por lo que las adiciones o eliminaciones realizadas en otro lugar se reflejan sin necesidad de reabrir el diálogo.

**Pestaña Auto-Save**

La pestaña Auto-Save contiene una única casilla de verificación y una breve descripción. Cuando **Auto-save profile changes** está marcada, los cambios en la configuración de TX y micrófono se guardan automáticamente en el perfil activo. Este estado se conserva como `AutoSaveTransmitProfile`. Cuando no está marcada, debe usar **Save** explícitamente para preservar cualquier cambio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Global (pestaña) | Pestaña | Gestiona perfiles globales. | — |
| Transmit (pestaña) | Pestaña | Gestiona perfiles de transmisión. | — |
| Microphone (pestaña) | Pestaña | Gestiona perfiles de micrófono. | — |
| Auto-Save (pestaña) | Pestaña | Controla el guardado automático de perfiles. | — |
| Profile name | Campo de texto | Nombre usado al guardar un perfil nuevo. Se completa automáticamente al seleccionar un perfil. | — |
| Lista de perfiles | Lista | Todos los perfiles para esta categoría; el activo está resaltado. | — |
| Load | Botón | Carga el perfil seleccionado en la radio. Deshabilitado cuando no hay nada seleccionado. | — |
| Save | Botón | Guarda el estado actual de la radio con el nombre escrito, o el nombre seleccionado si el campo está vacío. | — |
| Delete | Botón | Elimina el perfil seleccionado después de la confirmación. Deshabilitado cuando no hay nada seleccionado. | — |
| Auto-save profile changes | Casilla de verificación | Cuando está activada, los cambios de TX y micrófono se guardan automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |
| Close | Botón | Cierra el diálogo. | — |

## Consejos

- Hacer doble clic en un perfil de la lista lo carga inmediatamente sin necesidad de hacer clic en **Load**.
- El campo **Profile name** se completa al seleccionar un perfil, por lo que puede cargar o sobrescribir un perfil sin volver a escribir su nombre.

## Relacionados

- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre se conserven](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Crear un perfil de micrófono separado para cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
