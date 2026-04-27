# Crear un perfil de micrófono independiente por cada micrófono

La pestaña Microphone en Profile Manager permite guardar, cargar y eliminar perfiles de micrófono almacenados en el equipo. Al guardar un perfil con nombre para cada micrófono físico, puede cambiar la configuración del micrófono de forma instantánea sin tener que volver a introducir manualmente los valores de ecualización, nivel y procesamiento.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Profile Manager requiere una conexión activa con el equipo.
- Configure los ajustes de micrófono del equipo para el primer micrófono antes de guardar. El perfil captura el estado actual en el momento en que hace clic en Save.

## Pasos

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Configure los ajustes de micrófono del equipo (nivel, ecualización, procesamiento) para el primer micrófono, si aún no lo ha hecho.
4. Haga clic en el campo **Profile name** y escriba un nombre para este micrófono — por ejemplo, `Desk Mic`.
5. Haga clic en **Save**. El perfil aparece en la lista **Profile list**.
6. Conecte o seleccione su segundo micrófono y ajuste la configuración de micrófono del equipo según corresponda.
7. Haga clic en el campo **Profile name**, borre el texto existente y escriba un nombre para el segundo micrófono — por ejemplo, `Headset`.
8. Haga clic en **Save**. El segundo perfil aparece ahora en la lista **Profile list** junto al primero.
9. Para cambiar entre micrófonos en sesiones futuras, seleccione el nombre del perfil en la lista **Profile list** y haga clic en **Load**, o haga doble clic sobre el nombre del perfil.
10. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Microphone (pestaña)** | Pestaña | Muestra los perfiles de micrófono almacenados en el equipo. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un nuevo perfil de micrófono. Se rellena automáticamente al seleccionar un elemento de la lista. | — |
| **Profile list** | Lista | Todos los perfiles de micrófono del equipo; el perfil activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en el equipo. Se activa únicamente cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual del micrófono del equipo con el nombre indicado en **Profile name**. Si **Profile name** está vacío, utiliza el nombre del elemento seleccionado en la lista. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras solicitar confirmación. Se activa únicamente cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo Profile Manager. | — |

## Consejos

- Al seleccionar un perfil en la lista **Profile list**, su nombre se copia automáticamente en el campo **Profile name**. Si desea sobrescribir un perfil existente con ajustes actualizados, simplemente selecciónelo y haga clic en **Save** sin cambiar el nombre.
- La lista **Profile list** se actualiza automáticamente cuando el equipo notifica un cambio, por lo que un perfil recién guardado aparece sin necesidad de volver a abrir el diálogo.
- Para mantener actualizados los ajustes de micrófono del perfil activo sin tener que guardar manualmente, active **Auto-save profile changes** en la pestaña **Auto-Save**. Consulte [Activar el guardado automático para que los ajustes de TX siempre se conserven](turn-on-auto-save-so-tx-tweaks-always-persist.md) para más detalles. Tenga en cuenta que `AutoSaveTransmitProfile` se aplica tanto a los ajustes de TX como a los de micrófono.

## Solución de problemas

- **Load y Delete aparecen en gris** — No hay ningún perfil seleccionado en la lista **Profile list**. Haga clic en el nombre de un perfil para seleccionarlo.
- **Save no hace nada** — Tanto el campo **Profile name** como la selección en **Profile list** están vacíos. Escriba un nombre en **Profile name** antes de hacer clic en **Save**.
- **La lista Profile list está vacía** — Todavía no se ha guardado ningún perfil de micrófono en este equipo. Siga los pasos anteriores para crear el primero.

## Temas relacionados

- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre se conserven](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
