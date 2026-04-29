# Guardar el estado actual de la radio como un nuevo perfil global

Use esta página para capturar el estado actual de la radio y almacenarlo como un perfil global con nombre. Los perfiles globales registran la configuración general de la radio para que pueda volver a una configuración conocida más adelante.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Profile Manager requiere una conexión activa con la radio.
- Decida el nombre del nuevo perfil antes de empezar.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña `Global (tab)` si no está ya seleccionada.
3. En el campo `Profile name`, escriba el nombre del nuevo perfil.
4. Haga clic en `Save`.

La radio guarda el estado actual con el nombre que escribió. El campo `Profile name` se vacía y la radio envía una lista actualizada de vuelta a `Profile list`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| `Profile name` | Campo de texto | Nombre utilizado al guardar un nuevo perfil. Si se deja en blanco al hacer clic en Save y hay un perfil seleccionado en la lista, se usa el nombre del perfil seleccionado. | — |
| `Profile list` | Lista | Muestra todos los perfiles globales existentes. El perfil activo aparece resaltado. | — |
| `Load` | Botón | Carga el perfil seleccionado en la radio. Se activa únicamente cuando hay un perfil seleccionado. | — |
| `Save` | Botón | Guarda el estado actual de la radio con el nombre escrito en `Profile name`. | — |
| `Delete` | Botón | Elimina el perfil seleccionado tras una confirmación. Se activa únicamente cuando hay un perfil seleccionado. | — |
| `Close` | Botón | Cierra el diálogo Profile Manager. | — |

## Consejos

- Al hacer clic en un perfil existente en `Profile list`, el campo `Profile name` se rellena automáticamente con el nombre de ese perfil. Si luego hace clic en `Save`, el perfil existente se sobrescribe con el estado actual de la radio.
- También puede hacer doble clic en un perfil de `Profile list` para cargarlo de inmediato sin necesidad de hacer clic en `Load`.
- `Profile list` se actualiza automáticamente cuando la radio confirma el guardado. No es necesario cerrar y volver a abrir el diálogo para ver la nueva entrada.

## Solución de problemas

- **Save no tiene efecto y el perfil no aparece en la lista** — Confirme que la radio está conectada. El Profile Manager requiere una conexión activa con la radio; si la conexión se interrumpió, vuelva a conectar mediante `Settings > Connect to Radio...` e inténtelo de nuevo.
- **Al hacer clic en Save con el campo `Profile name` vacío no ocurre nada** — Escriba un nombre en `Profile name` o seleccione primero un perfil existente en `Profile list` (su nombre rellenará el campo automáticamente).

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
