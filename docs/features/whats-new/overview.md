# Novedades — Introducción a AetherSDR

El diálogo de Novedades muestra las notas de versión de AetherSDR que aún no ha visto. Aparece automáticamente tras una actualización y también está disponible bajo demanda desde el menú Ayuda.

## Cómo funciona

Cuando AetherSDR se inicia, compara la versión actual con el valor almacenado en `LastSeenVersion`. Si la versión actual es más reciente, el diálogo se abre automáticamente y obtiene las notas de versión de GitHub para cada versión entre la última versión vista y la actual, limitado a las cinco versiones más recientes. En una primera instalación, donde `LastSeenVersion` no tiene un valor almacenado, el diálogo muestra solo las notas de la versión actual y lo saluda con un encabezado de bienvenida en lugar de un encabezado de cambio de versión.

Cuando abre el diálogo mediante `Help > What's New...`, muestra todas las entradas de la versión actual independientemente de lo que contenga `LastSeenVersion`.

Las notas de versión se obtienen de la API de Versiones de GitHub y se renderizan como HTML estilizado en un navegador desplazable. Las funciones de Markdown de GitHub, como referencias a incidencias (p. ej., `#1234`), menciones de usuarios (p. ej., `@username`) y enlaces relativos, se convierten automáticamente en enlaces en los que se puede hacer clic. Se elimina el primer encabezado de cada nota de versión si duplica el título o el nombre de la etiqueta de la versión.

Si la API de GitHub está limitada por tasa (HTTP 403 con un mensaje de "límite de tasa"), el diálogo muestra un mensaje amigable sugiriendo esperar unos minutos o leer las notas de versión directamente en github.com/aethersdr/AetherSDR/releases.

## Qué hace cada control

| Control                        | Tipo                                                                                                                                                                             | Comportamiento                                                                                                                                                |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AETHERSDR V<version> ceja | indicador                                                                                                                                                                        | Encabezado con marca que muestra la versión actual de AetherSDR y un título de '¡Bienvenido!' o 'Novedades'. Renderizado como HTML estilizado en un QLabel con relleno.         |
| Etiqueta de estado             | indicador                                                                                                                                                                        | Debajo del encabezado muestra el título de la versión de GitHub y la fecha de publicación después de la obtención, o un mensaje de carga mientras se obtiene. Estado multilínea mediante inserción de `<br/>`. |
| Navegador de notas de versión  | QTextBrowser desplazable que renderiza las notas de versión como Markdown al estilo GitHub. Los números de incidencia/PR y las @menciones tienen hipervínculos a GitHub. Al hacer clic en los enlaces se abre el navegador predeterminado. | Refactorizado en v26.5.3 (#2979) para obtener notas en vivo de api.github.com. Muestra estado 'Cargando...', estado de error con sugerencias, o el cuerpo de la versión renderizado.  |
| Buscar                         | push_button                                                                                                                                                                      | Abre un QInputDialog para ingresar texto de búsqueda; resalta las coincidencias en las notas de versión y envuelve alrededor. Nuevo en v26.5.3 (#2979).                                  |
| Actualizar                     | Se muestra solo cuando showUpgrade es verdadero; abre la página de la versión más reciente en GitHub y cierra el diálogo.                                                                              | Estilizado como botón secundario.                                                                                                                               |
| Saltar esta versión            | Se muestra solo cuando showUpgrade es verdadero; persiste la versión actual como vista para que el diálogo no se muestre en el próximo inicio.                                                                 | Estilizado como botón secundario.                                                                                                                               |
| Cerrar                         | push_button                                                                                                                                                                      | Botón de acción principal que descarta el diálogo. Estilizado como botón azul principal. Siempre visible.                                                               |

Los botones `Upgrade` y `Skip this version` aparecen solo cuando AetherSDR ha detectado que hay una compilación más reciente disponible.

## Consejos

- Para volver a leer las notas de versión en cualquier momento sin activar una solicitud de actualización, use `Help > What's New...`. Esta ruta siempre muestra las notas de la versión actual.
- El pie de página de Sugerencia señala el botón de bombilla en la barra de título para enviar informes de errores o ideas de funciones.
- Si las notas de versión no se cargan debido a problemas de red o limitación de tasa de GitHub, siempre puede leerlas directamente en github.com/aethersdr/AetherSDR/releases.

## Relacionados

- [Leer qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Volver a leer las notas de versión más tarde mediante el menú Ayuda](re-read-release-notes-later-via-help-menu.md)
- [Abrir el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
- [Saltar las notas de versión de la versión actual](skip-the-current-version-s-release-notes.md)
