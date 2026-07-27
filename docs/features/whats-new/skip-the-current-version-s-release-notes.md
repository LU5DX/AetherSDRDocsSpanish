# Diálogo de Novedades

El diálogo de Novedades muestra las notas de la versión actual de AetherSDR. Aparece automáticamente después de un cambio de versión, o puede abrirlo manualmente mediante `Help > What's New...`. El diálogo obtiene las notas de la versión en vivo desde la API de GitHub y las renderiza como Markdown con estilo.

## Antes de comenzar

- Se requiere una conexión a Internet activa para obtener las notas de la versión en vivo desde GitHub.
- El diálogo aparece automáticamente cuando AetherSDR detecta que se ha instalado una nueva versión.
- Puede abrir el diálogo en cualquier momento desde el menú Help.

## Pasos

1. Si el diálogo no se abre automáticamente, vaya a `Help > What's New...`.
2. Espere a que se carguen las notas de la versión. La etiqueta de estado muestra "Loading..." mientras se obtienen los datos.
3. Lea las notas de la versión en el área de navegador. Haga clic en cualquier número de incidencia/PR o @menciones con hipervínculo para abrirlos en su navegador predeterminado.
4. Para buscar dentro de las notas de la versión, haga clic en "Find", ingrese su texto de búsqueda y presione Enter. Las coincidencias se resaltan y la vista se desplaza en bucle.
5. Cuando termine, haga clic en "Close" para cerrar el diálogo.

## Función de cada control

| Control                          | Tipo                                                                                                                                                                                                | Comportamiento                                                                                                                                                                                              |
|----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Encabezado AETHERSDR V<version>  | Indicador                                                                                                                                                                                           | Encabezado con marca que muestra la versión actual de AetherSDR y el título 'Welcome!' o 'What's New'. Renderizado como HTML con estilo en un QLabel con relleno.                                            |
| Etiqueta de estado               | Indicador                                                                                                                                                                                           | Debajo del encabezado muestra el título de la versión de GitHub y la fecha de publicación después de la obtención, o un mensaje de carga mientras se obtienen los datos. Estado multilínea mediante inserción `<br/>`. |
| Navegador de notas de versión    | QTextBrowser desplazable que renderiza las notas de la versión como Markdown al estilo de GitHub. Los números de incidencia/PR y @menciones tienen hipervínculos a GitHub. Al hacer clic en enlaces se abre el navegador predeterminado. | Refactorizado en v26.5.3 (#2979) para obtener notas en vivo desde api.github.com. Muestra estado 'Loading...', estado de error con sugerencias, o el cuerpo de la versión renderizado.                          |
| Find                             | Botón pulsador                                                                                                                                                                                      | Abre un QInputDialog para ingresar texto de búsqueda; resalta las coincidencias en las notas de la versión y se desplaza en bucle. Nuevo en v26.5.3 (#2979).                                                   |
| Upgrade                          | Se muestra solo cuando showUpgrade es verdadero; abre la página de la última versión en GitHub y cierra el diálogo.                                                                                | Estilizado como botón secundario.                                                                                                                                                                           |
| Skip this version                | Se muestra solo cuando showUpgrade es verdadero; persiste la versión actual como vista para que el diálogo no se muestre en el próximo inicio.                                                     | Estilizado como botón secundario.                                                                                                                                                                           |
| Close                            | Botón pulsador                                                                                                                                                                                      | Acción principal que cierra el diálogo. Siempre visible. Estilizado como botón primario azul.                                                                                                                |

## Consejos

- Los botones "Skip this version" y "Upgrade" aparecen solo cuando hay una actualización disponible. Si no se detecta ninguna actualización, solo se muestra "Close".
- "Skip this version" escribe la versión actual en `LastSeenVersion` y cierra el diálogo. El diálogo de Novedades no aparecerá automáticamente en el próximo inicio para esta versión.
- "Upgrade" abre la página de versiones en GitHub usando la URL de versiones configurada de la aplicación. Al hacer clic también cierra el diálogo.
- Para volver a leer las notas de la versión en cualquier momento, use `Help > What's New...`. Esto abre el diálogo independientemente del valor guardado de `LastSeenVersion`.
- Las notas de la versión se obtienen de `api.github.com`. Si su red tiene limitación de velocidad por parte de GitHub (HTTP 403 con un mensaje de "rate limit"), el diálogo muestra un mensaje amigable sugiriendo que lo intente más tarde o lea las notas directamente en la página de versiones.
- El navegador de notas de la versión renderiza Markdown del cuerpo de la versión de GitHub. Las referencias a incidencias de GitHub (por ejemplo, `#123`) y las menciones `@username` se convierten automáticamente en enlaces cliqueables.

## Solución de problemas

- **"Skip this version" no es visible** — El botón solo aparece cuando AetherSDR ha detectado que hay una actualización disponible. Si no se detecta ninguna actualización, solo se muestra "Close". Esto es comportamiento esperado.
- **"Upgrade" no es visible** — Misma condición que arriba. El botón solo aparece cuando se detecta una actualización.
- **Las notas de la versión no se cargan** — El diálogo obtiene las notas de la versión desde `api.github.com`. Si ve un mensaje de error, puede deberse a problemas de red o limitación de velocidad de GitHub. Intente de nuevo más tarde o visite la página de versiones directamente.
- **El diálogo de búsqueda no encuentra coincidencias** — La búsqueda no distingue entre mayúsculas y minúsculas y busca en el texto renderizado de las notas de la versión. Asegúrese de que su término de búsqueda esté escrito correctamente.

## Relacionado

- [Re-read release notes later via Help menu](re-read-release-notes-later-via-help-menu.md)
- [Open the upgrade flow for a newer build](open-the-upgrade-flow-for-a-newer-build.md)
- [Read what changed in the new version](read-what-changed-in-the-new-version.md)
