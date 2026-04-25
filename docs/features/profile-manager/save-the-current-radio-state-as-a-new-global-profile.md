# Guardar el estado actual de la radio como un nuevo perfil global

Use esta página para capturar el estado actual de la radio — frecuencias, modos y configuraciones — como un perfil global con nombre que podrá recargar más adelante.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Decida el nombre del nuevo perfil antes de abrir el cuadro de diálogo.

## Pasos

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Global**.
3. En el campo **Profile name**, escriba el nombre del nuevo perfil.
4. Haga clic en **Save**.

La radio guarda el estado actual con ese nombre. La **Profile list** se actualiza automáticamente cuando la radio confirma el nuevo perfil.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Global (tab)** | Pestaña | Cambia a la vista de perfiles globales. | — |
| **Profile name** | Campo de texto | Nombre que se usa al guardar un nuevo perfil. Si se deja en blanco, **Save** utiliza el nombre del elemento actualmente seleccionado en la **Profile list**. | — |
| **Profile list** | Lista | Muestra todos los perfiles globales existentes. El perfil activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre escrito en **Profile name**. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras un aviso de confirmación. Solo se habilita cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el cuadro de diálogo Profile Manager. | — |

## Consejos

- Si selecciona un perfil existente en la **Profile list**, su nombre se escribe automáticamente en el campo **Profile name**. Al hacer clic en **Save** en ese momento, se sobrescribe ese perfil con el estado actual de la radio.
- También puede cargar un perfil haciendo doble clic en su entrada en la **Profile list**, en lugar de usar **Load**.
- Para que los cambios de transmisión se escriban automáticamente de vuelta al perfil activo, habilite **Auto-save profile changes** en la pestaña **Auto-Save**. Esta configuración se almacena como `AutoSaveTransmitProfile`.

## Solución de problemas

- **Save no hace nada** — Verifique que el campo **Profile name** no esté vacío y que ningún perfil de la lista esté seleccionado con el campo de nombre en blanco. Para que **Save** funcione, debe existir al menos una fuente de nombre.
- **La Profile list no se actualiza después de guardar** — La lista se actualiza cuando la radio envía una actualización de estado. Si no aparece, verifique que la conexión con la radio siga activa mediante `Settings > Connect to Radio...`.

## Relacionados

- [Descripción general del Profile Manager](overview.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
