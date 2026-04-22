# Guardar el estado actual del radio como un nuevo perfil global

Use esta página para capturar el estado actual del radio en un perfil global con nombre, de modo que pueda recuperarlo más adelante. Los perfiles globales almacenan configuraciones como el modo, la frecuencia y la configuración de banda en todo el radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.
- Decida un nombre para el nuevo perfil antes de comenzar.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Global**.
3. En el campo **Profile name**, escriba el nombre del nuevo perfil.
4. Haga clic en **Save**.

El radio guarda su estado actual con el nombre que escribió. La lista **Profile list** se actualiza automáticamente cuando el radio confirma el guardado.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Global (tab)** | Pestaña | Cambia a la gestión de perfiles globales. | — |
| **Profile name** | Campo de texto | Nombre utilizado al guardar un nuevo perfil. Si el campo está vacío al hacer clic en Save, se usa en su lugar el nombre del elemento seleccionado en la lista. | — |
| **Profile list** | Lista | Muestra todos los perfiles globales guardados. El perfil activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en el radio. Se habilita únicamente cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual del radio con el nombre indicado en **Profile name**. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras una confirmación. Se habilita únicamente cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el diálogo Profile Manager. | — |

## Consejos

- También puede cargar un perfil haciendo doble clic en su entrada en la lista **Profile list**; no es necesario hacer clic en **Load** por separado.
- Al seleccionar un perfil existente en la lista **Profile list**, su nombre se copia automáticamente en el campo **Profile name**. Escriba un nombre diferente antes de hacer clic en **Save** si desea crear un nuevo perfil en lugar de sobrescribir el existente.
- Para que los cambios en la configuración de transmisión y micrófono se guarden automáticamente en el perfil activo, habilite **Auto-save profile changes** en la pestaña **Auto-Save**. Esta configuración se almacena como `AutoSaveTransmitProfile`.

## Relacionado

- [Descripción general del Profile Manager](overview.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
