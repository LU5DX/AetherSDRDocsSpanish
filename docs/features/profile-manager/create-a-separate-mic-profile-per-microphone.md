# Crear un perfil de micrófono independiente para cada micrófono

La pestaña Micrófono en el Administrador de perfiles le permite guardar, cargar y eliminar perfiles de micrófono almacenados en la radio. Al guardar un perfil con nombre para cada micrófono físico, puede cambiar la configuración del micrófono al instante sin tener que volver a introducir manualmente los valores de ecualización, nivel y procesamiento.

**Nota:** Para los perfiles de micrófono, la radio solo permite crear perfiles nuevos; no puede sobrescribir directamente un perfil de micrófono existente. Para actualizar un perfil existente con una nueva configuración, active ese perfil y habilite **Auto-Save** (consulte los pasos a continuación y el artículo relacionado *Activar el guardado automático*).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Configure los ajustes de micrófono de la radio para el primer micrófono antes de guardar. El perfil captura el estado actual en el momento en que hace clic en Crear.

## Pasos

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Configure los ajustes de micrófono de la radio (nivel, ecualización, procesamiento) para el primer micrófono si aún no lo ha hecho.
4. Haga clic en el campo **Profile name** y escriba un nombre para este micrófono; por ejemplo, `Desk Mic`.
5. Haga clic en **Create**. El perfil aparece en la **Profile list**.
6. Conecte o seleccione su segundo micrófono y ajuste la configuración de micrófono de la radio para que se adapte a él.
7. Haga clic en el campo **Profile name**, borre cualquier texto existente y escriba un nombre para el segundo micrófono; por ejemplo, `Headset`.
8. Haga clic en **Create**. El segundo perfil ahora aparece en la **Profile list** junto al primero.
9. Para cambiar entre micrófonos en sesiones futuras, seleccione el nombre del perfil en la **Profile list** y haga clic en **Load**, o haga doble clic en el nombre del perfil.
10. Haga clic en **Close** cuando haya terminado.

## Función de cada control

| Control              | Tipo       | Comportamiento                                                                                                                                                                                                                                           |
|----------------------|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Microphone (pestaña)** | Pestaña    | Muestra los perfiles de micrófono almacenados en la radio.                                                                                                                                                                                               |
| **Profile name**     | Campo de texto | Nombre que se utiliza al guardar un nuevo perfil de micrófono. Se rellena automáticamente al seleccionar un elemento de la lista. **Create** está desactivado cuando el campo está vacío. Editar el campo borra cualquier mensaje de resultado mostrado debajo de los botones. |
| **Profile list**     | Lista       | Todos los perfiles de micrófono en la radio; el perfil activo está resaltado.                                                                                                                                                                            |
| **Load**             | Botón       | Carga el perfil seleccionado en la radio. Solo está habilitado cuando hay un perfil seleccionado. Al hacer doble clic en un perfil también se carga.                                                                                                     |
| **Create**           | Botón       | Crea un nuevo perfil de micrófono con el nombre indicado en **Profile name**. Desactivado cuando el campo **Profile name** está vacío. La radio no admite sobrescribir un perfil de micrófono existente; use Auto-Save para capturar los cambios en un perfil activo. |
| **Delete**           | Botón       | Elimina el perfil seleccionado después de la confirmación. Solo está habilitado cuando hay un perfil seleccionado.                                                                                                                                       |
| **Close**            | Botón       | Cierra el cuadro de diálogo del Administrador de perfiles.                                                                                                                                                                                               |

### Nota adicional (visible en la pestaña Microphone)

Debajo de los botones aparece una etiqueta que dice:

> Las actualizaciones de los perfiles existentes se guardan automáticamente: active Auto-Save (pestaña Auto-Save) para que los cambios sigan al perfil activo. Create crea un perfil nuevo; no sobrescribe uno existente.

## Mensajes de resultado

Después de hacer clic en **Create**, aparece una línea de mensaje debajo de los botones que indica el resultado:

- **Éxito** — El perfil se creó en la radio. El mensaje se muestra en texto azul.
- **Error** — La radio rechazó la operación (por ejemplo, un nombre duplicado o un tiempo de espera agotado). El mensaje se muestra en texto rojo.
- **En progreso** — Mientras se espera la respuesta de la radio (máximo 15 segundos), puede aparecer un breve mensaje "creando...".

La línea de resultado se borra automáticamente cuando comienza a escribir en el campo **Profile name** o cuando carga un perfil diferente.

## Consejos

- Seleccionar un perfil en la **Profile list** copia su nombre en el campo **Profile name**.
- La **Profile list** se actualiza automáticamente cuando la radio informa de un cambio, por lo que un perfil recién creado aparece sin necesidad de volver a abrir el cuadro de diálogo.
- Para mantener la configuración de micrófono del perfil activo actualizada sin tener que volver a crearla manualmente, active **Auto-save profile changes** en la pestaña **Auto-Save**. Consulte [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md) para obtener más detalles. Tenga en cuenta que `AutoSaveTransmitProfile` se aplica tanto a la configuración de TX como a la de micrófono.

### Si intenta crear un perfil con un nombre existente

Si escribe un nombre que ya existe en la lista de perfiles y hace clic en **Create**, AetherSDR muestra un aviso:

> Ya existe un perfil de micrófono llamado "Desk Mic".  
> La radio no puede sobrescribir los perfiles de micrófono directamente; las actualizaciones se capturan mediante Auto-Save mientras el perfil está activo. Auto-Save está actualmente DESACTIVADO.  
> ¿Desea activar Auto-Save ahora para que sus cambios en "Desk Mic" se capturen?

Haga clic en **Enable Auto-Save** para activar el guardado automático de inmediato, luego active el perfil existente y aplique sus cambios; se guardarán automáticamente. La casilla de verificación Auto-Save en la pestaña **Auto-Save** se mantiene sincronizada con el estado de auto-guardado de la radio incluso si los cambios se originan fuera de este cuadro de diálogo (por ejemplo, desde otro cliente TCI o un cliente SmartSDR remoto).

## Solución de problemas

- **Load y Delete están atenuados** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo.
- **Create está atenuado** — El campo **Profile name** está vacío. Escriba un nombre antes de hacer clic en **Create**.
- **Create no hace nada** — Tanto el campo **Profile name** como la selección de la **Profile list** están vacíos. Escriba un nombre en **Profile name** antes de hacer clic en **Create**.
- **La Profile list está vacía** — Aún no se han guardado perfiles de micrófono en esta radio. Siga los pasos anteriores para crear el primero.
- **Aparece un mensaje de error después de Create** — Es posible que la radio haya rechazado la operación. Verifique que el nombre sea único y que la conexión con la radio sea estable. Si el error persiste, inténtelo de nuevo; si la radio no responde en 15 segundos, el cuadro de diálogo muestra un error de tiempo de espera.

## Relacionados

- [Cambiar el nombre o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
