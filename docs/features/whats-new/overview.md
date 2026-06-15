# Novedades — Resumen de AetherSDR

El cuadro de diálogo Novedades muestra las notas de la versión de AetherSDR que aún no ha visto. Aparece automáticamente después de una actualización y también está disponible a demanda desde el menú Help.

## Cómo funciona

Cuando AetherSDR se inicia, compara la versión actual con el valor almacenado en `LastSeenVersion`. Si la versión actual es más nueva, el cuadro de diálogo se abre automáticamente y obtiene las notas de la versión desde GitHub para cada versión entre la última versión vista y la actual, limitándose a las cinco versiones más recientes. En una primera instalación, donde `LastSeenVersion` no tiene ningún valor almacenado, el cuadro de diálogo muestra solo las notas de la versión actual y le saluda con un encabezado de bienvenida en lugar de un encabezado de cambio de versión.

Cuando abre el cuadro de diálogo mediante `Help > What's New...`, muestra todas las entradas de la versión actual independientemente de lo que contenga `LastSeenVersion`.

Las notas de la versión se obtienen de la API de Releases de GitHub y se renderizan como HTML con estilo en un navegador desplazable. Las funciones de Markdown de GitHub, como referencias a incidencias (ej. `#1234`), menciones de usuarios (ej. `@username`) y enlaces relativos, se convierten automáticamente en enlaces en los que se puede hacer clic. Se elimina el primer encabezado de cada nota de la versión si duplica el título de la versión o el nombre de la etiqueta.

Si la API de GitHub está limitada por tasa (HTTP 403 con un mensaje de "límite de tasa"), el cuadro de diálogo muestra un mensaje amigable sugiriendo que espere unos minutos o que lea las notas de la versión directamente en github.com/aethersdr/AetherSDR/releases.

## Qué hace cada control

| Control                   | Tipo                     | Comportamiento                                                                                                                                             |
|---------------------------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Título AETHERSDR V<versión> | indicador              | Encabezado con marca que muestra la versión actual de AetherSDR y el encabezado 'Welcome!' o 'What's New'. Se renderiza como HTML con estilo en un QLabel con relleno. |
| Etiqueta de estado        | indicador                | Debajo del encabezado muestra el título de la versión de GitHub y la fecha de publicación después de la obtención, o un mensaje de carga mientras se obtiene. Estado multilínea mediante inserción de `<br/>`.          |
| Navegador de notas de versión | campo_texto            | QTextBrowser desplazable que renderiza las notas de la versión como Markdown al estilo de GitHub. Los números de incidencias/PR y las @menciones tienen hipervínculos a GitHub. Al hacer clic en los enlaces se abre el navegador predeterminado. Muestra el estado 'Loading...', estado de error con sugerencias o el cuerpo de la versión renderizado. |
| Find                      | botón_de_empuje          | Abre un QInputDialog para introducir texto de búsqueda; resalta las coincidencias en las notas de la versión y se desplaza envolventemente. Nuevo en v26.5.3 (#2979).                                         |
| Upgrade                   | botón_de_empuje          | Visible solo cuando hay una actualización disponible. Abre la página de descarga de versiones de AetherSDR y cierra el cuadro de diálogo.                                                          |
| Skip this version         | botón_de_empuje          | Visible solo cuando hay una actualización disponible. Escribe la versión actual en `LastSeenVersion` y cierra el cuadro de diálogo, suprimiendo la solicitud de actualización para esta versión.     |
| Close                     | botón_de_empuje          | Botón de acción principal que descarta el cuadro de diálogo. Tiene estilo de botón azul primario. Siempre visible.                                                                        |

Los botones `Upgrade` y `Skip this version` aparecen solo cuando AetherSDR ha detectado que hay una versión más reciente disponible.

## Consejos

- Para volver a leer las notas de la versión en cualquier momento sin activar una solicitud de actualización, use `Help > What's New...`. Esta ruta siempre muestra las notas de la versión actual.
- El pie de página Hint señala el botón de bombilla en la barra de título para enviar informes de errores o ideas de funcionalidades.
- Si las notas de la versión no se cargan debido a problemas de red o limitación de tasa de GitHub, siempre puede leerlas directamente en github.com/aethersdr/AetherSDR/releases.

## Relacionado

- [Lea lo que cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Vuelva a leer las notas de la versión más tarde a través del menú Help](re-read-release-notes-later-via-help-menu.md)
- [Abra el flujo de actualización para una versión más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
