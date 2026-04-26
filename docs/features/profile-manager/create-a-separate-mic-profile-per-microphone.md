# Crear un perfil de micrófono independiente por cada micrófono

Use el Profile Manager para guardar un perfil de micrófono con nombre para cada micrófono físico que utilice. Cambiar de micrófono requiere entonces una sola operación de carga en lugar de ajustar manualmente la configuración del micrófono cada vez.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Configure los ajustes de micrófono del radio (ganancia, EQ, etc.) para el micrófono que desea guardar antes de crear el perfil.

## Pasos

1. Abra `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. Ajuste la configuración del micrófono en el radio para que corresponda al primer micrófono, si aún no lo ha hecho.
4. Haga clic en el campo **Profile name** y escriba un nombre para este micrófono (por ejemplo, el modelo o la posición del micrófono).
5. Haga clic en **Save**. El nuevo perfil aparece en la lista **Profile list**.
6. Repita los pasos 3–5 para cada micrófono adicional, usando un nombre distinto cada vez.

Para cambiar a un perfil de micrófono guardado posteriormente, selecciónelo en la lista **Profile list** y haga clic en **Load**, o haga doble clic directamente sobre el nombre del perfil.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| Pestaña **Microphone** | Pestaña | Muestra la lista de perfiles de micrófono y los controles asociados. | — |
| **Profile name** | Campo de texto | Nombre que se usa al guardar un nuevo perfil de micrófono. Se rellena automáticamente al seleccionar un perfil de la lista. | — |
| **Profile list** | Lista | Todos los perfiles de micrófono guardados; el activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil de micrófono seleccionado en el radio. Se habilita únicamente cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual del micrófono del radio con el nombre escrito en **Profile name**. Si **Profile name** está vacío y hay un perfil seleccionado, guarda sobre el nombre de ese perfil. | — |
| **Delete** | Botón | Elimina el perfil de micrófono seleccionado tras una confirmación. Se habilita únicamente cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo del Profile Manager. | — |

## Consejos

- Al seleccionar un perfil de la lista **Profile list**, su nombre se copia en el campo **Profile name**. Borre el campo y escriba un nombre nuevo antes de hacer clic en **Save** para crear un perfil nuevo en lugar de sobrescribir el existente.
- La lista **Profile list** se actualiza automáticamente si el radio envía cambios mientras el diálogo está abierto.
- Si también utiliza perfiles de transmisión, considere habilitar **Auto-save profile changes** en la pestaña **Auto-Save** para que los ajustes de micrófono realizados durante una sesión se escriban automáticamente en el perfil activo. Esta configuración se persiste como `AutoSaveTransmitProfile`.

## Solución de problemas

- **Load y Delete aparecen en gris** — No hay ningún perfil seleccionado. Haga clic en un nombre de la lista **Profile list** para seleccionarlo.
- **Hacer clic en Save no tiene efecto** — Tanto el campo **Profile name** como la selección en **Profile list** están vacíos. Escriba un nombre en **Profile name** antes de hacer clic en **Save**.
- **La lista Profile list está vacía** — El radio no tiene perfiles de micrófono guardados aún. Cree el primero siguiendo los pasos anteriores.

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Cambiar el nombre o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
