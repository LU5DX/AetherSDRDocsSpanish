# Administrador de Perfiles

El cuadro de diálogo Administrador de Perfiles permite crear, renombrar, cargar y eliminar perfiles Global, de Transmisión y de Micrófono en la radio, así como controlar el guardado automático de los cambios de transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de Perfiles requiere una conexión activa con la radio.
- Sepa qué perfil desea renombrar o eliminar. El perfil activo aparece resaltado en la lista.

## Abrir el Administrador de Perfiles

Haga clic en `Profiles > Profile Manager...`.

## Trabajar con perfiles

### Para renombrar un perfil de micrófono

No existe un comando de renombrar en el lugar. Renombrar es un proceso de dos pasos: cree un perfil nuevo con el nombre deseado y luego elimine el antiguo.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea renombrar en la **Lista de perfiles**. Su nombre aparece en el campo **Nombre de perfil**.
4. Borre el campo **Nombre de perfil** y escriba el nuevo nombre.
5. Haga clic en **Save**. La radio crea un nuevo perfil de micrófono con el nuevo nombre y la lista se actualiza.
6. Haga clic en el nombre del perfil original en la **Lista de perfiles**.
7. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación que pregunta "Delete profile "*nombre*"?".
8. Haga clic en **Yes**. El perfil se elimina de la lista.
9. Haga clic en **Close**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Haga clic en el perfil que desea eliminar en la **Lista de perfiles**.
4. Haga clic en **Delete**. Aparece un cuadro de diálogo de confirmación que pregunta "Delete profile "*nombre*"?".
5. Haga clic en **Yes**. El perfil se elimina de la lista.
6. Haga clic en **Close**.

### Para cargar o eliminar un perfil de transmisión

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Transmit**.
3. Haga clic en el perfil que desea cargar o eliminar en la **Lista de perfiles**.
4. Haga clic en **Load** para aplicar el perfil de transmisión seleccionado a la radio.
5. Haga clic en **Delete** para eliminar el perfil de transmisión seleccionado después de la confirmación.

### Para guardar un perfil global

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Global**.
3. Escriba un nombre en el campo **Nombre de perfil**.
4. Haga clic en **Save**. El cuadro de diálogo muestra un mensaje de estado que indica el resultado. Si la radio no responde en 15 segundos, el mensaje de estado se borra.

### Para habilitar o deshabilitar el guardado automático de cambios de transmisión

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Auto-Save**.
3. Marque o desmarque **Auto-save profile changes**. El estado de la radio se actualiza inmediatamente. La casilla de verificación lee el estado de guardado automático en vivo de la radio, no una configuración local.

## Qué hace cada control

| Control                               | Tipo       | Comportamiento                                                                                                                                                                                                                                                                                                                                                           |
|---------------------------------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pestaña **Global**                    | Pestaña    | Cambia el cuadro de diálogo para administrar perfiles globales.                                                                                                                                                                                                                                                                                                          |
| Pestaña **Transmit**                  | Pestaña    | Cambia el cuadro de diálogo para administrar perfiles de transmisión.                                                                                                                                                                                                                                                                                                    |
| Pestaña **Microphone**                | Pestaña    | Cambia el cuadro de diálogo para administrar perfiles de micrófono.                                                                                                                                                                                                                                                                                                      |
| Pestaña **Auto-Save**                 | Pestaña    | Cambia el cuadro de diálogo para controlar el guardado automático de perfiles.                                                                                                                                                                                                                                                                                           |
| **Nombre de perfil**                  | Campo de texto | Contiene el nombre que se usa al guardar un perfil nuevo. Se completa automáticamente cuando selecciona un perfil de la lista. El botón **Save** está deshabilitado cuando el campo está vacío. Volver a escribir el nombre borra cualquier mensaje de estado de la operación de guardado anterior.                                                                          |
| **Lista de perfiles**                 | Lista      | Muestra todos los perfiles de la categoría seleccionada en la radio. El perfil activo está resaltado. Al hacer doble clic en un perfil, se carga inmediatamente.                                                                                                                                                                                                           |
| **Load**                              | Botón      | Carga el perfil seleccionado en la radio. Habilitado solo cuando hay un perfil seleccionado. El estilo deshabilitado (atenuado) distingue el estado "sin selección" de un botón habilitado.                                                                                                                                                                             |
| **Save** (pestaña Global)             | Botón      | Guarda el estado actual de la radio con el nombre del campo **Nombre de perfil**. Deshabilitado cuando el campo **Nombre de perfil** está vacío. Después de hacer clic, aparece una línea de estado debajo de los botones que muestra información de éxito o error. La línea de estado se oculta cuando comienza a escribir un nombre nuevo.                              |
| **Save** (pestaña Transmit/Mic)       | Botón      | Etiquetado como **Create** en las pestañas Transmit y Microphone. Crea un perfil nuevo con el nombre del campo **Nombre de perfil**. Deshabilitado cuando el campo **Nombre de perfil** está vacío. Después de hacer clic, aparece una línea de estado debajo de los botones que muestra información de éxito o error. La línea de estado se oculta cuando comienza a escribir un nombre nuevo. |
| **Delete**                            | Botón      | Elimina el perfil seleccionado después de la confirmación. Habilitado solo cuando hay un perfil seleccionado. El estilo deshabilitado (atenuado) distingue el estado "sin selección" de un botón habilitado.                                                                                                                                                             |
| **Auto-save profile changes**         | Casilla de verificación | Cuando está habilitada, los cambios de transmisión se guardan automáticamente en el perfil de transmisión activo. La casilla lee y escribe el estado de guardado automático en vivo de la radio directamente. La configuración no se conserva mediante `AutoSaveTransmitProfile` en AppSettings. Al alternar, envía `profile autosave on` o `profile autosave off` a la radio. Nuevo en v26.7.4. |
| **Close**                             | Botón      | Cierra el cuadro de diálogo Administrador de Perfiles.                                                                                                                                                                                                                                                                                                                   |

