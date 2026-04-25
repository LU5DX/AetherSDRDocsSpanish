# Cambiar a un perfil de transmisión guardado

Cargue un perfil de transmisión previamente guardado en el radio para restaurar un conjunto específico de ajustes de TX en un solo paso.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Debe existir al menos un perfil de transmisión en el radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Transmit (tab)**.
3. En la lista **Profile list**, haga clic en el perfil que desea cargar para seleccionarlo.
4. Haga clic en **Load**.

De manera alternativa, haga doble clic en el nombre del perfil en la lista **Profile list** para cargarlo sin necesidad de hacer clic en **Load**.

El perfil activo queda resaltado en la lista **Profile list** después de la carga.

## Qué hace cada control

| Control | Descripción | Clave de ajuste |
|---|---|---|
| **Transmit (tab)** | Muestra los perfiles de transmisión almacenados en el radio. | — |
| **Profile list** | Todos los perfiles de transmisión guardados; el perfil activo aparece resaltado. | — |
| **Profile name** | Campo de texto que se completa con el nombre del perfil seleccionado al hacer clic en una entrada. También se utiliza al guardar un nuevo perfil. | — |
| **Load** | Envía el perfil seleccionado al radio. Se activa únicamente cuando hay un perfil seleccionado. | — |
| **Save** | Guarda el estado TX actual del radio con el nombre indicado en **Profile name**. | — |
| **Delete** | Elimina el perfil seleccionado tras una confirmación. | — |
| **Auto-save profile changes** | Cuando está marcado, los cambios de TX se escriben automáticamente en el perfil activo. | `AutoSaveTransmitProfile` |

## Sugerencias

- Al seleccionar un perfil en la lista **Profile list**, el campo **Profile name** se completa con el nombre de ese perfil. Si luego hace clic en **Save**, el radio sobreescribirá ese perfil con el estado TX actual.
- Para evitar que los cambios de TX sobreescriban el perfil que acaba de cargar, deje la opción **Auto-save profile changes** sin marcar en la pestaña **Auto-Save (tab)**.

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Activar el guardado automático para que los ajustes de TX siempre se conserven](turn-on-auto-save-so-tx-tweaks-always-persist.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
