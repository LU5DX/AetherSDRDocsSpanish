# Revisar la lista de perfiles globales activos

El Administrador de perfiles muestra todos los perfiles globales almacenados en el radio y resalta el que está en uso actualmente. Utilícelo cuando desee confirmar qué perfiles existen o identificar el perfil activo antes de cargarlo o eliminarlo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Administrador de perfiles requiere una conexión activa con el radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Global** si aún no está seleccionada.
3. Revise la **Lista de perfiles**. El perfil activo está resaltado.

## Función de cada control

| Control                       | Tipo       | Comportamiento                                                                                                                                                                                                                                                                          |
|-------------------------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Global (pestaña)**           | Pestaña    | Muestra la lista de perfiles globales del radio conectado.                                                                                                                                                                                                                              |
| **Transmit (pestaña)**         | Pestaña    | Muestra la lista de perfiles de transmisión del radio conectado.                                                                                                                                                                                                                        |
| **Microphone (pestaña)**       | Pestaña    | Muestra la lista de perfiles de micrófono del radio conectado.                                                                                                                                                                                                                          |
| **Auto-Save (pestaña)**        | Pestaña    | Controla el guardado automático de perfiles para los perfiles de transmisión y micrófono.                                                                                                                                                                                               |
| **Lista de perfiles**          | Lista      | Muestra todos los perfiles de la pestaña seleccionada. El perfil activo actualmente está resaltado.                                                                                                                                                                                     |
| **Nombre del perfil**          | Campo de texto | Nombre utilizado al guardar o crear un nuevo perfil. Cuando está vacío, el botón Guardar/Crear está desactivado para evitar guardados accidentales sin un destino.                                                                                                                      |
| **Load**                       | Botón      | Carga el perfil seleccionado en el radio. Solo está habilitado cuando hay un perfil seleccionado.                                                                                                                                                                                       |
| **Save** / **Create**          | Botón      | En la pestaña **Global**, guarda el estado actual del radio con el nombre ingresado en **Nombre del perfil**. En la pestaña **Transmit** o **Microphone**, crea un perfil nuevo; no sobrescribe uno existente. Está desactivado cuando **Nombre del perfil** está vacío.                  |
| **Delete**                     | Botón      | Elimina el perfil seleccionado después de un mensaje de confirmación. Solo está habilitado cuando hay un perfil seleccionado.                                                                                                                                                           |
| **Auto-save profile changes**  | Casilla de verificación | Cuando está activada, los cambios de transmisión y micrófono se guardan automáticamente en el perfil activo. Lee y escribe directamente en el modelo del radio. El estado refleja el estado en vivo del radio, no configuraciones locales. Al alternar, envía `profile autosave on/off` al radio. |
| **Close**                      | Botón      | Cierra el cuadro de diálogo.                                                                                                                                                                                                                                                            |
| **Mensaje de estado**          | Etiqueta   | Muestra un mensaje de resultado después de cada operación Guardar o Crear. Muestra el nombre del perfil y el estado del guardado en azul si es exitoso, o un mensaje de error en rojo si falla. Está oculto hasta que haya un resultado disponible. Se borra automáticamente al empezar a escribir un nuevo nombre de perfil. |

## Comportamiento del mensaje de estado

- Al hacer clic en **Save** o **Create**, aparece una línea de estado debajo de los botones.
- En caso de éxito: muestra el nombre del perfil con un mensaje de confirmación en texto azul.
- En caso de fallo: muestra una descripción del error en texto rojo.
- El mensaje de estado se borra automáticamente cuando comienza a escribir en el campo **Nombre del perfil**.
- La línea de estado está oculta cuando no hay ningún mensaje que mostrar, por lo que no agrega altura adicional al cuadro de diálogo.

## Consejos

- La **Lista de perfiles** se actualiza automáticamente si el radio envía una nueva lista de perfiles mientras el cuadro de diálogo está abierto. No es necesario cerrar y volver a abrir el cuadro de diálogo para ver los cambios.
- El perfil activo aparece resaltado en la lista. Si ningún elemento aparece resaltado, significa que no hay ningún perfil de ese tipo cargado actualmente en el radio.
- En las pestañas **Transmit** y **Microphone**, el botón **Save** se etiqueta como **Create** porque el radio no puede sobrescribir directamente los perfiles de transmisión o micrófono existentes. Las actualizaciones a perfiles existentes se capturan mediante el guardado automático mientras el perfil está activo. Active la casilla **Auto-save profile changes** en la pestaña **Auto-Save** para que los cambios sigan al perfil activo.
- Si intenta crear un perfil de transmisión o micrófono con un nombre que ya existe y el guardado automático está desactivado, AetherSDR le pedirá que active el guardado automático para que sus cambios en ese perfil se capturen.
- La casilla **Auto-save profile changes** se mantiene sincronizada con el estado de guardado automático del radio, incluso si ese estado cambia fuera del cuadro de diálogo. Por ejemplo, si activa el guardado automático a través del mensaje "Enable Auto-Save" o si un cliente SmartSDR remoto o un cliente TCI lo cambia, la casilla se actualiza para coincidir.
- Los botones **Save** y **Create** están desactivados cuando el campo **Nombre del perfil** está vacío, lo que evita guardados accidentales sin un nombre de perfil de destino.
- El menú `Profiles` también muestra una lista dinámica y seleccionable de perfiles globales debajo del separador. Puede ver el perfil activo de un vistazo sin abrir el Administrador de perfiles.

## Relacionados

- [Descripción general del Administrador de perfiles](overview.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
