# Guardar el estado actual de la radio como un nuevo perfil global

Use esta página para capturar el estado actual de la radio y almacenarlo como un perfil global con nombre. Los perfiles globales registran la configuración general de la radio para que pueda volver a una configuración conocida más adelante.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Decida un nombre para el nuevo perfil antes de comenzar.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.
2. Haga clic en la pestaña `Global (tab)` si aún no está seleccionada.
3. En el campo `Profile name`, escriba el nombre para el nuevo perfil.
4. Haga clic en `Save`.

La radio guarda el estado actual con el nombre que escribió. El campo `Profile name` se limpia y la radio envía una lista actualizada de vuelta a la `Profile list`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| `Profile name` | Campo de texto | Nombre que se usa al guardar un nuevo perfil. Si se deja en blanco al hacer clic en Save y hay un perfil seleccionado en la lista, se usa el nombre del perfil seleccionado. | — |
| `Profile list` | Lista | Muestra todos los perfiles globales existentes. El perfil activo está resaltado. | — |
| `Load` | Botón | Carga el perfil seleccionado en la radio. Habilitado solo cuando hay un perfil seleccionado. | — |
| `Save` | Botón | Guarda el estado actual de la radio con el nombre escrito en `Profile name`. | — |
| `Delete` | Botón | Elimina el perfil seleccionado después de un mensaje de confirmación. Habilitado solo cuando hay un perfil seleccionado. | — |
| `Close` | Botón | Cierra el diálogo del Administrador de perfiles. | — |

## Consejos

- Al hacer clic en un perfil existente en la `Profile list`, se rellena el campo `Profile name` con el nombre de ese perfil. Si luego hace clic en `Save`, el perfil existente se sobrescribe con el estado actual de la radio.
- También puede hacer doble clic en un perfil de la `Profile list` para cargarlo inmediatamente sin hacer clic en `Load`.
- La `Profile list` se actualiza automáticamente cuando la radio confirma el guardado. No necesita cerrar y volver a abrir el diálogo para ver la nueva entrada.

## Solución de problemas

- **Save no tiene efecto y el perfil no aparece en la lista** — Confirme que la radio está conectada. El Administrador de perfiles requiere una conexión activa con la radio; si la conexión se perdió, vuelva a conectarla mediante `Settings > Connect to Radio...` e intente de nuevo.
- **Hacer clic en Save con el campo `Profile name` vacío no hace nada** — Escriba un nombre en `Profile name` o seleccione primero un perfil existente en la `Profile list` (su nombre rellenará el campo automáticamente).

## Relacionados

- [Profile Manager overview](overview.md)
- [Review the list of active global profiles](review-the-list-of-active-global-profiles.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
