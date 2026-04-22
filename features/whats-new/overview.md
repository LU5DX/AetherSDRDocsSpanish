# Novedades — Descripción general de AetherSDR

El diálogo Novedades muestra las notas de versión correspondientes a las versiones que aún no ha visto. Aparece automáticamente tras una actualización y también está disponible bajo demanda desde el menú Help.

## Cómo funciona

Al iniciar AetherSDR, el programa compara la versión actual con la versión almacenada en `LastSeenVersion`. Si la versión actual es más reciente, el diálogo se abre automáticamente y muestra las notas de versión de cada versión comprendida entre la última vista y la actual, con un máximo de cinco versiones. En una primera instalación, cuando no se ha registrado ningún valor en `LastSeenVersion`, el diálogo muestra únicamente las notas de la versión actual con un encabezado de bienvenida en lugar del encabezado estándar "What's New".

Al abrir el diálogo manualmente mediante `Help > What's New...`, se muestran todas las entradas de la versión actual independientemente del valor de `LastSeenVersion`.

Las entradas de versión se presentan como HTML con estilos en un navegador desplazable. Cada entrada puede incluir un número de versión, una fecha de lanzamiento, un titular breve y una lista de cambios individuales. Los cambios se identifican con colores según su categoría:

| Categoría | Color indicador |
|---|---|
| Feature | Azul |
| Bug Fix | Rojo-naranja |
| Improvement | Verde |
| Infrastructure | Gris |

Al cerrar el diálogo con "Got it — 73!" se registra la versión actual en `LastSeenVersion`, de modo que el diálogo no vuelva a aparecer para esa versión.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de versión | Vista HTML desplazable | Muestra las notas de versión filtradas. Solo lectura; los enlaces externos no se abren dentro del diálogo. |
| `Got it — 73!` | Botón | Cierra el diálogo y marca la versión actual como vista actualizando `LastSeenVersion`. |
| `Upgrade` | Botón | Visible únicamente cuando hay una versión más reciente disponible. Abre la página de versiones de AetherSDR en el navegador predeterminado y cierra el diálogo. |
| `Skip this version` | Botón | Visible únicamente cuando hay una versión más reciente disponible. Escribe la versión actual en `LastSeenVersion` y cierra el diálogo sin actualizar, suprimiendo el aviso de actualización para esta versión. |
| Hint | Indicador en el pie | Muestra una línea de orientación breve que dirige al botón de bombilla en la barra de título para reportar errores y enviar ideas. |

## Consejos

- Para volver a leer las notas de versión después de cerrar el diálogo, use `Help > What's New...` en cualquier momento. Esto abre el diálogo en modo de visualización completa y no modifica `LastSeenVersion`.
- Si hace clic en `Skip this version`, el aviso de actualización no volverá a aparecer para esa versión, pero puede abrir el diálogo manualmente en cualquier momento mediante `Help > What's New...`.

## Relacionados

- [Leer los cambios introducidos en la nueva versión](read-what-changed-in-the-new-version.md)
- [Volver a leer las notas de versión más adelante desde el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Abrir el proceso de actualización para una versión más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Omitir las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)
