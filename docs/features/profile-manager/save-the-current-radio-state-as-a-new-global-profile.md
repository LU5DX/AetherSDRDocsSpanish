# Guardar el estado actual de la radio como un nuevo perfil global

Use esta página para capturar el estado actual de la radio y almacenarlo como un perfil global con nombre. Los perfiles globales registran la configuración general de la radio para que pueda volver a una configuración conocida más adelante.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El administrador de perfiles requiere una conexión activa con la radio.
- Decida un nombre para el nuevo perfil antes de comenzar.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del administrador de perfiles.
2. Haga clic en la pestaña `Global (tab)` si aún no está seleccionada.
3. En el campo `Profile name`, escriba el nombre del nuevo perfil.
4. Haga clic en `Save`.

La radio guarda el estado actual con el nombre que escribió. El campo `Profile name` se limpia y la radio envía una lista actualizada de vuelta a la `Profile list`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| `Profile name` | Campo de texto | Nombre usado al guardar un nuevo perfil. Si se deja en blanco al hacer clic en Save y hay un perfil seleccionado en la lista, se usa el nombre del perfil seleccionado. | — |
| `Profile list` | Lista | Muestra todos los perfiles globales existentes. El perfil activo está resaltado. | — |
| `Load` | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. | — |
| `Save` | Botón | Guarda el estado actual de la radio bajo el nombre escrito en `Profile name`. | — |
| `Delete` | Botón | Elimina el perfil seleccionado después de un mensaje de confirmación. Solo se habilita cuando hay un perfil seleccionado. | — |
| `Close` | Botón | Cierra el diálogo del administrador de perfiles. | — |
| `Auto-Save (tab)` | Pestaña | Abre la pestaña de guardado automático para controlar el guardado automático de perfiles. | — |
| `Auto-save profile changes` | Casilla de verificación | Cuando está activada, los cambios de TX se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |

## Comportamiento específico de cada pestaña

### Pestaña Global

- El botón `Save` crea o sobrescribe un perfil global. Ingrese un nombre nuevo para crear un perfil, o seleccione uno existente y haga clic en `Save` para sobrescribirlo.

### Pestañas Transmit y Microphone

- El botón `Save` se etiqueta como **Create** en lugar de **Save**. El firmware de la radio no admite la sobrescritura directa de perfiles de transmisión o micrófono. Al hacer clic en `Create`, siempre se crea un perfil nuevo con un nombre único.
- Si ya existe un perfil con el nombre escrito, aparece un diálogo que ofrece activar **Auto-Save**. Con Auto-Save activado, los cambios al perfil de transmisión o micrófono activo se capturan automáticamente mientras opera.
- Una nota debajo de los botones explica: "Las actualizaciones a perfiles existentes se guardan automáticamente: active Auto-Save (pestaña Auto-Save) para que los cambios sigan al perfil activo. Create crea un perfil nuevo; no sobrescribe uno existente."

### Pestaña Auto-Save

- Marque `Auto-save profile changes` para activar el guardado automático de cambios en los perfiles de transmisión y micrófono.
- Cuando está activado, cualquier ajuste que realice a un perfil de transmisión o micrófono activo se escribe de inmediato en ese perfil en la radio. No necesita guardar manualmente.

## Consejos

- Al hacer clic en un perfil existente en la `Profile list`, el campo `Profile name` se llena con el nombre de ese perfil. Si luego hace clic en `Save` en la pestaña Global, el perfil existente se sobrescribe con el estado actual de la radio.
- También puede hacer doble clic en un perfil de la `Profile list` para cargarlo inmediatamente sin hacer clic en `Load`.
- La `Profile list` se actualiza automáticamente cuando la radio confirma el guardado. No necesita cerrar y volver a abrir el diálogo para ver la nueva entrada.
- Para perfiles de transmisión y micrófono, active Auto-Save antes de hacer ajustes para no perder sus cambios.

## Solución de problemas

- **Save no tiene efecto y el perfil no aparece en la lista**: confirme que la radio esté conectada. El administrador de perfiles requiere una conexión activa con la radio; si la conexión se perdió, reconéctese mediante `Settings > Connect to Radio...` e intente de nuevo.
- **Hacer clic en Save con el campo `Profile name` vacío no hace nada**: escriba un nombre en `Profile name` o seleccione un perfil existente en la `Profile list` primero (su nombre llenará el campo automáticamente).
- **No se puede sobrescribir un perfil de transmisión o micrófono**: esto es por diseño. Use `Create` para crear un perfil nuevo, o active Auto-Save para que los cambios al perfil activo se guarden automáticamente.

## Relacionados

- [Profile Manager overview](overview.md)
- [Review the list of active global profiles](review-the-list-of-active-global-profiles.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
- [Turn on auto-save so TX tweaks always persist](turn-on-auto-save-so-tx-tweaks-always-persist.md)
