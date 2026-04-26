# Guardar el estado actual de la radio como un nuevo perfil global

Use el Administrador de perfiles para capturar el estado actual de la radio y almacenarlo como un perfil global con nombre. Los perfiles globales registran la configuración general de la radio y pueden recuperarse en cualquier momento desde el menú Profiles.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El Administrador de perfiles requiere una conexión de radio activa.
- Decida el nombre del nuevo perfil antes de comenzar.

## Pasos

1. Haga clic en `Profiles > Profile Manager...` para abrir el cuadro de diálogo Profile Manager.
2. Haga clic en la pestaña **Global (tab)**.
3. En el campo **Profile name**, escriba el nombre del nuevo perfil.
4. Haga clic en **Save**.

La radio guarda el estado actual con el nombre que ingresó. El campo **Profile name** se vacía y la radio envía una lista actualizada a AetherSDR. El nuevo perfil aparece en **Profile list**.

## Qué hace cada control

| Control | Tipo | Comportamiento | Clave de configuración |
|---|---|---|---|
| **Global (tab)** | Pestaña | Cambia a la vista de perfiles globales. | — |
| **Profile name** | Campo de texto | Nombre que se usa al guardar un nuevo perfil. Si está vacío al hacer clic en Save, se usa el nombre del elemento seleccionado en Profile list. | — |
| **Profile list** | Lista | Muestra todos los perfiles globales almacenados en la radio. El perfil activo aparece resaltado. | — |
| **Load** | Botón | Carga el perfil seleccionado en la radio. Se habilita solo cuando hay un perfil seleccionado. | — |
| **Save** | Botón | Guarda el estado actual de la radio con el nombre escrito en Profile name. | — |
| **Delete** | Botón | Elimina el perfil seleccionado tras una confirmación. Se habilita solo cuando hay un perfil seleccionado. | — |
| **Close** | Botón | Cierra el cuadro de diálogo Profile Manager. | — |

## Sugerencias

- También puede cargar un perfil haciendo doble clic en su entrada dentro de **Profile list**, sin necesidad de hacer clic en **Load**.
- Si selecciona un perfil existente de **Profile list**, su nombre se copia automáticamente en el campo **Profile name**. Al hacer clic en **Save** en ese momento, se sobrescribe ese perfil con el estado actual de la radio.
- Los perfiles globales guardados aparecen en la lista dinámica bajo `Profiles` en la barra de menú y pueden cargarse con un solo clic desde allí.

## Temas relacionados

- [Descripción general del Administrador de perfiles](overview.md)
- [Revisar la lista de perfiles globales activos](review-the-list-of-active-global-profiles.md)
- [Cambiar a un perfil de transmisión guardado](switch-to-a-saved-transmit-profile.md)
- [Activar el guardado automático para que los ajustes de TX siempre persistan](turn-on-auto-save-so-tx-tweaks-always-persist.md)
