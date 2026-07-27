# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar, renombrar y eliminar los tres tipos de perfiles almacenados en el FLEX-8600: Global, Transmit y Microphone. Úselo para guardar y restaurar estados completos de la radio, cambiar entre configuraciones operativas y controlar si los cambios de transmisión se guardan automáticamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- El cuadro de diálogo del Administrador de perfiles recuerda su tamaño y posición entre sesiones.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El cuadro de diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — además de un botón **Close** en la parte inferior.

**Pestañas Global, Transmit y Microphone**

Cada una de estas tres pestañas tiene la misma disposición:

- Un campo de texto **Profile name** en la parte superior. Escriba un nombre aquí antes de guardar o crear un nuevo perfil, o seleccione un perfil existente de la lista para rellenar este campo automáticamente. El botón **Save** (o **Create**) está deshabilitado cuando el campo de nombre está vacío, lo que evita clics accidentales sin destino.
- Botones **Load**, **Save** (o **Create**) y **Delete**. Load y Delete están deshabilitados hasta que seleccione un perfil en la lista. Seleccionar un perfil también copia su nombre en el campo **Profile name**.
- Una línea de estado de resultado debajo de los botones. Esta línea aparece momentáneamente para confirmar un guardado exitoso o mostrar un mensaje de error. Desaparece cuando comienza a escribir en el campo **Profile name** o carga un perfil diferente.
- Una **lista de perfiles** que muestra todos los perfiles guardados para esa categoría. El perfil activo está resaltado. Al hacer doble clic en un perfil de la lista, se carga inmediatamente, equivalente a seleccionarlo y hacer clic en **Load**.
- En las pestañas **Transmit** y **Microphone**, una nota informativa debajo de los botones explica el modelo de guardado automático para estos tipos de perfiles.

Al hacer clic en **Save** en la pestaña **Global**, la radio guarda el estado actual bajo el nombre en el campo **Profile name**, sobrescribiendo un perfil existente si ya existe uno con ese nombre. Si el campo está vacío, se utiliza el nombre del perfil seleccionado actualmente. Aparece un mensaje de estado que confirma el éxito o informa de un error.

Al hacer clic en **Create** en la pestaña **Transmit** o **Microphone**, la radio crea un nuevo perfil con el nombre escrito. No puede sobrescribir un perfil de transmisión o micrófono existente; si ya existe un perfil con ese nombre, aparece un cuadro de diálogo preguntando si desea habilitar Auto-Save para que los cambios en el perfil existente se capturen automáticamente.

Al hacer clic en **Delete**, aparece un cuadro de diálogo de confirmación antes de eliminar el perfil.

La lista de perfiles se actualiza automáticamente cuando la radio informa de un cambio, por lo que las adiciones o eliminaciones realizadas en otro lugar se reflejan sin tener que reabrir el cuadro de diálogo.

**Pestaña Auto-Save**

La pestaña Auto-Save contiene una sola casilla de verificación y una breve descripción. Cuando **Auto-save profile changes** está marcada, los cambios en la configuración de TX y micrófono se escriben automáticamente en el perfil activo. Este estado se lee en vivo del modelo de la radio, no de AppSettings locales. Cuando no está marcada, debe usar **Save** o **Create** explícitamente para conservar cualquier cambio.

La casilla de verificación se sincroniza automáticamente con el estado de guardado automático de la radio. Los cambios realizados desde cualquier fuente (la confirmación "Enable Auto-Save" del cuadro de diálogo de perfiles, clientes TCI, cargas de perfiles o clientes SmartSDR remotos) se reflejan en la casilla de verificación sin necesidad de reabrir el cuadro de diálogo.

## Qué hace cada control

