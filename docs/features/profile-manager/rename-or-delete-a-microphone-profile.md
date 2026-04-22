# Renombrar o eliminar un perfil de micrófono

El Profile Manager permite renombrar un perfil de micrófono guardando el estado actual del radio con un nombre nuevo, y eliminar los perfiles que ya no necesite. Úselo para mantener ordenada su lista de perfiles de micrófono cuando cambie la configuración del micrófono.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Tenga a mano el nombre del perfil que desea renombrar o eliminar.

## Pasos

### Para renombrar un perfil de micrófono

El radio no ofrece un comando directo de renombrado. Renombre guardando con un nombre nuevo y luego eliminando el anterior.

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. En la lista **Profile list**, haga clic en el perfil que desea renombrar. Su nombre aparecerá en el campo **Profile name**.
4. Borre el campo **Profile name** y escriba el nombre nuevo.
5. Haga clic en **Save**. El radio guarda el estado actual del micrófono con el nombre nuevo y la lista **Profile list** se actualiza.
6. En la lista **Profile list**, haga clic en el nombre anterior del perfil.
7. Haga clic en **Delete**. Aparece un cuadro de confirmación con el mensaje `Delete profile "<name>"?`.
8. Haga clic en **Yes**. El perfil se elimina de la lista **Profile list**.

### Para eliminar un perfil de micrófono

1. Haga clic en `Profiles > Profile Manager...`.
2. Haga clic en la pestaña **Microphone**.
3. En la lista **Profile list**, haga clic en el perfil que desea eliminar.
4. Haga clic en **Delete**. Aparece un cuadro de confirmación con el mensaje `Delete profile "<name>"?`.
5. Haga clic en **Yes**. El perfil se elimina de la lista **Profile list**.
6. Haga clic en **Close** cuando haya terminado.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Pestaña **Microphone** | Pestaña | Cambia el cuadro de diálogo para mostrar los perfiles de micrófono. |
| **Profile name** | Campo de texto | Contiene el nombre que se usará al hacer clic en Save. Se rellena automáticamente al seleccionar un perfil de la lista. |
| **Profile list** | Lista | Muestra todos los perfiles de micrófono del radio. El perfil activo aparece resaltado. |
| **Load** | Botón | Carga el perfil seleccionado en el radio. Solo se activa cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual del micrófono del radio con el nombre indicado en **Profile name**. |
| **Delete** | Botón | Elimina el perfil seleccionado tras la confirmación. Solo se activa cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el cuadro de diálogo. |

## Consejos

- Al seleccionar un perfil en la lista **Profile list**, su nombre se copia automáticamente en el campo **Profile name**, por lo que solo necesita editar la parte del nombre que desea cambiar antes de hacer clic en **Save**.
- Load y Delete permanecen desactivados hasta que seleccione un perfil de la lista **Profile list**. Si ambos botones aparecen en gris, haga clic primero en un nombre de perfil de la lista.
- La lista **Profile list** se actualiza automáticamente cuando el radio confirma un cambio. No es necesario volver a abrir el cuadro de diálogo.

## Solución de problemas

- **Delete aparece en gris** — No hay ningún perfil seleccionado. Haga clic en un nombre de la lista **Profile list** para seleccionarlo y, a continuación, haga clic en **Delete**.
- **Save crea un duplicado en lugar de renombrar** — Esto es el comportamiento esperado. Save crea primero el nombre nuevo; luego seleccione y elimine el perfil anterior siguiendo los pasos de renombrado descritos anteriormente.
- **La lista Profile list no se actualiza después de Save o Delete** — La lista se refresca cuando el radio envía una confirmación. Si no se actualiza, compruebe la conexión con el radio e intente volver a abrir el cuadro de diálogo mediante `Profiles > Profile Manager...`.

## Temas relacionados

- [Descripción general del Profile Manager](overview.md)
- [Crear un perfil de micrófono independiente por cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
