# Reabrir las Notas de la Versión Posteriormente a través del Menú Ayuda

El diálogo "Qué hay de nuevo — AetherSDR" se abre automáticamente después de una actualización, pero puede reabrirlo en cualquier momento desde el menú Ayuda para revisar las notas de la versión actual.

## Antes de empezar

- AetherSDR debe estar ejecutándose. No se requiere conexión de radio.

## Pasos

1. Haga clic en `Help > What's New...` en la barra de menú.
2. Desplácese por el navegador de notas de la versión para leer los cambios.
3. Haga clic en `Got it — 73!` para cerrar el diálogo.

## Función de cada control

| Control                         | Tipo       | Comportamiento                                                                                                                                                                                                                                                         |
|---------------------------------|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Panel AETHERSDR V<version>      | indicador  | Encabezado con marca que muestra la versión actual de AetherSDR y el título 'Welcome!' o 'What's New'. Representado como HTML estilizado en un QLabel con relleno.                                                                                                     |
| Etiqueta de estado              | indicador  | Debajo del encabezado, muestra el título de la versión de GitHub y la fecha de publicación después de la descarga, o un mensaje de carga mientras se descarga. Estado multilínea mediante inserción de <br/>.                                                          |
| Navegador de notas de la versión|campo_texto| QTextBrowser desplazable que muestra las notas de la versión en Markdown al estilo GitHub. Los números de Issue/PR y las menciones @ son hipervínculos a GitHub. Al hacer clic en los enlaces se abre el navegador predeterminado. Muestra estado de 'Loading...', estado de error con sugerencias, o el cuerpo de la versión renderizado. |
| Encontrar                       | botón      | Abre un QInputDialog para ingresar texto de búsqueda; resalta las coincidencias en las notas de la versión y envuelve alrededor.                                                                                                                                        |
| Actualizar                      | botón      | Se muestra solo cuando hay una actualización disponible. Abre la página de la última versión en GitHub y cierra el diálogo. Tiene estilo de botón secundario.                                                                                                            |
| Omitir esta versión             | botón      | Se muestra solo cuando hay una actualización disponible. Persiste la versión actual como vista para que el diálogo no se muestre en el próximo inicio. Tiene estilo de botón secundario.                                                                                 |
| Cerrar                          | botón      | Botón de acción principal que cierra el diálogo. Tiene estilo de botón azul principal. Siempre visible.                                                                                                                                                                |

## Consejos

- Al abrir el diálogo a través de `Help > What's New...`, siempre se muestran las notas completas de la versión actual, independientemente del valor de `LastSeenVersion`. La versión automática al inicio solo muestra las entradas más recientes que la última versión vista, con un máximo de cinco versiones.
- El diálogo obtiene las notas de la versión desde la API de GitHub. Si ve un error sobre límite de tasa, intente de nuevo en unos minutos, o visite directamente `github.com/aethersdr/AetherSDR/releases` en su navegador.
- El botón Actualizar utiliza la constante `kReleasesPageUrl` del UpdateChecker para abrir la página de versiones. Esto garantiza un uso coherente de la URL en toda la aplicación.

## Relacionado

- [Lea lo que cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
