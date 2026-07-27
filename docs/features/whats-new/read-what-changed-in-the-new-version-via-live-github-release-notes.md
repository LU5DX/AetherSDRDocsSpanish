# Lea qué cambió en la nueva versión mediante las notas de la versión en vivo desde GitHub

Consulte las notas de la versión de su AetherSDR actual, obtenidas en vivo desde GitHub. El diálogo también aparece automáticamente al iniciar por primera vez después de instalar una actualización.

## Antes de comenzar

- Se requiere una conexión a Internet activa para obtener las notas de la versión desde la API de GitHub.

## Pasos

1. Abra el diálogo **What's New**: `Help > What's New...`

   El diálogo muestra un encabezado con su versión actual de AetherSDR y ya sea "Welcome!" (primera instalación) o "What's New".

2. Las notas de la versión se cargan automáticamente desde GitHub. Una etiqueta de estado debajo del encabezado muestra el título de la versión y la fecha de publicación.

3. (Opcional) Haga clic en **Find** para buscar dentro de las notas de la versión. Ingrese su texto de búsqueda y presione Enter; las coincidencias se resaltan y se envuelven.

4. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Control                            | Valor predeterminado                                                                                                                                                                              | Comportamiento                                                                                                                                                                                                                                                                                                 |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Encabezado (AETHERSDR V&lt;versión&gt;) | —                                                                                                                                                                                                 | Muestra la versión actual y el encabezado "Welcome!" o "What's New"                                                                                                                                                                                                                                            |
| Etiqueta de estado                 | —                                                                                                                                                                                                 | Muestra el título de la versión de GitHub y la fecha de publicación, o un mensaje de carga/error                                                                                                                                                                                                               |
| Navegador de notas de la versión   | QTextBrowser desplazable que renderiza las notas de la versión como Markdown al estilo de GitHub. Los números de issue/PR y las @menciones tienen hipervínculos a GitHub. Al hacer clic en los enlaces se abre el navegador predeterminado. | Refactorizado en v26.5.3 (#2979) para obtener notas en vivo desde api.github.com. Muestra estado 'Loading...', estado de error con sugerencias, o el cuerpo de la versión renderizado.                                                                                                                        |
| Find                               | —                                                                                                                                                                                                 | Abre un diálogo de búsqueda; resalta el texto coincidente en las notas de la versión                                                                                                                                                                                                                          |
| Upgrade                            | Se muestra solo cuando showUpgrade es true; abre la página de la última versión en GitHub y cierra el diálogo.                                                                                    | Estilizado como botón secundario.                                                                                                                                                                                                                                                                              |
| Skip this version                  | Se muestra solo cuando showUpgrade es true; persiste la versión actual como vista para que el diálogo no se muestre en el próximo inicio.                                                         | Estilizado como botón secundario.                                                                                                                                                                                                                                                                              |
| Close                              | —                                                                                                                                                                                                 | Cierra el diálogo                                                                                                                                                                                                                                                                                              |
| Línea de encabezado AETHERSDR V&lt;versión&gt; | Encabezado que muestra la versión actual de AetherSDR y ya sea el título 'Welcome!' o 'What's New'.                                                                                              | Renderizado como HTML estilizado en un QLabel con relleno.                                                                                                                                                                                                                                                    |

## Solución de problemas

- **"GitHub está limitando la tasa de solicitudes desde su red"** — La API no autenticada de GitHub está limitada a 60 solicitudes por hora por IP. Espere unos minutos e intente nuevamente, o visite github.com/aethersdr/AetherSDR/releases directamente.
- **"GitHub devolvió HTTP ..."** — La solicitud a la API falló. Verifique su conexión a Internet e intente nuevamente más tarde.

## Relacionado

- [Vuelva a leer las notas de la versión más tarde mediante el menú Help](re-read-release-notes-later-via-help-menu.md)
- [Busque dentro de las notas de la versión usando el botón Find](search-within-the-release-notes-using-the-find-button.md)
- [Omita las notas de la versión actual](skip-the-current-version-s-release-notes.md)
- [Abra el flujo de actualización para una compilación más reciente](open-the-upgrade-flow-for-a-newer-build.md)
