# Novedades — Resumen de AetherSDR

El cuadro de diálogo de Novedades muestra las notas de la versión de AetherSDR que usted aún no ha visto. Aparece automáticamente después de una actualización y también está disponible bajo demanda desde el menú Ayuda.

## Cómo funciona

Cuando AetherSDR se inicia, compara la versión actual con el valor almacenado en `LastSeenVersion`. Si la versión actual es más reciente, el cuadro de diálogo se abre automáticamente y obtiene las notas de la versión desde GitHub para cada versión entre la última versión vista y la actual, limitado a las cinco versiones más recientes. En una primera instalación, donde `LastSeenVersion` no tiene ningún valor almacenado, el cuadro de diálogo muestra solo las notas de la versión actual y lo saluda con un encabezado de bienvenida en lugar de un encabezado de cambio de versión.

Cuando abre el cuadro de diálogo mediante `Help > What's New...`, muestra todas las entradas de la versión actual independientemente de lo que contenga `LastSeenVersion`.

Las notas de la versión se obtienen desde la API de Releases de GitHub y se renderizan como HTML con estilo en un navegador desplazable. Las características de Markdown de GitHub, como referencias a incidencias (p. ej., `#1234`), menciones de usuarios (p. ej., `@username`) y enlaces relativos, se convierten automáticamente en enlaces en los que se puede hacer clic. El primer encabezado se elimina de cada nota de la versión si duplica el título de la versión o el nombre de la etiqueta.

Si la API de GitHub tiene límite de tasa (HTTP 403 con un mensaje de "límite de tasa"), el cuadro de diálogo muestra un mensaje amigable que sugiere esperar unos minutos o leer las notas de la versión directamente en github.com/aethersdr/AetherSDR/releases.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| Navegador de notas de la versión | Área de texto desplazable | Muestra notas de la versión en HTML con estilo para versiones más recientes que `LastSeenVersion`, hasta cinco versiones. El contenido se obtiene en vivo desde GitHub, no está incrustado en la aplicación. |
| `Got it — 73!` | Botón | Descarta el cuadro de diálogo y marca la versión actual como vista al actualizar `LastSeenVersion`. |
| `Upgrade` | Botón | Visible solo cuando hay una actualización disponible. Abre la página de descarga de versiones de AetherSDR en https://github.com/aethersdr/AetherSDR/releases/latest y cierra el cuadro de diálogo. |
| `Skip this version` | Botón | Visible solo cuando hay una actualización disponible. Escribe la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo, suprimiendo la solicitud de actualización para esta versión. |
| Sugerencia | Indicador de pie de página | Muestra una breve línea de orientación debajo del encabezado. |

Los botones `Upgrade` y `Skip this version` aparecen solo cuando AetherSDR ha detectado que hay una compilación más reciente disponible.

## Consejos

- Para volver a leer las notas de la versión en cualquier momento sin activar una solicitud de actualización, use `Help > What's New...`. Esta ruta siempre muestra las notas de la versión actual.
- El pie de página de Sugerencia señala el botón de bombilla en la barra de título para enviar informes de errores o sugerencias de funciones.
- Si las notas de la versión no se cargan debido a problemas de red o al límite de tasa de GitHub, siempre puede leerlas directamente en github.com/aethersdr/AetherSDR/releases.

## Relacionado

- [Lea lo que cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Vuelva a leer las notas de la versión más tarde mediante el menú Ayuda](re-read-release-notes-later-via-help-menu.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
