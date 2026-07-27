# Cambiar a un perfil de transmisión guardado

Cargue un perfil de transmisión previamente guardado en la radio. Esto aplica un conjunto de parámetros de TX almacenados en un solo paso, reemplazando la configuración de transmisión actual.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Debe existir al menos un perfil de transmisión en la radio. Si la lista de perfiles está vacía, cree un perfil primero.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Transmit** para cambiar a la lista de perfiles de transmisión.
3. En la **lista de perfiles**, haga clic en el perfil que desea cargar. El perfil activo se resalta.
4. Haga clic en **Load**.

Alternativamente, haga doble clic en cualquier entrada de la **lista de perfiles** para cargarla sin hacer clic en **Load**.

## Función de cada control

| Control                                  | Tipo       | Comportamiento                                                                                                                   |
|------------------------------------------|------------|----------------------------------------------------------------------------------------------------------------------------------|
| Pestaña **Global**                       | Pestaña    | Cambia el cuadro de diálogo a la vista de perfiles globales.                                                                     |
| Pestaña **Transmit**                     | Pestaña    | Cambia el cuadro de diálogo a la vista de perfiles de transmisión.                                                               |
| Pestaña **Microphone**                   | Pestaña    | Cambia el cuadro de diálogo a la vista de perfiles de micrófono.                                                                 |
| Pestaña **Auto-Save**                    | Pestaña    | Cambia el cuadro de diálogo a la vista de configuración de guardado automático.                                                  |
| **Profile name**                         | Campo texto| Nombre utilizado al guardar un nuevo perfil. El botón **Save** se deshabilita cuando este campo está vacío.                      |
| **Profile list**                         | Lista      | Muestra todos los perfiles de la categoría seleccionada almacenados en la radio. El perfil activo actual se resalta.              |
| **Load**                                 | Botón      | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. Se deshabilita cuando no hay ningún perfil seleccionado. |
| **Save**                                 | Botón      | Guarda el estado actual de la radio con el nombre escrito. Se deshabilita cuando el campo **Profile name** está vacío.           |
| **Delete**                               | Botón      | Elimina el perfil seleccionado tras la confirmación. Solo se habilita cuando hay un perfil seleccionado. Se deshabilita cuando no hay ningún perfil seleccionado. |
| **Auto-save profile changes**            | Casilla    | Cuando está activada, los cambios de TX se escriben automáticamente en el perfil activo. El estado se lee en vivo del modelo de radio, no de la configuración local de AppSettings. Envía `profile autosave on/off` a la radio al alternar. |
| **Close**                                | Botón      | Cierra el cuadro de diálogo.                                                                                                     |

## Notas

- El botón para guardar perfiles se etiqueta **Save** en la pestaña Global y **Create** en las pestañas Transmit y Microphone. Para actualizar un perfil existente, active **Auto-save profile changes** en la pestaña **Auto-Save**: los cambios en el perfil activo se capturarán automáticamente.
- La casilla **Auto-save profile changes** se sincroniza directamente con la radio. Los cambios realizados fuera del cuadro de diálogo (por clientes TCI, carga de perfiles o clientes SmartSDR remotos) actualizarán el estado de la casilla. Esta configuración ya no se conserva mediante la clave `AutoSaveTransmitProfile` de AppSettings.
- Si intenta guardar un perfil con un nombre que ya existe y el guardado automático está desactivado, aparecerá un cuadro de diálogo que ofrece activar el guardado automático para que los cambios futuros en el perfil se capturen.
- Un mensaje de resultado aparece debajo de los botones **Load**, **Save/Create** y **Delete** después de cada operación de guardado, mostrando si la operación fue exitosa o fallida. Este mensaje desaparece automáticamente cuando comienza a escribir un nuevo nombre de perfil.
- El botón **Save/Create** se deshabilita cuando el campo **Profile name** está vacío, evitando clics accidentales sin un nombre de destino.

## Consejos

- Seleccionar un perfil en la lista completa el campo **Profile name** con el nombre de ese perfil. Si escribe un nombre diferente y hace clic en **Save** (Global) o **Create** (Transmit/Microphone), se crea un nuevo perfil con ese nombre.
- Para conservar los cambios de TX en el perfil de transmisión activo sin guardarlos manualmente, active **Auto-save profile changes** en la pestaña **Auto-Save**.
- Al hacer doble clic en un perfil de la lista, se carga inmediatamente y se borra cualquier mensaje de resultado de guardado anterior.

## Solución de problemas

- **Load o Delete están atenuados** — No hay ningún perfil seleccionado en la **lista de perfiles**. Haga clic en un nombre de perfil para seleccionarlo y luego haga clic en el botón.
- **Save está atenuado** — El campo **Profile name** está vacío. Escriba un nombre o seleccione un perfil de la lista para autocompletar el nombre.
- **La lista de perfiles está vacía** — Aún no existen perfiles para la categoría seleccionada en la radio. Use **Save** (Global) o **Create** (Transmit/Microphone) para crear uno primero.
- **Hacer clic en Save/Create no funciona para un nombre existente** — La radio no puede sobrescribir perfiles directamente. Active el guardado automático para que sus cambios se capturen automáticamente, o realice cambios manualmente mientras el perfil está activo y el guardado automático está encendido.
- **El resultado del guardado muestra un error** — Es posible que la radio se haya desconectado durante la operación de guardado. Espere a que se restablezca la conexión e intente nuevamente.

## Relacionados

- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Descripción general del Administrador de perfiles](overview.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Guardar el estado actual de la radio como un nuevo perfil de transmisión](save-the-current-radio-state-as-a-new-transmit-profile.md)
