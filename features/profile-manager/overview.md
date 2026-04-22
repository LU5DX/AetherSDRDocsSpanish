# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar, renombrar y eliminar perfiles Global, Transmit y Microphone almacenados en el radio. Úselo para guardar y restaurar estados completos del radio sin necesidad de reconfigurar los ajustes manualmente en cada sesión.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Administrador de perfiles requiere una conexión activa con el radio.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — cada una correspondiente a una categoría separada de perfiles almacenados en el FLEX-8600.

**Las pestañas Global, Transmit y Microphone** comparten el mismo diseño: un campo de texto en la parte superior para ingresar el nombre del perfil, tres botones de acción (Load, Save, Delete) y una lista con todos los perfiles de esa categoría debajo. El perfil activo en ese momento aparece resaltado en la lista. Al seleccionar un perfil en la lista, el campo **Profile name** se rellena con el nombre de ese perfil y se habilitan los botones Load y Delete. Hacer doble clic sobre un perfil en la lista lo carga de inmediato, lo que equivale a hacer clic en Load.

**La pestaña Auto-Save** contiene una única casilla de verificación que controla si los cambios en los ajustes de transmisión y micrófono se escriben automáticamente en el perfil activo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Ajuste persistido |
|---|---|---|---|
| Global (pestaña) | Pestaña | Administra los perfiles globales almacenados en el radio. | — |
| Transmit (pestaña) | Pestaña | Administra los perfiles de transmisión almacenados en el radio. | — |
| Microphone (pestaña) | Pestaña | Administra los perfiles de micrófono almacenados en el radio. | — |
| Auto-Save (pestaña) | Pestaña | Controla el guardado automático de los cambios de transmisión y micrófono. | — |
| Profile name | Campo de texto | Nombre utilizado al guardar un nuevo perfil. Se rellena automáticamente al seleccionar un perfil de la lista. | — |
| Lista de perfiles | Lista | Todos los perfiles de la categoría actual. El perfil activo aparece resaltado. | — |
| Load | Botón | Envía el perfil seleccionado al radio, activándolo. Se habilita solo cuando hay un perfil seleccionado en la lista. | — |
| Save | Botón | Guarda el estado actual del radio con el nombre indicado en el campo **Profile name**. Si el campo está vacío, utiliza el nombre del elemento seleccionado en la lista. | — |
| Delete | Botón | Elimina el perfil seleccionado tras una confirmación. Se habilita solo cuando hay un perfil seleccionado en la lista. | — |
| Auto-save profile changes | Casilla de verificación | Cuando está marcada, los cambios en los ajustes de TX y micrófono se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |
| Close | Botón | Cierra el diálogo del Administrador de perfiles. | — |

## Consejos

- Al seleccionar un perfil en la lista, el campo **Profile name** se rellena con su nombre. Para guardar con un nombre diferente, edite el campo antes de hacer clic en Save; esto crea un nuevo perfil en lugar de sobrescribir el seleccionado.
- La lista de perfiles se actualiza automáticamente cuando el radio informa cambios, por lo que los perfiles guardados o eliminados desde otro cliente aparecerán sin necesidad de volver a abrir el diálogo.

## Relacionados

- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Crear un perfil de micrófono separado por micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
