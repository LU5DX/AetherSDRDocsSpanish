# Active el autoguardado para que los ajustes de TX siempre persistan

Cuando el autoguardado está activado, cualquier cambio que realice en la configuración de TX y del micrófono se escribe automáticamente en el perfil activo, de modo que nunca pierda un ajuste por olvidar guardarlo manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El administrador de perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión o de micrófono en la radio para que el autoguardado tenga un perfil donde escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo del administrador de perfiles.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque **Auto-save profile changes**.
4. Haga clic en **Close**.

La configuración surte efecto de inmediato. AetherSDR envía el cambio a la radio; no es necesario reiniciar.

Para desactivar el autoguardado, repita los pasos y desmarque **Auto-save profile changes**.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Global** | Pestaña | Administra los perfiles globales. | — |
| **Transmit** | Pestaña | Administra los perfiles de transmisión. Nota: la radio no puede sobrescribir directamente perfiles de transmisión existentes; el botón Guardar/Crear está etiquetado como "Create" y solo crea un perfil nuevo. Las actualizaciones a perfiles existentes son capturadas por el autoguardado mientras el perfil está activo. | — |
| **Microphone** | Pestaña | Administra los perfiles de micrófono. Nota: la radio no puede sobrescribir directamente perfiles de micrófono existentes; el botón Guardar/Crear está etiquetado como "Create" y solo crea un perfil nuevo. Las actualizaciones a perfiles existentes son capturadas por el autoguardado mientras el perfil está activo. | — |
| **Auto-Save** | Pestaña | Controla el guardado automático de perfiles. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un perfil nuevo. | — |
| **Profile list** | Lista | Todos los perfiles de esta categoría; el activo está resaltado. | — |
| **Load** | Botón pulsador | Carga el perfil seleccionado en la radio. | — |
| **Save** (pestaña Global) | Botón pulsador | Guarda el estado actual de la radio con el nombre escrito (crea o sobrescribe). | — |
| **Create** (pestañas Transmit y Microphone) | Botón pulsador | Crea un perfil nuevo con el nombre escrito. No sobrescribe un perfil existente. | — |
| **Delete** | Botón pulsador | Elimina el perfil seleccionado (con confirmación). | — |
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en la configuración de TX y micrófono se guardan automáticamente en el perfil activo de la radio. Cuando no está marcada, los cambios se descartan a menos que guarde manualmente. | `AutoSaveTransmitProfile` |
| **Close** | Botón pulsador | Cierra el cuadro de diálogo. | — |

## Consejos

- El autoguardado aplica tanto a los ajustes de TX como a los de micrófono, no solo a una categoría. Si quiere experimentar sin sobrescribir su perfil actual, desmarque primero **Auto-save profile changes**, realice sus cambios y evalúelos antes de hacer un guardado manual.
- La casilla de verificación refleja el estado actual reportado por la radio al abrir el cuadro de diálogo. Si otro cliente cambió la configuración en la radio, la casilla se actualiza para coincidir. También se mantiene sincronizada con los cambios de autoguardado que se originan fuera de AetherSDR, como al cargar un perfil, clientes TCI o clientes remotos de SmartSDR.
- En las pestañas Transmit y Microphone, si ingresa un nombre que ya existe y hace clic en **Create**, un cuadro de diálogo explica la limitación y ofrece activar el autoguardado para que sus cambios en el perfil existente sean capturados. Si hace clic en **Enable Auto-Save**, la casilla en la pestaña Auto-Save se actualiza automáticamente.

## Relacionado

- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
- [Profile Manager overview](overview.md)
