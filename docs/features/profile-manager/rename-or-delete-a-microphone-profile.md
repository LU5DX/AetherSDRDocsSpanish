# Cambiar el nombre o eliminar un perfil de micrófono

El Administrador de perfiles le permite cambiar el nombre de un perfil de micrófono guardando el estado actual del radio con un nombre nuevo y luego eliminando el anterior. Use esta página para depurar perfiles de micrófono obsoletos o asignarles nombres más descriptivos.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Administrador de perfiles requiere una conexión activa con el radio.
- Conozca el nombre del perfil que desea renombrar o eliminar. Abra la pestaña Microphone para revisar la lista si es necesario.

## Pasos

### Para cambiar el nombre de un perfil de micrófono

El radio no ofrece un comando de renombrado directo. Cambie el nombre guardando el perfil con un nombre nuevo y luego eliminando el anterior.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. En la lista **Profile list**, haga clic en el perfil que desea renombrar. Su nombre aparece en el campo **Profile name**.
4. Borre el campo **Profile name** y escriba el nuevo nombre.
5. Haga clic en **Save**. El radio guarda el estado actual del micrófono con el nuevo nombre y la lista **Profile list** se actualiza.
6. En la lista **Profile list**, haga clic en el nombre anterior del perfil.
7. Haga clic en **Delete**.
8. Cuando aparezca el mensaje "Delete profile "…"?", haga clic en **Yes**.
9. Haga clic en **Close**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. En la lista **Profile list**, haga clic en el perfil que desea eliminar.
4. Haga clic en **Delete**.
5. Cuando aparezca el mensaje "Delete profile "…"?", haga clic en **Yes**.
6. Haga clic en **Close**.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña **Microphone** | Pestaña | Muestra todos los perfiles de micrófono almacenados en el radio. |
| **Profile name** | Campo de texto | Contiene el nombre que se usará al hacer clic en Save. Se rellena automáticamente al seleccionar un perfil de la lista. |
| **Profile list** | Lista | Todos los perfiles de micrófono del radio; el perfil activo aparece resaltado. |
| **Load** | Botón | Carga el perfil seleccionado en el radio. Se habilita únicamente cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual del micrófono del radio con el nombre indicado en el campo **Profile name**. |
| **Delete** | Botón | Elimina el perfil seleccionado tras una confirmación. Se habilita únicamente cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

## Consejos

- Al seleccionar un perfil en la lista **Profile list**, el campo **Profile name** se rellena automáticamente con el nombre de ese perfil, lo que reduce la escritura al renombrar.
- Hacer doble clic en un perfil de la lista **Profile list** lo carga de inmediato, igual que hacer clic en **Load**.
- Si `AutoSaveTransmitProfile` está habilitado, los cambios en la configuración del micrófono se escriben automáticamente en el perfil activo. Verifique qué perfil está activo antes de eliminar alguno para evitar perder cambios recientes. Consulte [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md).

## Solución de problemas

- **Delete aparece desactivado** — No hay ningún perfil seleccionado en la lista **Profile list**. Haga clic en el nombre de un perfil para seleccionarlo y luego haga clic en **Delete**.
- **La lista Profile list no se actualiza tras Save o Delete** — El radio envía la lista actualizada mediante un mensaje de estado. Si la lista no se actualiza en pocos segundos, cierre y vuelva a abrir el Administrador de perfiles para forzar una recarga.

## Relacionados

- [Descripción general del Administrador de perfiles](overview.md)
- [Crear un perfil de micrófono independiente por cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
