# Descripción general del Administrador de perfiles

El Administrador de perfiles le permite crear, cargar y eliminar perfiles Global, Transmit y Microphone almacenados en el radio. Úselo para guardar y recuperar estados completos del radio sin reconfigurar los ajustes manualmente.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El Administrador de perfiles requiere una conexión de radio activa.

## Cómo funciona

Abra el Administrador de perfiles desde `Profiles > Profile Manager...`. El cuadro de diálogo contiene cuatro pestañas — **Global**, **Transmit**, **Microphone** y **Auto-Save** — cada una opera de forma independiente sobre su categoría de perfiles correspondiente.

En las pestañas **Global**, **Transmit** y **Microphone**, el flujo de trabajo es el mismo:

1. La **Profile list** muestra todos los perfiles almacenados en el radio para esa categoría. El perfil activo actualmente aparece resaltado.
2. Al seleccionar una entrada en la **Profile list**, el campo **Profile name** se rellena con el nombre de esa entrada y se habilitan los botones **Load** y **Delete**.
3. Escriba un nombre nuevo en **Profile name** y haga clic en **Save** para guardar el estado actual del radio con ese nombre. Si el campo está vacío al hacer clic en **Save**, el cuadro de diálogo utiliza el nombre del elemento seleccionado en la lista.
4. Seleccione un perfil y haga clic en **Load** (o haga doble clic en la entrada) para aplicarlo al radio de inmediato.
5. Seleccione un perfil y haga clic en **Delete** para eliminarlo. Aparece una solicitud de confirmación antes de que el perfil sea eliminado.

La pestaña **Auto-Save** contiene una única casilla de verificación que controla el guardado automático de los cambios de transmisión.

Haga clic en **Close** para cerrar el cuadro de diálogo.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de ajuste |
|---|---|---|---|
| **Global** | Pestaña | Administra perfiles globales. | — |
| **Transmit** | Pestaña | Administra perfiles de transmisión. | — |
| **Microphone** | Pestaña | Administra perfiles de micrófono. | — |
| **Auto-Save** | Pestaña | Controla el guardado automático de perfiles. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un nuevo perfil. Si está vacío al momento de guardar, se usa el nombre del elemento seleccionado en la lista. | — |
| **Profile list** | Lista | Todos los perfiles de la categoría activa; el perfil activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en el radio. Se habilita solo cuando hay un perfil seleccionado. También se activa al hacer doble clic en una entrada de la lista. | — |
| **Save** | Botón | Guarda el estado actual del radio con el nombre indicado en **Profile name**. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras la confirmación. Se habilita solo cuando hay un perfil seleccionado. | — |
| **Auto-save profile changes** | Casilla de verificación | Cuando está marcada, los cambios en los ajustes de TX y micrófono se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |
| **Close** | Botón | Cierra el cuadro de diálogo. | — |

## Sugerencias

- La **Profile list** se actualiza automáticamente cuando el radio notifica un cambio, por lo que los perfiles guardados o eliminados desde otro lugar (por ejemplo, desde SmartSDR en otro cliente) aparecen sin necesidad de volver a abrir el cuadro de diálogo.
- Los botones Load y Delete permanecen deshabilitados hasta que seleccione un perfil de la lista. Si los botones aparecen en gris, primero haga clic en el nombre de un perfil.

## Relacionado

- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Renombrar o eliminar un perfil de micrófono](rename-or-delete-a-microphone-profile.md)
- [Crear un perfil de micrófono separado por cada micrófono](create-a-separate-mic-profile-per-microphone.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
