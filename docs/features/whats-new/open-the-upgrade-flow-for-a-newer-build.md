# Abrir el flujo de actualización para una compilación más reciente

Cuando una compilación más reciente de AetherSDR está disponible, el diálogo "What's New" muestra un botón "Upgrade" que abre la página de descarga en su navegador. Esta página explica cómo llegar a ese botón.

## Antes de comenzar

- El botón "Upgrade" aparece solo cuando AetherSDR ha detectado que hay una compilación más reciente disponible. Si no hay ninguna actualización disponible, el botón no se muestra.
- No se requiere conexión con la radio.

## Pasos

1. Abra `Help > What's New...`.
2. Revise las notas de la versión en el navegador desplazable en la parte superior del diálogo.
3. Haga clic en `Upgrade`.

AetherSDR abre la página de versiones de AetherSDR en su navegador web predeterminado y cierra el diálogo. La URL de la página de descarga se obtiene de la referencia interna de la página de versiones de la aplicación.

## Función de cada control

| Control                      | Tipo                                                                                                                                                                             | Comportamiento                                                                                                                                                 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Navegador de notas de versión | QTextBrowser desplazable que renderiza las notas de la versión en Markdown estilo GitHub. Los números de incidencias/PR y las @menciones tienen hipervínculos a GitHub. Al hacer clic en los enlaces se abre el navegador predeterminado. | Refactorizado en v26.5.3 (#2979) para obtener notas en vivo desde api.github.com. Muestra el estado 'Cargando...', un estado de error con sugerencias, o el cuerpo de la versión renderizado. |
| `Got it — 73!`               | Botón pulsador                                                                                                                                                                   | Cierra el diálogo y marca la versión como vista.                                                                                                               |
| `Upgrade`                    | Botón pulsador                                                                                                                                                                   | Visible solo cuando hay una actualización disponible. Abre la página de descarga.                                                                              |
| `Skip this version`          | Botón pulsador                                                                                                                                                                   | Omite el aviso de versión para esta versión.                                                                                                                    |
| Título AETHERSDR V<version>  | Encabezado con la marca que muestra la versión actual de AetherSDR y el título 'Welcome!' o 'What's New'.                                                                       | Renderizado como HTML con estilo en un QLabel con relleno.                                                                                                      |
| Etiqueta de estado           | Debajo del encabezado, muestra el título de la versión de GitHub y la fecha de publicación después de la obtención, o un mensaje de carga mientras se obtiene.                    | Estado multilínea mediante inserción de <br/>.                                                                                                                  |
| Buscar                       | Abre un QInputDialog para ingresar texto de búsqueda; resalta las coincidencias en las notas de la versión y se desplaza circularmente.                                         | Nuevo en v26.5.3 (#2979).                                                                                                                                     |
| Cerrar                       | Botón de acción principal que cierra el diálogo.                                                                                                                                 | Con estilo de botón primario azul. Siempre visible.                                                                                                            |

## Consejos

- Si cierra el diálogo con `Got it — 73!` en lugar de `Upgrade`, AetherSDR registra la versión actual en `LastSeenVersion` y no le volverá a preguntar por esta versión. Aún puede volver al diálogo mediante `Help > What's New...`.
- Si hace clic en `Skip this version`, `LastSeenVersion` se establece en la versión actual y se suprime el aviso para esta versión, pero no se abre la página de descarga.

## Relacionado

- [Volver a leer las notas de la versión más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Leer lo que cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omitir las notas de la versión actual](skip-the-current-version-s-release-notes.md)
