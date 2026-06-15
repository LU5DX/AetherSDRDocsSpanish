# Lea qué cambió en la nueva versión

El diálogo de Novedades muestra las notas de publicación de las versiones que aún no ha visto. Aparece automáticamente después de una actualización y también está disponible a demanda desde el menú Ayuda. Las notas de publicación se obtienen en vivo desde GitHub, por lo que el diálogo requiere conexión a internet para mostrarlas.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución. No se requiere conexión con la radio.
- Se necesita una conexión activa a internet para obtener las notas de publicación desde GitHub.

## Pasos

1. Haga clic en `Help > What's New...`.
2. Lea las notas de publicación en el **Navegador de notas de publicación** con desplazamiento.
3. Haga clic en `Got it — 73!` para cerrar el diálogo. AetherSDR registra la versión actual en `LastSeenVersion` para que el diálogo no vuelva a aparecer para esta versión.

## Qué hace cada control

| Control                      | Comportamiento                                                                                                                                                                    | Notas                                                                                                                                                          |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Navegador de notas de publicación | QTextBrowser con desplazamiento que renderiza las notas de publicación como Markdown al estilo GitHub. Los números de incidencias/PR y las menciones @ son hipervínculos a GitHub. Al hacer clic en los enlaces se abre el navegador predeterminado. | Refactorizado en v26.5.3 (#2979) para obtener notas en vivo desde api.github.com. Muestra estado 'Cargando...', estado de error con sugerencias, o el cuerpo de publicación renderizado. |
| `Got it — 73!`               | Cierra el diálogo y marca la versión actual como vista en `LastSeenVersion`.                                                                                                    |                                                                                                                                                                |
| `Upgrade`                    | Visible solo cuando hay una compilación más nueva disponible. Abre la página de la última versión en GitHub en su navegador del sistema y cierra el diálogo.                      | Estilizado como botón secundario.                                                                                                                              |
| `Skip this version`          | Visible solo cuando hay una compilación más nueva disponible. Escribe la versión actual en `LastSeenVersion` y cierra el diálogo sin actualizar.                                | Estilizado como botón secundario.                                                                                                                              |
| Encabezado AETHERSDR V<version> | Encabezado con marca que muestra la versión actual de AetherSDR y el título 'Welcome!' o 'What's New'.                                                                          | Renderizado como HTML estilizado en un QLabel con relleno.                                                                                                     |
| Etiqueta de estado           | Bajo el encabezado muestra el título de la publicación de GitHub y la fecha de publicación después de la obtención, o un mensaje de carga mientras se obtienen los datos.        | Estado multilínea mediante inserción de <br/>.                                                                                                                 |
| Buscar                       | Abre un QInputDialog para ingresar texto de búsqueda; resalta las coincidencias en las notas de publicación y envuelve la búsqueda.                                              | Nuevo en v26.5.3 (#2979).                                                                                                                                      |
| Cerrar                       | Botón de acción principal que cierra el diálogo.                                                                                                                                 | Estilizado como botón primario azul. Siempre visible.                                                                                                          |

## Consejos

- En la primera instalación, el diálogo muestra solo las notas de la versión actual. En actualizaciones posteriores muestra cada versión publicada desde la última versión vista.
- Las notas de publicación se muestran como HTML estilizado con colores de soporte para encabezados, bloques de código, citas en bloque y enlaces.
- Las referencias a incidencias de GitHub (ej., `#42`) se convierten automáticamente en hipervínculos a la incidencia correspondiente en GitHub.
- Los nombres de usuario de GitHub (ej., `@username`) se convierten automáticamente en hipervínculos al perfil de usuario correspondiente.
- Si el diálogo no puede acceder a la API de GitHub, muestra un mensaje de error. Una causa común es el límite de velocidad no autenticado de GitHub (60 solicitudes por hora por dirección IP). En ese caso, puede leer las notas de publicación directamente en `github.com/aethersdr/AetherSDR/releases`.
- Para volver a leer las notas en cualquier momento, use `Help > What's New...`. Esta ruta siempre muestra las notas completas de la versión actual independientemente de `LastSeenVersion`.

## Relacionados

- [Vuelva a leer las notas de publicación más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Omita las notas de publicación de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abra el flujo de actualización para una compilación más nueva](open-the-upgrade-flow-for-a-newer-build.md)
