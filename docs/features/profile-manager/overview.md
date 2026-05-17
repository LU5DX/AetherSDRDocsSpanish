# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar, renombrar y eliminar los tres tipos de perfiles almacenados en el FLEX-8600: Global, Transmit y Microphone. Úselo para guardar y restaurar estados completos de la radio, cambiar entre configuraciones operativas y controlar si los cambios de transmisión se guardan automáticamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- El cuadro de diálogo del Administrador de perfiles recuerda su tamaño y posición entre sesiones.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El cuadro de diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — más un botón **Close** en la parte inferior.

**Pestañas Global, Transmit y Microphone**

Cada una de estas tres pestañas tiene la misma disposición:

- Un campo de texto **Profile name** en la parte superior. Escriba un nombre aquí antes de guardar o crear un perfil nuevo, o seleccione un perfil existente de la lista para que este campo se complete automáticamente.
- Botones **Load**, **Save** (o **Create**) y **Delete**. Load y Delete están deshabilitados hasta que seleccione un perfil en la lista. Al seleccionar un perfil, su nombre se copia en el campo **Profile name**.
- Una **Profile list** que muestra todos los perfiles guardados para esa categoría. El perfil activo está resaltado. Al hacer doble clic en un perfil de la lista, se carga inmediatamente, lo que equivale a seleccionarlo y hacer clic en **Load**.
- En las pestañas **Transmit** y **Microphone**, una nota informativa debajo de los botones explica el modelo de autoguardado para estos tipos de perfil.

Cuando hace clic en **Save** en la pestaña **Global**, la radio guarda el estado actual con el nombre que está en el campo **Profile name**, sobrescribiendo un perfil existente si ya existe uno con ese nombre. Si el campo está vacío, se utiliza el nombre del perfil seleccionado actualmente.

Cuando hace clic en **Create** en la pestaña **Transmit** o **Microphone**, la radio crea un perfil nuevo con el nombre escrito. No puede sobrescribir un perfil de transmisión o micrófono existente; si ya existe un perfil con ese nombre, aparece un cuadro de diálogo preguntando si desea habilitar Auto-Save para que sus cambios en el perfil existente se capturen automáticamente.

Cuando hace clic en **Delete**, aparece un cuadro de diálogo de confirmación antes de eliminar el perfil.

La lista de perfiles se actualiza automáticamente cuando la radio informa un cambio, por lo que las adiciones o eliminaciones realizadas en otro lugar se reflejan sin necesidad de volver a abrir el cuadro de diálogo.

**Pestaña Auto-Save**

La pestaña Auto-Save contiene una única casilla de verificación y una breve descripción. Cuando **Auto-save profile changes** está marcada, los cambios en la configuración de TX y micrófono se escriben de nuevo en el perfil activo automáticamente. Este estado se conserva como `AutoSaveTransmitProfile`. Cuando no está marcada, debe usar **Save** o **Create** explícitamente para conservar cualquier cambio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Global (pestaña) | Pestaña | Administra perfiles globales. | — |
| Transmit (pestaña) | Pestaña | Administra perfiles de transmisión. | — |
| Microphone (pestaña) | Pestaña | Administra perfiles de micrófono. | — |
| Auto-Save (pestaña) | Pestaña | Controla el guardado automático de perfiles. | — |
| Profile name | Campo de texto | Nombre que se usa al guardar un perfil nuevo. Se completa automáticamente al seleccionar un perfil. | — |
| Profile list | Lista | Todos los perfiles para esta categoría; el activo está resaltado. | — |
| Load | Botón | Carga el perfil seleccionado en la radio. Deshabilitado cuando no hay nada seleccionado. | — |
| Save | Botón | Solo en la pestaña Global. Guarda el estado actual de la radio con el nombre escrito, sobrescribiendo un perfil existente si ya existe uno con ese nombre. | — |
| Create | Botón | Solo en las pestañas Transmit y Microphone. Crea un perfil nuevo con el nombre escrito. No puede sobrescribir un perfil existente; si se produce una colisión de nombres, un cuadro de diálogo ofrece habilitar Auto-Save. | — |
| Delete | Botón | Elimina el perfil seleccionado después de la confirmación. Deshabilitado cuando no hay nada seleccionado. | — |
| Auto-save profile changes | Casilla de verificación | Cuando está habilitada, los cambios de TX y micrófono se escriben de nuevo en el perfil activo automáticamente. | `AutoSaveTransmitProfile` |
| Close | Botón | Cierra el cuadro de diálogo. | — |

## Consejos

- Al hacer doble clic en un perfil de la lista, se carga inmediatamente sin necesidad de hacer clic en **Load**.
- El campo **Profile name** se completa al seleccionar un perfil, por lo que puede cargar o sobrescribir un perfil sin volver a escribir su nombre.
- En las pestañas **Transmit** y **Microphone**, el botón **Save** está etiquetado como **Create** porque la radio no puede sobrescribir directamente perfiles de transmisión o micrófono existentes; los cambios se capturan mediante Auto-Save mientras el perfil está activo.
- Si ve un cuadro de diálogo al hacer clic en **Create** en una pestaña de transmisión o micrófono que indica que un perfil ya existe, puede hacer clic en **Enable Auto-Save** para activar el guardado automático sin cambiar a la pestaña **Auto-Save**.

## Relacionados

- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Create a separate mic profile per microphone](create-a-separate-mic-profile-per-microphone.md)
- [Rename or delete a microphone profile](rename-or-delete-a-microphone-profile.md)
- [Review the list of active global profiles](review-the-list-of-active-global-profiles.md)
