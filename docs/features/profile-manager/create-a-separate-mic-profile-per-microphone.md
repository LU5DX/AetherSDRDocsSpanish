# Crear un perfil de micrófono independiente para cada micrófono

La pestaña Micrófono en el Administrador de perfiles le permite guardar, cargar y eliminar perfiles de micrófono almacenados en la radio. Al guardar un perfil con nombre para cada micrófono físico, puede cambiar la configuración del micrófono al instante sin tener que volver a ingresar manualmente los valores de ecualización, nivel y procesamiento.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Configure los ajustes de micrófono de la radio para el primer micrófono antes de guardar. El perfil captura el estado actual en el momento en que hace clic en Guardar.

## Pasos

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Configure los ajustes de micrófono de la radio (nivel, ecualización, procesamiento) para el primer micrófono si aún no lo ha hecho.
4. Haga clic en el campo **Profile name** y escriba un nombre para este micrófono — por ejemplo, `Desk Mic`.
5. Haga clic en **Save**. El perfil aparece en la **Profile list**.
6. Conecte o seleccione su segundo micrófono y ajuste la configuración de micrófono de la radio según corresponda.
7. Haga clic en el campo **Profile name**, borre cualquier texto existente y escriba un nombre para el segundo micrófono — por ejemplo, `Headset`.
8. Haga clic en **Save**. El segundo perfil ahora aparece en la **Profile list** junto al primero.
9. Para cambiar entre micrófonos en sesiones futuras, seleccione el nombre del perfil en la **Profile list** y haga clic en **Load**, o haga doble clic en el nombre del perfil.
10. Haga clic en **Close** cuando haya terminado.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Microphone (tab)** | Pestaña | Muestra los perfiles de micrófono almacenados en la radio. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un nuevo perfil de micrófono. Se completa automáticamente al seleccionar un elemento en la lista. | — |
| **Profile list** | Lista | Todos los perfiles de micrófono en la radio; el perfil activo está resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual del micrófono de la radio con el nombre en **Profile name**. Si **Profile name** está vacío, utiliza el nombre del elemento seleccionado en la lista. | — |
| **Delete** | Botón | Elimina el perfil seleccionado después de la confirmación. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo del Administrador de perfiles. | — |

## Consejos

- Al seleccionar un perfil en la **Profile list**, su nombre se copia en el campo **Profile name**. Si desea sobrescribir un perfil existente con ajustes actualizados, simplemente selecciónelo y haga clic en **Save** sin cambiar el nombre.
- La **Profile list** se actualiza automáticamente cuando la radio reporta un cambio, por lo que un perfil recién guardado aparece sin necesidad de volver a abrir el diálogo.
- Para mantener actualizados los ajustes de micrófono del perfil activo sin guardarlos manualmente, active **Auto-save profile changes** en la pestaña **Auto-Save**. Consulte [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md) para más detalles. Tenga en cuenta que `AutoSaveTransmitProfile` se aplica tanto a los ajustes de TX como a los de micrófono.

## Solución de problemas

- **Load y Delete aparecen atenuados** — No hay ningún perfil seleccionado en la **Profile list**. Haga clic en un nombre de perfil para seleccionarlo.
- **Save no hace nada** — Tanto el campo **Profile name** como la selección en la **Profile list** están vacíos. Escriba un nombre en **Profile name** antes de hacer clic en **Save**.
- **Profile list está vacía** — Aún no se han guardado perfiles de micrófono en esta radio. Siga los pasos anteriores para crear el primero.

## Relacionados

- [Rename or delete a microphone profile](rename-or-delete-a-microphone-profile.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