| Control                  | Tipo                                                                                                                                                                                                                            | Comportamiento                                                                                                                                                                                    |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Global (pestaña)         | Pestaña                                                                                                                                                                                                                        | Administra los perfiles globales.                                                                                                                                                                 |
| Transmit (pestaña)       | Pestaña                                                                                                                                                                                                                        | Administra los perfiles de transmisión.                                                                                                                                                           |
| Microphone (pestaña)     | Pestaña                                                                                                                                                                                                                        | Administra los perfiles de micrófono.                                                                                                                                                             |
| Auto-Save (pestaña)      | Pestaña                                                                                                                                                                                                                        | Controla el guardado automático de perfiles.                                                                                                                                                      |
| Profile name             | Campo de texto                                                                                                                                                                                                                 | Nombre utilizado al guardar un nuevo perfil. Se rellena automáticamente al seleccionar un perfil. Habilita o deshabilita el botón Save/Create a medida que se escribe o borra texto. Escribir borra cualquier resultado de estado de un guardado anterior. |
| Lista de perfiles        | Lista                                                                                                                                                                                                                          | Todos los perfiles para esta categoría; el activo está resaltado.                                                                                                                                 |
| Load                     | Botón                                                                                                                                                                                                                          | Carga el perfil seleccionado en la radio. Deshabilitado cuando no hay nada seleccionado. Borra la línea de estado.                                                                                 |
| Save                     | Botón                                                                                                                                                                                                                          | Solo en la pestaña Global. Guarda el estado actual de la radio bajo el nombre escrito, sobrescribiendo un perfil existente si ya existe uno con ese nombre. Deshabilitado cuando el campo de nombre está vacío. Muestra un mensaje de estado al completarse o si hay error. |
| Create                   | Botón                                                                                                                                                                                                                          | Solo en las pestañas Transmit y Microphone. Crea un nuevo perfil con el nombre escrito. No puede sobrescribir un perfil existente; si hay una colisión de nombre, un cuadro de diálogo ofrece habilitar Auto-Save. Deshabilitado cuando el campo de nombre está vacío. Muestra un mensaje de estado al completarse o si hay error. |
| Delete                   | Botón                                                                                                                                                                                                                          | Elimina el perfil seleccionado después de la confirmación. Deshabilitado cuando no hay nada seleccionado.                                                                                         |
| Auto-save profile changes | Cuando está habilitado, los cambios de TX se escriben automáticamente en el perfil activo. El estado se lee en vivo del estado auto_save del modelo de la radio, no de AppSettings locales. Envía 'profile autosave on/off' a la radio al alternar. | Nuevo en v26.7.4: lee/escribe directamente el modelo de la radio. Ya no se conserva mediante la clave AppSettings AutoSaveTransmitProfile.                                                       |
| Close                    | Botón                                                                                                                                                                                                                          | Cierra el cuadro de diálogo.                                                                                                                                                                      |

## Consejos

- Al hacer doble clic en un perfil de la lista, se carga inmediatamente sin necesidad de hacer clic en **Load**.
- El campo **Profile name** se rellena al seleccionar un perfil, por lo que puede cargar o sobrescribir un perfil sin volver a escribir su nombre.
- En las pestañas **Transmit** y **Microphone**, el botón **Save** está etiquetado como **Create** porque la radio no puede sobrescribir directamente los perfiles de transmisión o micrófono existentes; los cambios se capturan mediante Auto-Save mientras el perfil está activo.
- Si ve un cuadro de diálogo al hacer clic en **Create** en una pestaña de transmisión o micrófono que indica que ya existe un perfil, puede hacer clic en **Enable Auto-Save** para activar el guardado automático sin cambiar a la pestaña **Auto-Save**.
- La casilla de verificación Auto-Save se actualiza automáticamente cuando el guardado automático se habilita o deshabilita por cualquier medio: una carga de perfil, un comando TCI, un cliente remoto o el cuadro de diálogo de confirmación en las pestañas Transmit/Microphone.
- La línea de estado después de guardar muestra un mensaje de éxito (por ejemplo, "Profile saved.") o un mensaje de error (por ejemplo, "Save timed out."). Escribir en el campo de nombre borra este estado para que siempre vea comentarios nuevos.
- Al cargar un perfil de transmisión, la radio utiliza internamente el comando `profile tx load`. Este cambio es transparente y no afecta la experiencia del usuario.
- Los botones deshabilitados se atenúan visualmente para que pueda ver de un vistazo qué acciones están disponibles.

## Relacionado

- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Create a separate mic profile per microphone](create-a-separate-mic-profile-per-microphone.md)
- [Rename or delete a microphone profile](rename-or-delete-a-microphone-profile.md)
- [Review the list of active global profiles](review-the-list-of-active-global-profiles.md)
