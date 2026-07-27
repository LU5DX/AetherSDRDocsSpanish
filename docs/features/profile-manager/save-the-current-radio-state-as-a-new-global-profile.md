# Administrador de Perfiles

Use el Administrador de Perfiles para crear, renombrar, cargar y eliminar perfiles Globales, de Transmisión y de Micrófono en la radio, así como para activar o desactivar el guardado automático de cambios de transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de Perfiles requiere una conexión activa con la radio.
- Familiarícese con las categorías de perfiles: los perfiles Globales almacenan la configuración general de la radio; los perfiles de Transmisión y Micrófono almacenan ajustes específicos de transmisión.

## Abrir el Administrador de Perfiles

Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de Perfiles.

## Función de cada control

| Control                     | Tipo         | Comportamiento                                                                                                                                                   |
|-----------------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Global (tab)`              | Pestaña      | Administra perfiles globales.                                                                                                                                    |
| `Transmit (tab)`            | Pestaña      | Administra perfiles de transmisión.                                                                                                                              |
| `Microphone (tab)`          | Pestaña      | Administra perfiles de micrófono.                                                                                                                                |
| `Auto-Save (tab)`           | Pestaña      | Controla el guardado automático de perfiles.                                                                                                                     |
| `Profile name`              | Campo texto  | Nombre usado al guardar un nuevo perfil. Si se deja en blanco al hacer clic en Save y hay un perfil seleccionado en la lista, se usará el nombre del perfil seleccionado. |
| `Profile list`              | Lista        | Muestra todos los perfiles existentes para la categoría seleccionada. El perfil activo está resaltado.                                                           |
| `Load`                      | Botón        | Carga el perfil seleccionado en la radio. Habilitado solo cuando hay un perfil seleccionado.                                                                     |
| `Save`                      | Botón        | Guarda el estado actual de la radio con el nombre escrito en `Profile name`. Deshabilitado cuando el campo de nombre está vacío.                                 |
| `Delete`                    | Botón        | Elimina el perfil seleccionado después de un mensaje de confirmación. Habilitado solo cuando hay un perfil seleccionado.                                         |
| `Close`                     | Botón        | Cierra el diálogo del Administrador de Perfiles.                                                                                                                 |
| `Auto-save profile changes` | Casilla      | Al activarla, los cambios de TX se guardan automáticamente en el perfil activo. El estado se lee en vivo del modelo de radio, no de la configuración local.      |

## Comportamiento específico por pestaña

### Pestaña Global

- El botón `Save` crea o sobrescribe un perfil global. Ingrese un nombre nuevo para crear un perfil, o seleccione uno existente y haga clic en `Save` para sobrescribirlo.
- Aparece una línea de resultado debajo de los botones después de un intento de guardado, mostrando éxito o fallo. Desaparece cuando edita el campo de nombre del perfil.
- El botón `Load` usa el comando de firmware `profile load` para cargar el perfil seleccionado.

### Pestañas de Transmisión y Micrófono

- El botón `Save` está etiquetado como **Create** en lugar de **Save**. El firmware de la radio no admite sobrescribir directamente perfiles de transmisión o micrófono. Al hacer clic en `Create` siempre se crea un nuevo perfil con un nombre único.
- Si ya existe un perfil con el nombre escrito, aparece un diálogo que ofrece activar **Auto-Save**. Al hacer clic en el botón Habilitar Auto-Save en este diálogo, se envía el comando `profile autosave on` a la radio. La casilla Auto-Save en la pestaña Auto-Save se actualiza automáticamente en respuesta a la confirmación de la radio.
- Una nota debajo de los botones explica: "Las actualizaciones a perfiles existentes se guardan automáticamente — active Auto-Save (pestaña Auto-Save) para que los cambios sigan al perfil activo. Create crea un perfil nuevo; no sobrescribe uno existente."
- El botón `Load` usa el comando de firmware `profile tx load` (en la pestaña Transmit) y `profile mic load` (en la pestaña Microphone) para cargar el perfil seleccionado.
- Aparece una línea de resultado debajo de los botones después de un intento de creación, mostrando éxito o fallo. Desaparece cuando edita el campo de nombre del perfil.

### Pestaña Auto-Save

- Marque `Auto-save profile changes` para activar el guardado automático de cambios en perfiles de transmisión y micrófono.
- Cuando está activada, cualquier ajuste que realice a un perfil activo de transmisión o micrófono se guarda inmediatamente en ese perfil en la radio. No necesita guardar manualmente.
- La casilla lee su estado directamente del modelo de radio, no de AppSettings locales. Refleja el estado real de auto-guardado de la radio en todo momento.
- La casilla envía `profile autosave on/off` a la radio al alternarse.
- La casilla se mantiene sincronizada con el estado real de auto-guardado de la radio, incluso cuando el auto-guardado se activa o desactiva mediante:
  - El botón Habilitar Auto-Save en el diálogo de nombre duplicado de las pestañas Transmit o Microphone
  - Clientes TCI que envían comandos de auto-guardado
  - Carga de un perfil que tiene el auto-guardado activado o desactivado
  - Clientes remotos SmartSDR
- La casilla ignora su propia señal de alternancia al sincronizarse desde la radio, evitando bucles de retroalimentación.

## Consejos

- Al hacer clic en un perfil existente en la `Profile list`, se completa el campo `Profile name` con el nombre de ese perfil. Si luego hace clic en `Save` en la pestaña Global, el perfil existente se sobrescribe con el estado actual de la radio.
- También puede hacer doble clic en un perfil de la `Profile list` para cargarlo inmediatamente sin hacer clic en `Load`.
- La `Profile list` se actualiza automáticamente cuando la radio confirma el guardado. No necesita cerrar y volver a abrir el diálogo para ver la nueva entrada.
- Para perfiles de transmisión y micrófono, active Auto-Save antes de realizar ajustes para no perder los cambios.
- Los botones `Save` y `Create` están deshabilitados cuando el campo de nombre del perfil está vacío, evitando clics involuntarios que no tendrían efecto.

## Solución de problemas

- **Save no tiene efecto y el perfil no aparece en la lista** — Confirme que la radio está conectada. El Administrador de Perfiles requiere una conexión activa con la radio; si la conexión se perdió, reconéctese mediante `Settings > Connect to Radio...` e intente de nuevo.
- **Al hacer clic en Save con el campo `Profile name` vacío no sucede nada** — Escriba un nombre en `Profile name` o seleccione primero un perfil existente en la `Profile list` (su nombre llenará el campo automáticamente). El botón Save está deshabilitado cuando el campo está vacío.
- **No se puede sobrescribir un perfil de transmisión o micrófono** — Esto es por diseño. Use `Create` para crear un nuevo perfil, o active Auto-Save para que los cambios al perfil activo se guarden automáticamente.
- **La casilla Auto-Save parece cambiar sola** — Esto es normal. La casilla refleja el estado real de auto-guardado de la radio. Puede actualizarse cuando activa Auto-Save desde la pestaña Transmit o Microphone, o cuando otro cliente alterna el auto-guardado en la radio.
- **Una línea de resultado de guardado permanece visible después de un tiempo de espera** — Si la radio no responde a un comando de guardado en 15 segundos, la línea de resultado se borra automáticamente. Esto evita que un estado obsoleto persista después de una desconexión de la radio.

## Relacionado

- [Descripción general del Administrador de Perfiles](overview.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el auto-guardado para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
