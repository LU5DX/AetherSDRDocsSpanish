# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar, renombrar y eliminar los tres tipos de perfiles almacenados en el FLEX-8600: Global, Transmit y Microphone. Úselo para guardar y restaurar estados completos del radio, cambiar entre configuraciones de operación y controlar si los cambios de transmisión se guardan automáticamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Administrador de perfiles requiere una conexión activa con el radio.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El cuadro de diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — más un botón **Close** en la parte inferior.

**Pestañas Global, Transmit y Microphone**

Cada una de estas tres pestañas tiene el mismo diseño:

- Un campo de texto **Profile name** en la parte superior. Escriba un nombre aquí antes de guardar un nuevo perfil, o seleccione un perfil existente de la lista para completar este campo automáticamente.
- Botones **Load**, **Save** y **Delete**. Load y Delete permanecen deshabilitados hasta que seleccione un perfil en la lista. Al seleccionar un perfil también se copia su nombre en el campo **Profile name**.
- Una **Profile list** que muestra todos los perfiles guardados para esa categoría. El perfil activo aparece resaltado. Hacer doble clic en un perfil de la lista lo carga de inmediato, equivalente a seleccionarlo y hacer clic en **Load**.

Al hacer clic en **Save**, el radio guarda el estado actual con el nombre indicado en el campo **Profile name**. Si el campo está vacío, se utiliza el nombre del perfil seleccionado actualmente.

Al hacer clic en **Delete**, aparece un cuadro de diálogo de confirmación antes de eliminar el perfil.

La lista de perfiles se actualiza automáticamente cuando el radio reporta un cambio, por lo que las adiciones o eliminaciones realizadas en otro lugar se reflejan sin necesidad de volver a abrir el cuadro de diálogo.

**Pestaña Auto-Save**

La pestaña Auto-Save contiene una sola casilla de verificación y una breve descripción. Cuando **Auto-save profile changes** está marcada, los cambios en la configuración de TX y micrófono se escriben de vuelta al perfil activo automáticamente. Este estado se conserva como `AutoSaveTransmitProfile`. Cuando está desmarcada, debe usar **Save** explícitamente para conservar cualquier cambio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Global (tab) | Pestaña | Administra perfiles globales. | — |
| Transmit (tab) | Pestaña | Administra perfiles de transmisión. | — |
| Microphone (tab) | Pestaña | Administra perfiles de micrófono. | — |
| Auto-Save (tab) | Pestaña | Controla el guardado automático de perfiles. | — |
| Profile name | Campo de texto | Nombre utilizado al guardar un nuevo perfil. Se completa automáticamente cuando se selecciona un perfil. | — |
| Profile list | Lista | Todos los perfiles de esta categoría; el activo aparece resaltado. | — |
| Load | Botón | Carga el perfil seleccionado en el radio. Deshabilitado cuando no hay nada seleccionado. | — |
| Save | Botón | Guarda el estado actual del radio con el nombre escrito, o con el nombre seleccionado si el campo está vacío. | — |
| Delete | Botón | Elimina el perfil seleccionado después de confirmación. Deshabilitado cuando no hay nada seleccionado. | — |
| Auto-save profile changes | Casilla de verificación | Cuando está habilitada, los cambios de TX y micrófono se escriben de vuelta al perfil activo automáticamente. | `AutoSaveTransmitProfile` |
| Close | Botón | Cierra el cuadro de diálogo. | — |

## Consejos

- Hacer doble clic en un perfil de la lista lo carga de inmediato sin necesidad de hacer clic en **Load**.
- El campo **Profile name** se completa al seleccionar un perfil, por lo que puede cargar o sobrescribir un perfil sin necesidad de volver a escribir su nombre.

## Temas relacionados

- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre se conserven](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Crear un perfil de micrófono independiente por cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
