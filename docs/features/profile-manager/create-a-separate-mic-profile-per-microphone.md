# Crear un perfil de micrófono independiente por cada micrófono

Use el Profile Manager para guardar un perfil de micrófono con nombre para cada micrófono físico que utilice. Al cambiar de perfil se restauran los ajustes correctos del micrófono sin necesidad de configurarlos manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Profile Manager requiere una conexión de radio activa.
- Configure los ajustes de micrófono de la radio (ganancia, EQ, etc.) para el primer micrófono antes de guardar.

## Pasos

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Escriba un nombre para este micrófono en el campo **Profile name** (por ejemplo, el modelo del micrófono o su caso de uso).
4. Haga clic en **Save**. El perfil se crea en la radio y aparece en la lista **Profile list**.
5. Conecte o seleccione su segundo micrófono y ajuste los parámetros de micrófono de la radio para él.
6. Repita los pasos 3–4 con un nombre diferente para el segundo micrófono.
7. Para cambiar entre micrófonos, seleccione el perfil correspondiente en la lista **Profile list** y haga clic en **Load**, o haga doble clic en el nombre del perfil. La radio carga esos ajustes de micrófono de inmediato.
8. Haga clic en **Close** cuando haya terminado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Microphone** (pestaña) | Pestaña | Administra los perfiles de micrófono almacenados en la radio. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un nuevo perfil. Se rellena automáticamente al seleccionar un perfil existente de la lista. | — |
| **Profile list** | Lista | Todos los perfiles de micrófono de la radio; el perfil activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Se habilita únicamente cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual del micrófono de la radio con el nombre indicado en **Profile name**. Si el campo está vacío, sobreescribe el perfil seleccionado. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras una confirmación. Se habilita únicamente cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo del Profile Manager. | — |

## Consejos

- Al seleccionar un perfil en la lista **Profile list**, su nombre se copia en el campo **Profile name**. Edite ese nombre antes de hacer clic en **Save** para guardarlo como un nuevo perfil en lugar de sobreescribir el existente.
- Si desea que los cambios del micrófono se guarden automáticamente en el perfil activo sin necesidad de hacer clic manualmente en **Save**, habilite **Auto-save profile changes** en la pestaña **Auto-Save**. Esto se controla mediante el ajuste `AutoSaveTransmitProfile`.

## Relacionado

- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Descripción general del Profile Manager](overview.md)
