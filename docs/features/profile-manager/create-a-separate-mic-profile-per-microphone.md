# Crear un perfil de micrófono independiente para cada micrófono

La pestaña Microphone en el Profile Manager permite guardar, cargar y eliminar perfiles de micrófono almacenados en la radio. Al guardar un perfil con nombre para cada micrófono físico, puede cambiar la configuración del micrófono al instante sin tener que volver a introducir manualmente los valores de EQ, nivel y procesamiento.

**Nota:** Para los perfiles de micrófono, la radio solo admite la creación de perfiles nuevos; no puede sobrescribir un perfil de micrófono existente directamente. Para actualizar un perfil existente con nuevos ajustes, active ese perfil y habilite **Auto-Save** (consulte los pasos a continuación y el artículo relacionado *Turn on auto-save*).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Profile Manager requiere una conexión activa con la radio.
- Configure los ajustes de micrófono de la radio para el primer micrófono antes de guardar. El perfil captura el estado actual en el momento en que hace clic en Create.

## Pasos

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Configure los ajustes de micrófono de la radio (nivel, EQ, procesamiento) para el primer micrófono si aún no lo ha hecho.
4. Haga clic en el campo **Profile name** y escriba un nombre para este micrófono; por ejemplo, `Desk Mic`.
5. Haga clic en **Create**. El perfil aparece en la **Profile list**.
6. Conecte o seleccione su segundo micrófono y ajuste la configuración de micrófono de la radio para adaptarlo.
7. Haga clic en el campo **Profile name**, borre el texto existente y escriba un nombre para el segundo micrófono; por ejemplo, `Headset`.
8. Haga clic en **Create**. El segundo perfil aparece ahora en la **Profile list** junto al primero.
9. Para cambiar entre micrófonos en sesiones futuras, seleccione el nombre del perfil en la **Profile list** y haga clic en **Load**, o haga doble clic en el nombre del perfil.
10. Haga clic en **Close** cuando haya terminado.

## Función de cada control

| Control | Tipo | Comportamiento | Setting key |
|---|---|---|---|
| **Microphone (tab)** | Pestaña | Muestra los perfiles de micrófono almacenados en la radio. | — |
| **Profile name** | Campo de texto | Nombre que se utiliza al guardar un nuevo perfil de micrófono. Se completa automáticamente al seleccionar un elemento en la lista. | — |
| **Profile list** | Lista | Todos los perfiles de micrófono en la radio; el perfil activo está resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Create** | Botón | Crea un nuevo perfil de micrófono con el nombre indicado en **Profile name**. Si **Profile name** está vacío, utiliza el nombre del elemento seleccionado en la lista. La radio no admite sobrescribir un perfil de micrófono existente; use Auto-Save para capturar cambios en un perfil activo. | — |
| **Delete** | Botón | Elimina el perfil seleccionado después de la confirmación. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el cuadro de diálogo Profile Manager. | — |

### Nota adicional (visible en la pestaña Microphone)

Una etiqueta debajo de los botones indica lo siguiente:

> Las actualizaciones de perfiles existentes se guardan automáticamente: active Auto-Save (pestaña Auto-Save) para que los cambios sigan al perfil activo. Create crea un perfil nuevo; no sobrescribe uno existente.

## Consejos

- Al seleccionar un perfil en la **Profile list**, su nombre se copia en el campo **Profile name**.
- La **Profile list** se actualiza automáticamente cuando la radio informa de un cambio, por lo que un perfil recién creado aparece sin necesidad de volver a abrir el cuadro de diálogo.
- Para mantener actualizados los ajustes de micrófono del perfil activo sin tener que volver a crearlos manualmente, active **Auto-save profile changes** en la pestaña **Auto-Save**. Consulte [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md) para obtener más detalles. Tenga en cuenta que `AutoSaveTransmitProfile` se aplica tanto a los ajustes de TX como a los de micrófono.

### Si intenta crear un perfil con un nombre existente

Si escribe un nombre que ya existe en la lista de perfiles y hace clic en **Create**, AetherSDR muestra un mensaje:

> Ya existe un perfil de micrófono llamado "Desk Mic".  
> La radio no puede sobrescribir perfiles de micrófono directamente: las actualizaciones se capturan mediante Auto-Save mientras el perfil está activo. Auto-Save está actualmente DESACTIVADO.  
> ¿Desea activar Auto-Save ahora para que sus cambios en "Desk Mic" se capturen?

Haga clic en **Enable Auto-Save** para activar el guardado automático de inmediato; luego active el perfil existente y aplique sus cambios; se guardarán automáticamente.

## Solución de problemas

- **Load y Delete están atenuados** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo.
- **Create no hace nada** — Tanto el campo **Profile name** como la selección de la **Profile list** están vacíos. Escriba un nombre en **Profile name** antes de hacer clic en **Create**.
- **La Profile list está vacía** — Aún no se han guardado perfiles de micrófono en esta radio. Siga los pasos anteriores para crear el primero.

## Relacionados

- [Rename or delete a microphone profile](rename-or-delete-a-microphone-profile.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
