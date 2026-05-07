# Novedades — Resumen de AetherSDR

El diálogo de Novedades muestra las notas de la versión de AetherSDR que aún no ha visto. Aparece automáticamente tras una actualización y también está disponible a demanda desde el menú Help.

## Cómo funciona

Cuando AetherSDR se inicia, compara la versión actual con el valor almacenado en `LastSeenVersion`. Si la versión actual es más reciente, el diálogo se abre automáticamente y muestra las notas de la versión para cada versión entre la última vista y la actual, limitado a las cinco versiones más recientes. En una primera instalación, donde `LastSeenVersion` no tiene un valor almacenado, el diálogo muestra solo las notas de la versión actual y lo saluda con un encabezado de bienvenida en lugar de un encabezado de cambio de versión.

Cuando abre el diálogo mediante `Help > What's New...`, se muestran todas las entradas de la versión actual, independientemente de lo que contenga `LastSeenVersion`.

Las entradas de las versiones se muestran como HTML con estilo en un navegador desplazable. Cada entrada puede incluir un número de versión, una fecha de publicación, un título breve y una lista de cambios individuales. Los cambios están codificados por colores según la categoría:

| Categoría | Color del indicador |
|---|---|
| Funcionalidad | Azul |
| Corrección de error | Rojo-anaranjado |
| Mejora | Verde |
| Infraestructura | Gris |

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de la versión | Área de texto desplazable | Muestra notas de la versión con estilo HTML para versiones más recientes que `LastSeenVersion`, hasta cinco versiones. |
| `Got it — 73!` | Botón | Descarta el diálogo y marca la versión actual como vista actualizando `LastSeenVersion`. |
| `Upgrade` | Botón | Visible solo cuando hay una actualización disponible. Abre la página de descarga de versiones de AetherSDR y cierra el diálogo. |
| `Skip this version` | Botón | Visible solo cuando hay una actualización disponible. Escribe la versión actual en `LastSeenVersion` y cierra el diálogo, suprimiendo la solicitud de actualización para esta versión. |
| Sugerencia | Indicador de pie de página | Muestra una línea breve de orientación debajo del encabezado. |

Los botones `Upgrade` y `Skip this version` aparecen solo cuando AetherSDR ha detectado que hay una compilación más reciente disponible.

## Consejos

- Para volver a leer las notas de la versión en cualquier momento sin activar una solicitud de actualización, use `Help > What's New...`. Esta ruta siempre muestra las notas de la versión actual.
- El pie de página de sugerencias señala el botón de bombilla en la barra de título para enviar informes de errores o ideas de funcionalidades.

## Relacionados

- [Read what changed in the new version](read-what-changed-in-the-new-version.md)
- [Re-read release notes later via Help menu](re-read-release-notes-later-via-help-menu.md)
- [Open the upgrade flow for a newer build](open-the-upgrade-flow-for-a-newer-build.md)
- [Skip the current version's release notes](skip-the-current-version-s-release-notes.md)