## Mensajes de estado

Después de guardar o crear un perfil, aparece una línea de estado debajo de los botones Save/Create y Delete. La línea de estado indica si la operación fue exitosa o falló:

- Los mensajes de éxito aparecen en un color azul claro.
- Los mensajes de error aparecen en un color rojo claro.

La línea de estado desaparece cuando comienza a escribir en el campo **Nombre de perfil**, o cuando han transcurrido 15 segundos sin una respuesta de la radio después de hacer clic en Save en un perfil global.

## Consejos

- Al seleccionar un perfil en la **Lista de perfiles**, el campo **Nombre de perfil** se completa automáticamente. Para renombrar, simplemente sobrescriba ese texto antes de hacer clic en **Save**.
- Los botones Load, Delete, Save y Create están deshabilitados hasta que exista un destino válido. Si un botón está atenuado, verifique que haya un perfil seleccionado (para Load/Delete) o que el campo **Nombre de perfil** no esté vacío (para Save/Create).
- Haga doble clic en un perfil de la lista para cargarlo inmediatamente, omitiendo el botón **Load**.
- La lista se actualiza automáticamente cuando la radio informa un cambio. No es necesario volver a abrir el cuadro de diálogo después de crear o eliminar.
- Los perfiles de micrófono no se pueden sobrescribir directamente. Para actualizar un perfil de micrófono existente, active **Auto-save profile changes** en la pestaña **Auto-Save** y luego realice sus cambios mientras el perfil está activo.
- La casilla **Auto-save profile changes** se mantiene sincronizada con la radio: si otro cliente o el proceso de carga de perfiles alterna el guardado automático, la casilla se actualiza automáticamente.
- El botón **Load** para perfiles de transmisión usa internamente el comando `profile tx load`. Este cambio es transparente y no afecta la forma de interactuar con el cuadro de diálogo.

## Solución de problemas

- **Delete está atenuado** — No hay ningún perfil seleccionado en la **Lista de perfiles**. Haga clic en un nombre de perfil para seleccionarlo y luego haga clic en **Delete**.
- **Save está atenuado** — El campo **Nombre de perfil** está vacío. Escriba un nombre de perfil para habilitar el botón.
- **Save aparece, pero el nuevo perfil no se muestra en la lista** — La radio envía las actualizaciones de la lista de forma asíncrona. Espere un momento para que la lista se actualice. Si no se actualiza, cierre y vuelva a abrir el Administrador de Perfiles.
- **Aparece un cuadro de diálogo "Profile already exists"** — Intentó crear un perfil de micrófono con un nombre que ya existe. La radio no puede sobrescribir perfiles de micrófono. Haga clic en **Enable Auto-Save** en el cuadro de diálogo para activar el guardado automático de perfiles, luego cargue el perfil existente y realice sus cambios para actualizarlo.
- **El nombre del perfil antiguo aún está presente después de eliminar** — Es posible que haya hecho clic en **No** en la solicitud de confirmación. Repita los pasos 3 a 5 y haga clic en **Yes** para confirmar.
- **La carga del perfil de transmisión falla** — Asegúrese de que la radio esté conectada y que el nombre del perfil de transmisión sea válido. El cuadro de diálogo usa el comando `profile tx load` para cargar perfiles de transmisión.
- **El mensaje de estado permanece en pantalla demasiado tiempo** — Si la radio no responde en 15 segundos a un guardado de perfil global, el mensaje de estado se borra automáticamente.

## Relacionado

- [Descripción general del Administrador de Perfiles](overview.md)
- [Crear un perfil de micrófono separado por micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
