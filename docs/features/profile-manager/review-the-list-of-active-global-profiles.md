# Revisar la lista de perfiles globales activos

El Profile Manager muestra todos los perfiles globales almacenados en el radio y resalta el que está en uso actualmente. Use esta función cuando desee confirmar qué perfiles existen o identificar el activo antes de cargarlo o eliminarlo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El Profile Manager requiere una conexión activa con el radio.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el diálogo Profile Manager.
2. Haga clic en la pestaña **Global (tab)** si no está seleccionada todavía.
3. Revise la **Profile list**. El perfil activo aparece resaltado.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Global (tab)** | Pestaña | Muestra la lista de perfiles globales del radio conectado. |
| **Profile list** | Lista | Muestra todos los perfiles globales almacenados en el radio. El perfil activo actualmente aparece resaltado. |
| **Profile name** | Campo de texto | Se rellena automáticamente al seleccionar un perfil de la lista. Se usa al guardar. |
| **Load** | Botón | Carga el perfil seleccionado en el radio. Se habilita únicamente cuando hay un perfil seleccionado. |
| **Save** | Botón | Guarda el estado actual del radio con el nombre indicado en **Profile name**. |
| **Delete** | Botón | Elimina el perfil seleccionado tras una confirmación. Se habilita únicamente cuando hay un perfil seleccionado. |
| **Close** | Botón | Cierra el diálogo. |

## Consejos

- La **Profile list** se actualiza automáticamente si el radio envía una nueva lista de perfiles mientras el diálogo está abierto. No es necesario cerrar y volver a abrir el diálogo para ver los cambios.
- El perfil activo aparece resaltado en la lista. Si ningún elemento aparece resaltado, no hay ningún perfil global cargado actualmente en el radio.
- El menú `Profiles` también muestra una lista dinámica con casillas de verificación de los perfiles globales debajo del separador. Puede identificar el perfil activo de un vistazo sin necesidad de abrir el Profile Manager.

## Temas relacionados

- [Descripción general del Profile Manager](overview.md)
- [Guardar el estado actual del radio como un nuevo perfil global](save-the-current-radio-state-as-a-new-global-profile.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
