# Releer las notas de la versión posteriormente desde el menú Ayuda

El cuadro de diálogo Novedades — AetherSDR se abre automáticamente después de una actualización, pero puede reabrirlo en cualquier momento desde el menú Ayuda para revisar las notas de la versión actual.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión con la radio.

## Pasos

1. Haga clic en `Help > What's New...` en la barra de menú.
2. Desplácese por el navegador de notas de la versión para leer los cambios.
3. Haga clic en `Got it — 73!` para cerrar el cuadro de diálogo.

## Función de cada control

| Control                          | Tipo                                                                                                                | Comportamiento                                                                                                                                                               |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Indicador AETHERSDR V<version>   | indicador                                                                                                           | Encabezado con la marca que muestra la versión actual de AetherSDR y el título 'Bienvenido' o 'Novedades'. Se representa como HTML estilizado en un QLabel con relleno. |
| Etiqueta de estado               | indicador                                                                                                           | Debajo del encabezado muestra el título de la versión de GitHub y la fecha de publicación después de obtenerlos, o un mensaje de carga mientras se obtienen. Estado de varias líneas mediante inserción de <br/>. |
| Navegador de notas de la versión | QTextBrowser desplazable que muestra las notas de la versión como Markdown al estilo GitHub. Los números de incidencias/PR y las menciones @ tienen hipervínculos a GitHub. Al hacer clic en los enlaces se abre el navegador predeterminado. | Refactorizado en v26.5.3 (#2979) para obtener notas en vivo desde api.github.com. Muestra el estado 'Cargando...', estado de error con sugerencias, o el cuerpo de la versión procesado. |
| Buscar                           | botón                                                                                                               | Abre un QInputDialog para ingresar texto de búsqueda; resalta las coincidencias en las notas de la versión y se desplaza cíclicamente.                                         |
| Actualizar                       | Se muestra solo cuando showUpgrade es verdadero; abre la página de la última versión en GitHub y cierra el cuadro de diálogo.                                                    | Estilizado como botón secundario.                                                                                                                                             |
| Omitir esta versión              | Se muestra solo cuando showUpgrade es verdadero; guarda la versión actual como vista para que el cuadro de diálogo no se muestre en el próximo inicio.                            | Estilizado como botón secundario.                                                                                                                                             |
| Cerrar                           | botón                                                                                                               | Botón de acción principal que cierra el cuadro de diálogo. Estilizado como botón azul principal. Siempre visible.                                                              |
## Consejos

- Abrir el cuadro de diálogo mediante `Help > What's New...` siempre muestra las notas completas de la versión actual, independientemente del valor de `LastSeenVersion`. La versión automática al inicio muestra solo las entradas más recientes que la última versión vista, con un máximo de cinco versiones.
- El cuadro de diálogo obtiene las notas de la versión desde la API de GitHub. Si ve un error por límite de tasa, intente nuevamente en unos minutos, o visite `github.com/aethersdr/AetherSDR/releases` directamente en su navegador.
- El botón Actualizar usa la constante `kReleasesPageUrl` de UpdateChecker para abrir la página de versiones. Esto garantiza un uso coherente de la URL en toda la aplicación.

## Relacionados

- [Lea qué cambió en la nueva versión](read-what-changed-in-the-new-version.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
