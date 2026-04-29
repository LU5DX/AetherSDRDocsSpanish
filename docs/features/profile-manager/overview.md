# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar, renombrar y eliminar los tres tipos de perfiles almacenados en el FLEX-8600: Global, Transmit y Microphone. Úselo para guardar y restaurar estados completos de la radio, cambiar entre configuraciones de operación y controlar si los cambios de transmisión se guardan automáticamente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El cuadro de diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — además de un botón **Close** en la parte inferior.

**Pestañas Global, Transmit y Microphone**

Cada una de estas tres pestañas tiene el mismo diseño:

- Un campo de texto **Profile name** en la parte superior. Escriba un nombre aquí antes de guardar un perfil nuevo, o seleccione un perfil existente de la lista para completar este campo automáticamente.
- Botones **Load**, **Save** y **Delete**. Load y Delete permanecen deshabilitados hasta que seleccione un perfil en la lista. Al seleccionar un perfil, su nombre se copia automáticamente en el campo **Profile name**.
- Una **Profile list** que muestra todos los perfiles guardados para esa categoría. El perfil activo aparece resaltado. Hacer doble clic en un perfil de la lista lo carga de inmediato, lo que equivale a seleccionarlo y hacer clic en **Load**.

Al hacer clic en **Save**, la radio guarda el estado actual con el nombre indicado en el campo **Profile name**. Si el campo está vacío, se utiliza el nombre del perfil seleccionado en ese momento.

Al hacer clic en **Delete**, aparece un cuadro de confirmación antes de que el perfil sea eliminado.

La lista de perfiles se actualiza automáticamente cuando la radio reporta un cambio, de modo que las adiciones o eliminaciones realizadas en otro lugar se reflejan sin necesidad de volver a abrir el cuadro de diálogo.

**Pestaña Auto-Save**

La pestaña Auto-Save contiene una única casilla de verificación y una breve descripción. Cuando **Auto-save profile changes** está activada, los cambios en los ajustes de TX y micrófono se escriben automáticamente en el perfil activo. Este estado se persiste como `AutoSaveTransmitProfile`. Cuando está desactivada, debe usar **Save** de forma explícita para conservar cualquier cambio.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Global (tab) | Pestaña | Gestiona los perfiles globales. | — |
| Transmit (tab) | Pestaña | Gestiona los perfiles de transmisión. | — |
| Microphone (tab) | Pestaña | Gestiona los perfiles de micrófono. | — |
| Auto-Save (tab) | Pestaña | Controla el guardado automático de perfiles. | — |
| Profile name | Campo de texto | Nombre utilizado al guardar un perfil nuevo. Se completa automáticamente al seleccionar un perfil. | — |
| Profile list | Lista | Todos los perfiles de esta categoría; el activo aparece resaltado. | — |
| Load | Botón | Carga el perfil seleccionado en la radio. Deshabilitado cuando no hay nada seleccionado. | — |
| Save | Botón | Guarda el estado actual de la radio con el nombre escrito, o con el nombre seleccionado si el campo está vacío. | — |
| Delete | Botón | Elimina el perfil seleccionado tras confirmación. Deshabilitado cuando no hay nada seleccionado. | — |
| Auto-save profile changes | Casilla de verificación | Cuando está habilitada, los cambios de TX y micrófono se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |
| Close | Botón | Cierra el cuadro de diálogo. | — |

## Consejos

- Hacer doble clic en un perfil de la lista lo carga de inmediato sin necesidad de hacer clic en **Load**.
- El campo **Profile name** se completa al seleccionar un perfil, por lo que puede cargar o sobrescribir un perfil sin tener que volver a escribir su nombre.

## Temas relacionados

- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Crear un perfil de micrófono independiente por cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
