# Guardar el estado actual de la radio como un nuevo perfil global

Use esta página para capturar el estado actual de la radio y almacenarlo como un perfil global con nombre. Los perfiles globales registran la configuración general de la radio para que pueda volver a una configuración conocida más adelante.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Decida un nombre para el nuevo perfil antes de empezar.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.
2. Haga clic en la pestaña `Global (tab)` si no está ya seleccionada.
3. En el campo `Profile name`, escriba el nombre del nuevo perfil.
4. Haga clic en `Save`.

La radio guarda el estado actual con el nombre que escribió. El campo `Profile name` se limpia y la radio envía una lista actualizada de vuelta a la `Profile list`.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| `Profile name` | Campo de texto | Nombre que se usa al guardar un nuevo perfil. Si se deja en blanco al hacer clic en Save y hay un perfil seleccionado en la lista, se usa el nombre del perfil seleccionado. | — |
| `Profile list` | Lista | Muestra todos los perfiles existentes para la categoría seleccionada. El perfil activo está resaltado. | — |
| `Load` | Botón | Carga el perfil seleccionado en la radio. Solo está habilitado cuando hay un perfil seleccionado. | — |
| `Save` | Botón | Guarda el estado actual de la radio con el nombre escrito en `Profile name`. | — |
| `Delete` | Botón | Elimina el perfil seleccionado después de un mensaje de confirmación. Solo está habilitado cuando hay un perfil seleccionado. | — |
| `Close` | Botón | Cierra el diálogo del Administrador de perfiles. | — |
| `Auto-Save (tab)` | Pestaña | Abre la pestaña de Guardado automático para controlar el guardado automático de perfiles. | — |
| `Auto-save profile changes` | Casilla de verificación | Cuando está activada, los cambios de TX se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |

## Comportamiento específico por pestaña

### Pestaña Global

- El botón `Save` crea o sobrescribe un perfil global. Escriba un nombre nuevo para crear un perfil, o seleccione uno existente y haga clic en `Save` para sobrescribirlo.

### Pestañas Transmit y Microphone

- El botón `Save` se etiqueta como **Create** en lugar de **Save**. El firmware de la radio no admite sobrescribir directamente perfiles de transmisión o de micrófono. Al hacer clic en `Create` siempre se crea un nuevo perfil con un nombre único.
- Si ya existe un perfil con el nombre escrito, aparece un diálogo que ofrece habilitar **Auto-Save**. Al hacer clic en el botón Habilitar Auto-Save en este diálogo, se envía el comando `profile autosave on` a la radio. La casilla Auto-Save en la pestaña Auto-Save se actualiza automáticamente en respuesta a la confirmación de la radio.
- Una nota debajo de los botones explica: "Las actualizaciones a perfiles existentes se guardan automáticamente: active Auto-Save (pestaña Auto-Save) para que los cambios sigan al perfil activo. Create crea un perfil nuevo; no sobrescribe uno existente."

### Pestaña Auto-Save

- Marque `Auto-save profile changes` para habilitar el guardado automático de cambios en perfiles de transmisión y micrófono.
- Cuando está activada, cualquier ajuste que realice en un perfil de transmisión o micrófono activo se escribe inmediatamente de vuelta en ese perfil en la radio. No es necesario guardar manualmente.
- La casilla se mantiene sincronizada con el estado real de guardado automático de la radio, incluso cuando el guardado automático se activa o desactiva mediante:
  - El botón Habilitar Auto-Save en el diálogo de nombre duplicado de la pestaña Transmit o Microphone
  - Clientes TCI que envían comandos de guardado automático
  - La carga de un perfil que tenga el guardado automático activado o desactivado
  - Clientes SmartSDR remotos
- La casilla ignora su propia señal de activación/desactivación al sincronizar desde la radio, lo que evita bucles de realimentación.

## Consejos

- Al hacer clic en un perfil existente en la `Profile list`, se rellena el campo `Profile name` con el nombre de ese perfil. Si luego hace clic en `Save` en la pestaña Global, el perfil existente se sobrescribe con el estado actual de la radio.
- También puede hacer doble clic en un perfil de la `Profile list` para cargarlo inmediatamente sin hacer clic en `Load`.
- La `Profile list` se actualiza automáticamente cuando la radio confirma el guardado. No es necesario cerrar y volver a abrir el diálogo para ver la nueva entrada.
- Para perfiles de transmisión y micrófono, active Auto-Save antes de hacer ajustes para no perder los cambios.

## Solución de problemas

- **Save no tiene efecto y el perfil no aparece en la lista** — Confirme que la radio está conectada. El Administrador de perfiles requiere una conexión activa con la radio; si la conexión se perdió, reconéctese mediante `Settings > Connect to Radio...` e intente de nuevo.
- **Al hacer clic en Save con el campo `Profile name` vacío no sucede nada** — Escriba un nombre en `Profile name` o seleccione primero un perfil existente en la `Profile list` (su nombre llenará el campo automáticamente).
- **No se puede sobrescribir un perfil de transmisión o micrófono** — Esto es intencional. Use `Create` para crear un perfil nuevo, o active Auto-Save para que los cambios en el perfil activo se guarden automáticamente.
- **La casilla Auto-Save parece cambiar sola** — Esto es normal. La casilla refleja el estado real de guardado automático de la radio. Puede actualizarse cuando activa Auto-Save desde la pestaña Transmit o Microphone, o cuando otro cliente activa o desactiva el guardado automático en la radio.

## Relacionados

- [Descripción general del Administrador de perfiles](overview.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
