# Crear un perfil de micrófono independiente por cada micrófono

Use el Profile Manager para guardar un perfil de micrófono dedicado a cada micrófono físico que utilice. Al cambiar de micrófono, bastará con una acción de carga en lugar de ajustar manualmente la configuración del micrófono cada vez.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Configure los ajustes de micrófono del radio (ganancia, EQ, etc.) para el micrófono que desea guardar antes de abrir el diálogo.

## Pasos

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. En el campo **Profile name**, escriba un nombre que identifique el micrófono (por ejemplo, `Heil PR-40` o `Desk Mic`).
4. Haga clic en **Save**. El perfil aparece en la lista **Profile list**.
5. Repita los pasos 3–4 para cada micrófono adicional, ajustando la configuración de micrófono del radio antes de cada guardado.
6. Para cambiar a un perfil de micrófono guardado, selecciónelo en la lista **Profile list** y haga clic en **Load**, o haga doble clic en su entrada en la lista.
7. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Microphone** (pestaña) | Pestaña | Muestra los perfiles de micrófono almacenados en el radio. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un nuevo perfil de micrófono. Al seleccionar un perfil existente, este campo se rellena automáticamente. | — |
| **Profile list** | Lista | Todos los perfiles de micrófono en el radio; el activo en ese momento aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en el radio. También se activa haciendo doble clic en una entrada de la lista. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual del micrófono del radio con el nombre indicado en **Profile name**. Si **Profile name** está vacío y hay un perfil seleccionado, guarda con el nombre de ese perfil. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras confirmación. Solo está habilitado cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo. | — |

## Consejos

- Al seleccionar un perfil en la lista **Profile list**, su nombre aparece automáticamente en el campo **Profile name**. Edite el texto antes de hacer clic en **Save** para guardar una copia con un nuevo nombre sin sobrescribir el original.
- Si desea que los cambios del micrófono se escriban automáticamente en el perfil activo cada vez que los ajuste, habilite **Auto-save profile changes** en la pestaña **Auto-Save**. Esto se controla mediante la configuración `AutoSaveTransmitProfile`.

## Solución de problemas

- **Load y Delete aparecen en gris** — no hay ningún perfil seleccionado en la lista **Profile list**. Haga clic en el nombre de un perfil para seleccionarlo.
- **Save no hace nada** — el campo **Profile name** está vacío y no hay ningún perfil seleccionado. Escriba un nombre en **Profile name** y haga clic en **Save** nuevamente.
- **La lista Profile list está vacía después de guardar** — el radio actualiza la lista mediante una notificación de estado. Si la lista no se actualiza, cierre y vuelva a abrir el diálogo para forzar una nueva consulta.

## Relacionados

- [Descripción general del Profile Manager](overview.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
