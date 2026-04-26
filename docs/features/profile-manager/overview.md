# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar, renombrar y eliminar perfiles Global, Transmit y Microphone almacenados en el radio. Úselo para guardar y recuperar estados completos del radio sin reconfigurar los ajustes manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Administrador de perfiles no está disponible cuando está desconectado.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El cuadro de diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — cada una cubre una categoría de perfil independiente.

**Las pestañas Global, Transmit y Microphone** comparten el mismo diseño:

- Escriba un nombre en **Profile name** para identificar un nuevo perfil antes de guardarlo, o seleccione una entrada existente en **Profile list** para completar el campo automáticamente.
- La **Profile list** muestra todos los perfiles de esa categoría. El perfil activo actualmente aparece resaltado.
- Haga clic en **Load** (o haga doble clic en una entrada de la lista) para aplicar el perfil seleccionado al radio de inmediato.
- Haga clic en **Save** para guardar el estado actual del radio con el nombre que aparece en **Profile name**. Si el nombre coincide con un perfil existente, ese perfil se sobrescribe.
- Haga clic en **Delete** para eliminar el perfil seleccionado. Aparece un mensaje de confirmación antes de que el perfil sea eliminado.

**La pestaña Auto-Save** controla si los cambios de transmisión y micrófono se acumulan automáticamente:

- Cuando **Auto-save profile changes** está marcado, cualquier cambio en los ajustes de TX o micrófono se escribe en el perfil activo sin necesidad de hacer clic en Save manualmente. Este ajuste se almacena como `AutoSaveTransmitProfile`.

Haga clic en **Close** para cerrar el cuadro de diálogo. Los cambios ya enviados al radio permanecen vigentes.

## Qué hace cada control

| Control | Ubicación | Comportamiento | Clave de ajuste |
|---|---|---|---|
| Global (pestaña) | Barra de pestañas | Cambia a la gestión de perfiles globales. | — |
| Transmit (pestaña) | Barra de pestañas | Cambia a la gestión de perfiles de transmisión. | — |
| Microphone (pestaña) | Barra de pestañas | Cambia a la gestión de perfiles de micrófono. | — |
| Auto-Save (pestaña) | Barra de pestañas | Cambia a la configuración de guardado automático. | — |
| Profile name | Pestañas Global / Transmit / Microphone | Nombre usado al crear o sobrescribir un perfil. Se completa automáticamente al seleccionar una entrada de la lista. | — |
| Profile list | Pestañas Global / Transmit / Microphone | Todos los perfiles de la categoría activa. El perfil activo aparece resaltado. | — |
| Load | Pestañas Global / Transmit / Microphone | Aplica el perfil seleccionado al radio. También se activa al hacer doble clic en una entrada de la lista. | — |
| Save | Pestañas Global / Transmit / Microphone | Guarda el estado actual del radio con el nombre indicado en Profile name. | — |
| Delete | Pestañas Global / Transmit / Microphone | Elimina el perfil seleccionado tras confirmación. | — |
| Auto-save profile changes | Pestaña Auto-Save | Cuando está habilitado, los cambios de TX y micrófono se escriben en el perfil activo automáticamente. | `AutoSaveTransmitProfile` |
| Close | Parte inferior del cuadro de diálogo | Cierra el cuadro de diálogo. | — |

## Consejos

- Load y Delete están deshabilitados hasta que seleccione un perfil de la lista. Seleccione una entrada primero.
- La **Profile list** se actualiza automáticamente si el radio reporta un cambio mientras el cuadro de diálogo está abierto — no es necesario cerrarlo y volver a abrirlo.
- La lista dinámica bajo `Profiles >` en la barra de menú muestra los perfiles globales activos y permite cargarlos sin abrir el Administrador de perfiles.

## Relacionado

- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Crear un perfil de micrófono separado por cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
