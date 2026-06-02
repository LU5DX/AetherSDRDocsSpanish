# Active el auto-guardado para que los ajustes de TX siempre persistan

Cuando el auto-guardado está habilitado, cualquier cambio que realice en los ajustes de TX y micrófono se escribe automáticamente en el perfil activo, de modo que nunca pierda un ajuste por olvidar guardarlo manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión o micrófono en la radio para que el auto-guardado tenga un perfil donde escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque **Auto-save profile changes**.
4. Haga clic en **Close**.

El ajuste surte efecto de inmediato. AetherSDR envía el cambio a la radio; no es necesario reiniciar.

Para desactivar el auto-guardado, repita los pasos y desmarque **Auto-save profile changes**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Global** | Pestaña | Gestiona los perfiles globales. | — |
| **Transmit** | Pestaña | Gestiona los perfiles de transmisión. Nota: la radio no puede sobrescribir perfiles de transmisión existentes directamente; el botón Guardar/Crear está etiquetado como "Create" y solo crea un perfil nuevo. Las actualizaciones a perfiles existentes son capturadas por Auto-Save mientras el perfil está activo. | — |
| **Microphone** | Pestaña | Gestiona los perfiles de micrófono. Nota: la radio no puede sobrescribir perfiles de micrófono existentes directamente; el botón Guardar/Crear está etiquetado como "Create" y solo crea un perfil nuevo. Las actualizaciones a perfiles existentes son capturadas por Auto-Save mientras el perfil está activo. | — |
| **Auto-Save** | Pestaña | Controla el guardado automático de perfiles. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un perfil nuevo. | — |
| **Profile list** | Lista | Todos los perfiles de esta categoría; el activo está resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en la radio. | — |
| **Save** (pestaña Global) | Botón | Guarda el estado actual de la radio con el nombre escrito (crea o sobrescribe). | — |
| **Create** (pestañas Transmit y Microphone) | Botón | Crea un perfil nuevo con el nombre escrito. No sobrescribe un perfil existente. | — |
| **Delete** | Botón | Elimina el perfil seleccionado (con confirmación). | — |
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en los ajustes de TX y micrófono se guardan automáticamente en el perfil activo de la radio. Cuando no está marcada, los cambios se descartan a menos que guarde manualmente. | `AutoSaveTransmitProfile` |
| **Close** | Botón | Cierra el diálogo. | — |

## Consejos

- El auto-guardado se aplica tanto a los ajustes de TX como de micrófono, no solo a una categoría. Si desea experimentar sin sobrescribir su perfil actual, desmarque primero **Auto-save profile changes**, realice sus cambios y evalúe antes de confirmar un guardado manual.
- La casilla de verificación refleja el estado actual informado por la radio cuando se abre el diálogo. Si otro cliente cambió el ajuste en la radio, la casilla se actualiza para coincidir. La casilla también se mantiene sincronizada con los cambios de Auto-Save que se originan fuera de AetherSDR, como cargar un perfil, clientes TCI o clientes SmartSDR remotos.
- En las pestañas Transmit y Microphone, si ingresa un nombre que ya existe y hace clic en **Create**, un diálogo explica la limitación y ofrece habilitar Auto-Save para que sus cambios en el perfil existente sean capturados. Si hace clic en **Enable Auto-Save**, la casilla de la pestaña Auto-Save se actualiza automáticamente.

## Relacionado

- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Descripción general del Administrador de perfiles](overview.md)
