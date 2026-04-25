# Revisar la lista de perfiles globales activos

El Administrador de perfiles muestra todos los perfiles globales almacenados en la radio y resalta el que está activo en ese momento. Úselo cuando desee confirmar qué perfil está cargado o encontrar el nombre de un perfil antes de cargarlo, guardarlo o eliminarlo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Global (tab)** si no está seleccionada.
3. Lea la **Profile list**. Aquí aparecen todos los perfiles globales almacenados en la radio. El perfil activo en ese momento está resaltado.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Global (tab)** | Pestaña | Muestra la gestión de perfiles globales. Contiene la lista de perfiles globales. |
| **Profile list** | Lista | Muestra todos los perfiles globales de la radio. El perfil activo está resaltado. Al seleccionar una entrada se habilitan Load y Delete, y se copia el nombre en el campo Profile name. |
| **Profile name** | Campo de texto | Muestra el nombre del perfil seleccionado. Se usa como nombre al guardar un perfil nuevo. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Deshabilitado hasta que se seleccione un perfil. |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre indicado en el campo Profile name. |
| **Delete** | Botón | Elimina el perfil seleccionado tras una confirmación. Deshabilitado hasta que se seleccione un perfil. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- La lista de perfiles se actualiza automáticamente si la radio informa un cambio mientras el diálogo está abierto. No es necesario cerrar y volver a abrir el diálogo para ver los perfiles añadidos o eliminados.
- Hacer doble clic en un perfil de la lista lo carga en la radio de inmediato, igual que seleccionarlo y hacer clic en Load.
- Para verificar qué perfil global está activo sin abrir el diálogo, haga clic en `Profiles` en la barra de menú. La radio muestra una lista de perfiles globales con casillas de verificación debajo del separador; el perfil activo aparece marcado.

## Relacionado

- [Descripción general del Administrador de perfiles](overview.md)
- [Guardar el estado actual de la radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
