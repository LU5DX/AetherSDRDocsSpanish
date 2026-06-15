# Administrador de perfiles

Utilice el Administrador de perfiles para crear, renombrar, cargar y eliminar perfiles Globales, de Transmisión y de Micrófono en la radio, así como para activar o desactivar el guardado automático de los cambios de transmisión.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.
- Familiarícese con las categorías de perfiles: los perfiles Globales almacenan la configuración general de la radio; los perfiles de Transmisión y Micrófono almacenan ajustes específicos de transmisión.

## Abrir el Administrador de perfiles

Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.

## Función de cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| `Global (pestaña)` | Pestaña | Administra los perfiles globales. | — |
| `Transmit (pestaña)` | Pestaña | Administra los perfiles de transmisión. | — |
| `Microphone (pestaña)` | Pestaña | Administra los perfiles de micrófono. | — |
| `Auto-Save (pestaña)` | Pestaña | Controla el guardado automático de perfiles. | — |
| `Profile name` | Campo de texto | Nombre que se usará al guardar un nuevo perfil. Si se deja vacío al hacer clic en Save y hay un perfil seleccionado en la lista, se usará el nombre del perfil seleccionado. | — |
| `Profile list` | Lista | Muestra todos los perfiles existentes para la categoría seleccionada. El perfil activo aparece resaltado. | — |
| `Load` | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. | — |
| `Save` | Botón | Guarda el estado actual de la radio con el nombre escrito en `Profile name`. | — |
| `Delete` | Botón | Elimina el perfil seleccionado después de un mensaje de confirmación. Solo se habilita cuando hay un perfil seleccionado. | — |
| `Close` | Botón | Cierra el diálogo del Administrador de perfiles. | — |
| `Auto-save profile changes` | Casilla de verificación | Cuando está activada, los cambios de TX se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |

## Comportamiento específico de cada pestaña

### Pestaña Global

- El botón `Save` crea o sobrescribe un perfil global. Ingrese un nombre nuevo para crear un perfil, o seleccione uno existente y haga clic en `Save` para sobrescribirlo.

### Pestañas Transmit y Microphone

- El botón `Save` se muestra como **Create** en lugar de **Save**. El firmware de la radio no permite sobrescribir directamente los perfiles de transmisión o micrófono. Al hacer clic en `Create`, siempre se crea un perfil nuevo con un nombre único.
- Si ya existe un perfil con el nombre escrito, aparece un diálogo que ofrece activar **Auto-Save**. Al hacer clic en el botón Enable Auto-Save de este diálogo, se envía el comando `profile autosave on` a la radio. La casilla Auto-Save de la pestaña Auto-Save se actualiza automáticamente según la confirmación de la radio.
- Una nota debajo de los botones explica: "Las actualizaciones a perfiles existentes se guardan automáticamente; active Auto-Save (pestaña Auto-Save) para que los cambios sigan al perfil activo. Create crea un perfil nuevo; no sobrescribe uno existente".
- El botón `Load` utiliza el comando de firmware `profile tx load` (en la pestaña Transmit) y `profile mic load` (en la pestaña Microphone) para cargar el perfil seleccionado.

### Pestaña Auto-Save

- Marque `Auto-save profile changes` para activar el guardado automático de los cambios en los perfiles de transmisión y micrófono.
- Cuando está activado, cualquier ajuste que realice en un perfil activo de transmisión o micrófono se escribe inmediatamente en ese perfil en la radio. No es necesario guardar manualmente.
- La casilla se mantiene sincronizada con el estado real de auto-guardado de la radio, incluso cuando el auto-guardado se activa o desactiva mediante:
  - El botón Enable Auto-Save en el diálogo de nombre duplicado de las pestañas Transmit o Microphone
  - Clientes TCI que envían comandos de auto-guardado
  - La carga de un perfil que tiene el auto-guardado activado o desactivado
  - Clientes remotos SmartSDR
- La casilla ignora su propia señal de cambio al sincronizarse desde la radio, evitando bucles de realimentación.

## Consejos

- Al hacer clic en un perfil existente en la `Profile list`, el campo `Profile name` se rellena con el nombre de ese perfil. Si luego hace clic en `Save` en la pestaña Global, el perfil existente se sobrescribe con el estado actual de la radio.
- También puede hacer doble clic en un perfil de la `Profile list` para cargarlo inmediatamente sin necesidad de hacer clic en `Load`.
- La `Profile list` se actualiza automáticamente cuando la radio confirma el guardado. No es necesario cerrar y volver a abrir el diálogo para ver la nueva entrada.
- Para los perfiles de transmisión y micrófono, active Auto-Save antes de realizar ajustes para no perder los cambios.

## Solución de problemas

- **Save no tiene efecto y el perfil no aparece en la lista** — Confirme que la radio esté conectada. El Administrador de perfiles requiere una conexión activa con la radio; si la conexión se perdió, reconéctese mediante `Settings > Connect to Radio...` e intente nuevamente.
- **Hacer clic en Save con el campo `Profile name` vacío no hace nada** — Escriba un nombre en `Profile name` o seleccione primero un perfil existente en la `Profile list` (su nombre llenará el campo automáticamente).
- **No se puede sobrescribir un perfil de transmisión o micrófono** — Esto es intencional. Use `Create` para crear un perfil nuevo, o active Auto-Save para que los cambios al perfil activo se guarden automáticamente.
- **La casilla Auto-Save parece cambiar por sí sola** — Esto es normal. La casilla refleja el estado real de auto-guardado de la radio. Puede actualizarse cuando activa Auto-Save desde la pestaña Transmit o Microphone, o cuando otro cliente cambia el auto-guardado en la radio.

## Relacionado

- [Descripción general del Administrador de perfiles](overview.md)
- [Revise la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
- [Cambie a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Active el auto-guardado para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
