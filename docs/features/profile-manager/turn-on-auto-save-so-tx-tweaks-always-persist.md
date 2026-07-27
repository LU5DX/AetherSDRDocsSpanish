# Active el autoguardado para que los ajustes de TX sean siempre persistentes

Cuando el autoguardado está habilitado, cualquier cambio que realice en los ajustes de transmisión y micrófono se escribe automáticamente en el perfil activo, para que nunca pierda un ajuste por olvidar guardarlo manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Gestor de Perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión o micrófono en la radio para que el autoguardado tenga un perfil donde escribir.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Gestor de Perfiles.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque **Auto-save profile changes**.
4. Haga clic en **Close**.

El ajuste surte efecto de inmediato. AetherSDR envía el cambio a la radio; no es necesario reiniciar.

Para desactivar el autoguardado, repita los pasos y desmarque **Auto-save profile changes**.

## Qué hace cada control

| Control                                   | Tipo        | Comportamiento                                                                                                                                                                                                                                                                               |
|-------------------------------------------|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Global**                                | Pestaña     | Gestiona los perfiles globales.                                                                                                                                                                                                                                                              |
| **Transmit**                              | Pestaña     | Gestiona los perfiles de transmisión. Nota: la radio no puede sobrescribir directamente perfiles de transmisión existentes; el botón Guardar/Crear se etiqueta "Create" y solo crea un perfil nuevo. Las actualizaciones a perfiles existentes se capturan mediante Autoguardado mientras el perfil está activo. |
| **Microphone**                            | Pestaña     | Gestiona los perfiles de micrófono. Nota: la radio no puede sobrescribir directamente perfiles de micrófono existentes; el botón Guardar/Crear se etiqueta "Create" y solo crea un perfil nuevo. Las actualizaciones a perfiles existentes se capturan mediante Autoguardado mientras el perfil está activo.   |
| **Auto-Save**                             | Pestaña     | Controla el guardado automático de perfiles.                                                                                                                                                                                                                                                 |
| **Profile name**                          | Campo de texto | Nombre que se usa al guardar un perfil nuevo. Un campo vacío deshabilita el botón Guardar/Crear. Escribir o editar el campo borra cualquier mensaje de estado que se muestre en esa pestaña.                                                                                                 |
| **Profile list**                          | Lista       | Todos los perfiles de esta categoría; el activo se resalta. Haga doble clic para cargar el perfil.                                                                                                                                                                                           |
| **Load**                                  | Botón       | Carga el perfil seleccionado en la radio. Deshabilitado cuando no hay ningún perfil seleccionado.                                                                                                                                                                                            |
| **Save** (pestaña Global)                 | Botón       | Guarda el estado actual de la radio con el nombre escrito (crea o sobrescribe). Deshabilitado cuando el campo de nombre de perfil está vacío. Después de hacer clic, muestra un mensaje de estado ("Saving...", "Saved" o un error) debajo de los botones. El tiempo de espera para una respuesta de guardado es de 15 segundos. |
| **Create** (pestañas Transmit y Microphone) | Botón       | Crea un perfil nuevo con el nombre escrito. No sobrescribe un perfil existente. Deshabilitado cuando el campo de nombre de perfil está vacío. Después de hacer clic, muestra un mensaje de estado ("Saving...", "Saved" o un error) debajo de los botones. El tiempo de espera para una respuesta de guardado es de 15 segundos. |
| **Delete**                                | Botón       | Elimina el perfil seleccionado (con confirmación). Deshabilitado cuando no hay ningún perfil seleccionado.                                                                                                                                                                                   |
| **Auto-save profile changes**             | Casilla de verificación | Cuando está habilitada, los cambios de TX se escriben automáticamente en el perfil activo. El estado se lee en vivo del modelo de radio, no de ajustes locales. Cuando está deshabilitada, los cambios se descartan a menos que guarde manualmente. Al alternar, envía `profile autosave on/off` a la radio. |
| **Close**                                 | Botón       | Cierra el diálogo.                                                                                                                                                                                                                                                                           |

## Consejos

- El botón Guardar/Crear está deshabilitado cuando el campo de nombre de perfil está vacío, lo que evita clics accidentales en un botón que no haría nada.
- Después de hacer clic en Guardar o Crear, aparece un mensaje de estado debajo de los botones que muestra "Saving...", "Saved" (en azul) o un error (en rojo). El estado se borra automáticamente cuando escribe o edita el campo de nombre de perfil.
- El autoguardado se aplica tanto a los ajustes de TX como de micrófono, no solo a una categoría. Si desea experimentar sin sobrescribir su perfil actual, desmarque primero **Auto-save profile changes**, realice sus cambios y evalúe antes de confirmar un guardado manual.
- La casilla refleja el estado actual que reporta la radio cuando se abre el diálogo. Si otro cliente cambió el ajuste en la radio, la casilla se actualiza para coincidir. La casilla también se mantiene sincronizada con los cambios de Autoguardado que se originan fuera de AetherSDR, como cargar un perfil, clientes TCI o clientes remotos de SmartSDR.
- En las pestañas Transmit y Microphone, si ingresa un nombre que ya existe y hace clic en **Create**, un diálogo explica la limitación y ofrece habilitar el Autoguardado para que sus cambios en el perfil existente sean capturados. Si hace clic en **Enable Auto-Save**, la casilla de la pestaña Auto-Save se actualiza automáticamente.

## Relacionados

- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Descripción general del Gestor de Perfiles](overview.md)
