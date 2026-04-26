# Revisar la lista de perfiles globales activos

Abra el Profile Manager para ver todos los perfiles globales almacenados en la radio e identificar cuál está activo en este momento.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Profile Manager requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Global (tab)** si no está seleccionada todavía.
3. Lea la **Profile list**. Aquí aparecen todos los perfiles globales almacenados en la radio. El perfil activo en ese momento aparece resaltado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Global (tab)** | Pestaña | Muestra los perfiles globales. El perfil activo aparece resaltado en la **Profile list**. |
| **Profile list** | Lista | Muestra todos los perfiles globales de la radio. El perfil activo queda preseleccionado cuando se abre el diálogo. |
| **Profile name** | Campo de texto | Se completa automáticamente al seleccionar un perfil en la lista. Se usa al guardar. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Se activa únicamente cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre escrito en **Profile name**. |
| **Delete** | Botón | Elimina el perfil seleccionado tras pedir confirmación. Se activa únicamente cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el diálogo. |

## Sugerencias

- La **Profile list** se actualiza automáticamente si la radio notifica un cambio mientras el diálogo está abierto. No es necesario volver a abrir el diálogo para ver los nuevos perfiles.
- Al hacer clic en un perfil de la **Profile list**, el campo **Profile name** se completa con el nombre de ese perfil y se activan los botones **Load** y **Delete**.
- El perfil activo también puede cargarse directamente desde el menú `Profiles` sin abrir el Profile Manager. Por debajo del separador de ese menú, la radio muestra una lista marcable de perfiles globales; el que está activo en ese momento aparece marcado.

## Temas relacionados

- [Descripción general del Profile Manager](overview.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
