# Resumen del Administrador de Perfiles

El Administrador de Perfiles le permite crear, cargar, renombrar y eliminar los tres tipos de perfiles almacenados en el FLEX-8600: Global, Transmisión y Micrófono. Úselo para guardar y restaurar estados completos de la radio, cambiar entre configuraciones operativas y controlar si los cambios de transmisión se guardan automáticamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de Perfiles requiere una conexión activa con la radio.
- El diálogo del Administrador de Perfiles recuerda su tamaño y posición entre sesiones.

## Cómo funciona

Abra el Administrador de Perfiles desde `Profiles > Profile Manager...`. El diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — además de un botón **Close** en la parte inferior.

**Pestañas Global, Transmit y Microphone**

Cada una de estas tres pestañas tiene la misma disposición:

- Un campo de texto **Profile name** en la parte superior. Escriba un nombre aquí antes de guardar o crear un nuevo perfil, o seleccione un perfil existente de la lista para rellenar este campo automáticamente.
- Botones **Load**, **Save** (o **Create**) y **Delete**. Los botones Load y Delete están deshabilitados hasta que seleccione un perfil en la lista. Seleccionar un perfil también copia su nombre en el campo **Profile name**.
- Una **Profile list** que muestra todos los perfiles guardados para esa categoría. El perfil activo está resaltado. Haga doble clic en un perfil de la lista para cargarlo inmediatamente, equivalente a seleccionarlo y hacer clic en **Load**.
- En las pestañas **Transmit** y **Microphone**, una nota informativa debajo de los botones explica el modelo de guardado automático para estos tipos de perfil.

Cuando hace clic en **Save** en la pestaña **Global**, la radio guarda el estado actual bajo el nombre del campo **Profile name**, sobrescribiendo un perfil existente si ya existe uno con ese nombre. Si el campo está vacío, se utiliza el nombre del perfil seleccionado actualmente.

Cuando hace clic en **Create** en la pestaña **Transmit** o **Microphone**, la radio crea un nuevo perfil con el nombre escrito. No puede sobrescribir un perfil de transmisión o micrófono existente; si ya existe un perfil con ese nombre, aparece un diálogo preguntando si desea habilitar Auto-Save para que sus cambios en el perfil existente se capturen automáticamente.

Cuando hace clic en **Delete**, aparece un diálogo de confirmación antes de eliminar el perfil.

La lista de perfiles se actualiza automáticamente cuando la radio reporta un cambio, por lo que las adiciones o eliminaciones realizadas desde otro lugar se reflejan sin necesidad de volver a abrir el diálogo.

**Pestaña Auto-Save**

La pestaña Auto-Save contiene una única casilla de verificación y una breve descripción. Cuando **Auto-save profile changes** está marcado, los cambios en la configuración de TX y micrófono se escriben automáticamente en el perfil activo. Este estado se persiste como `AutoSaveTransmitProfile`. Cuando no está marcado, debe usar **Save** o **Create** explícitamente para conservar cualquier cambio.

La casilla de verificación se sincroniza automáticamente con el estado de guardado automático de la radio. Los cambios realizados desde cualquier fuente — la confirmación "Enable Auto-Save" del diálogo de perfiles, clientes TCI, cargas de perfiles o clientes remotos de SmartSDR — se reflejan en la casilla de verificación sin necesidad de volver a abrir el diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Global (pestaña) | Pestaña | Administra perfiles globales. | — |
| Transmit (pestaña) | Pestaña | Administra perfiles de transmisión. | — |
| Microphone (pestaña) | Pestaña | Administra perfiles de micrófono. | — |
| Auto-Save (pestaña) | Pestaña | Controla el guardado automático de perfiles. | — |
| Profile name | Campo de texto | Nombre usado al guardar un nuevo perfil. Se rellena automáticamente al seleccionar un perfil. | — |
| Profile list | Lista | Todos los perfiles de esta categoría; el activo está resaltado. | — |
| Load | Botón | Carga el perfil seleccionado en la radio. Deshabilitado cuando no hay nada seleccionado. | — |
| Save | Botón | Solo en la pestaña Global. Guarda el estado actual de la radio bajo el nombre escrito, sobrescribiendo un perfil existente si ya existe uno con ese nombre. | — |
| Create | Botón | Solo en las pestañas Transmit y Microphone. Crea un nuevo perfil con el nombre escrito. No puede sobrescribir un perfil existente; si hay una colisión de nombres, un diálogo ofrece habilitar Auto-Save. | — |
| Delete | Botón | Elimina el perfil seleccionado después de la confirmación. Deshabilitado cuando no hay nada seleccionado. | — |
| Auto-save profile changes | Casilla de verificación | Cuando está habilitado, los cambios de TX y micrófono se escriben automáticamente en el perfil activo. Se sincroniza con el estado de la radio desde cualquier fuente. | `AutoSaveTransmitProfile` |
| Close | Botón | Cierra el diálogo. | — |

## Consejos

- Haga doble clic en un perfil de la lista para cargarlo inmediatamente sin necesidad de hacer clic en **Load**.
- El campo **Profile name** se rellena al seleccionar un perfil, por lo que puede cargar o sobrescribir un perfil sin volver a escribir su nombre.
- En las pestañas **Transmit** y **Microphone**, el botón **Save** está etiquetado como **Create** porque la radio no puede sobrescribir directamente perfiles de transmisión o micrófono existentes; los cambios se capturan mediante Auto-Save mientras el perfil está activo.
- Si al hacer clic en **Create** en una pestaña de transmisión o micrófono aparece un diálogo indicando que el perfil ya existe, puede hacer clic en **Enable Auto-Save** para activar el guardado automático sin cambiar a la pestaña **Auto-Save**.
- La casilla de verificación Auto-Save se actualiza automáticamente cuando el guardado automático se habilita o deshabilita por cualquier medio — una carga de perfil, un comando TCI, un cliente remoto o el diálogo de confirmación en las pestañas Transmit/Microphone.

## Relacionados

- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Create a separate mic profile per microphone](create-a-separate-mic-profile-per-microphone.md)
- [Rename or delete a microphone profile](rename-or-delete-a-microphone-profile.md)
- [Review the list of active global profiles](review-the-list-of-active-global-profiles.md)
