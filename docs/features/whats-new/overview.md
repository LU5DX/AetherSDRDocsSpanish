# Novedades — Descripción general de AetherSDR

El diálogo What's New muestra las notas de versión de AetherSDR que usted aún no ha visto. Aparece automáticamente después de una actualización y también está disponible bajo demanda desde el menú Help.

## Cómo funciona

Al iniciarse AetherSDR, el programa compara la versión actual con el valor almacenado en `LastSeenVersion`. Si la versión actual es más reciente, el diálogo se abre automáticamente y muestra las notas de versión de cada versión comprendida entre la última vista y la actual, con un límite de las cinco versiones más recientes. En una primera instalación, cuando `LastSeenVersion` no tiene ningún valor almacenado, el diálogo muestra únicamente las notas de la versión actual y lo saluda con un encabezado de bienvenida en lugar de un encabezado de cambio de versión.

Al abrir el diálogo mediante `Help > What's New...`, se muestran todas las entradas de la versión actual independientemente del contenido de `LastSeenVersion`.

Las entradas de versión se muestran como HTML con estilos en un navegador desplazable. Cada entrada puede incluir un número de versión, una fecha de lanzamiento, un titular breve y una lista de cambios individuales. Los cambios están codificados por color según su categoría:

| Categoría | Color indicador |
|---|---|
| Feature | Azul |
| Bug Fix | Rojo-anaranjado |
| Improvement | Verde |
| Infrastructure | Gris |

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de versión | Área de texto desplazable | Muestra las notas de versión en HTML con estilos para las versiones más recientes que `LastSeenVersion`, hasta cinco versiones. |
| `Got it — 73!` | Botón | Cierra el diálogo y marca la versión actual como vista actualizando `LastSeenVersion`. |
| `Upgrade` | Botón | Visible solo cuando hay una actualización disponible. Abre la página de descarga de versiones de AetherSDR y cierra el diálogo. |
| `Skip this version` | Botón | Visible solo cuando hay una actualización disponible. Escribe la versión actual en `LastSeenVersion` y cierra el diálogo, suprimiendo el aviso de actualización para esta versión. |
| Hint | Indicador de pie de página | Muestra una línea breve de orientación debajo del encabezado. |

Los botones `Upgrade` y `Skip this version` aparecen únicamente cuando AetherSDR ha detectado que hay una versión más reciente disponible.

## Consejos

- Para volver a leer las notas de versión en cualquier momento sin activar un aviso de actualización, use `Help > What's New...`. Esta ruta muestra siempre las notas de la versión actual.
- El pie de página Hint señala el botón de bombilla en la barra de título para enviar informes de errores o ideas de nuevas funciones.

## Relacionados

- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Volver a leer las notas de versión más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Abrir el flujo de actualización para una versión más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Omitir las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)
