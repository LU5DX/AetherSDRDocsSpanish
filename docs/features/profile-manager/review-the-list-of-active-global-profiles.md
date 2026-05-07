# Revisar la lista de perfiles globales activos

El Administrador de perfiles muestra todos los perfiles globales almacenados en la radio y resalta el que está actualmente en uso. Utilícelo cuando desee confirmar qué perfiles existen o identificar el perfil activo antes de cargarlo o eliminarlo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión activa con la radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo del Administrador de perfiles.
2. Haga clic en la pestaña **Global (tab)** si aún no está seleccionada.
3. Revise la **Profile list**. El perfil activo está resaltado.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Global (tab)** | Pestaña | Muestra la lista de perfiles globales de la radio conectada. |
| **Profile list** | Lista | Muestra todos los perfiles globales almacenados en la radio. El perfil actualmente activo está resaltado. |
| **Profile name** | Campo de texto | Se completa automáticamente al seleccionar un perfil de la lista. Se utiliza al guardar. |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Solo se habilita cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre indicado en **Profile name**. |
| **Delete** | Botón | Elimina el perfil seleccionado después de un mensaje de confirmación. Solo se habilita cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- La **Profile list** se actualiza automáticamente si la radio envía una nueva lista de perfiles mientras el diálogo está abierto. No es necesario cerrar y volver a abrir el diálogo para ver los cambios.
- El perfil activo se muestra resaltado en la lista. Si ningún elemento aparece resaltado, significa que no hay ningún perfil global cargado actualmente en la radio.
- El menú `Profiles` también muestra una lista dinámica seleccionable de perfiles globales debajo del separador. Puede ver el perfil activo de un vistazo allí sin necesidad de abrir el Administrador de perfiles.

## Relacionados

- [Profile Manager overview](overview.md)
- [Save the current radio state as a new global profile](save-the-current-radio-state-as-a-new-global-profile.md)
- [Switch to a saved transmit profile](switch-to-a-saved-transmit-profile.md)
