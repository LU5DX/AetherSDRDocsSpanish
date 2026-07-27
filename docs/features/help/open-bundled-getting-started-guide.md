# Abrir la guía de inicio incluida

AetherSDR incluye un conjunto de temas de ayuda sin conexión que se abren sin necesidad de conexión a internet. Esta página explica cómo abrir la guía de inicio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a una radio.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Haga clic en `Getting Started...`.
3. Se abre el diálogo de ayuda, mostrando el tema de inicio en el visor Markdown.
4. Para buscar dentro del tema, escriba un término en el campo `Find:` y haga clic en `Next` para avanzar entre las coincidencias o `Previous` para retroceder. Presione Return para ir a la siguiente coincidencia. Presione Shift+Return para ir a la coincidencia anterior.
5. Para cerrar el diálogo, haga clic en `Close`.

## Función de cada control

| Control                            | Comportamiento                                                                                                                        | Notas                                                                                                                                                 |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `AETHERSDR OFFLINE HELP` (encabezado) | Encabezado de marca mostrado sobre el título del tema. Solo lectura.                                                                  |                                                                                                                                                       |
| Título                             | Muestra el nombre del tema pasado al diálogo al abrirlo. Solo lectura.                                                                |                                                                                                                                                       |
| Subtítulo                          | Descripción de una línea del tema. Solo lectura.                                                                                      |                                                                                                                                                       |
| Visor Markdown                     | Renderiza el contenido Markdown incluido para el tema seleccionado. Solo lectura; los enlaces externos se abren en su navegador.      |                                                                                                                                                       |
| Campo `Find:`                      | Escriba un asunto o término para buscar dentro del tema mostrado. Los botones `Next` y `Previous` están deshabilitados hasta que ingrese texto. | Ctrl+F enfoca el campo. Enter salta a la siguiente coincidencia; Shift+Enter salta a la anterior. QLineEdit con botón de borrar y marcador 'Subject or term'. |
| `Next`                             | Encuentra la siguiente ocurrencia del término de búsqueda. Vuelve al principio cuando se llega al final del documento.                | Deshabilitado cuando el campo de búsqueda está vacío.                                                                                                 |
| `Previous`                         | Encuentra la ocurrencia anterior del término de búsqueda. Vuelve al final cuando se llega al inicio del documento.                    | Deshabilitado cuando el campo de búsqueda está vacío.                                                                                                 |
| Estado de búsqueda                 | Muestra 'No matches' (rojo) o 'Wrapped to top/bottom' cuando no se encuentran más coincidencias en la dirección actual.              |                                                                                                                                                       |
| Pista / pie de página              | Muestra un consejo breve de uso. Solo lectura.                                                                                        |                                                                                                                                                       |
| `Close`                            | Cierra el diálogo de ayuda.                                                                                                           |                                                                                                                                                       |

## Consejos

- Cada entrada en el menú `Help` abre un diálogo separado para ese tema, por lo que puede mantener varios temas abiertos al mismo tiempo. Cada diálogo recuerda su propia posición y tamaño de forma independiente.
- El contenido de ayuda está incluido con la aplicación y no requiere conexión de red.
- Si no se puede cargar un archivo de ayuda, el visor muestra un aviso solicitándole que reinstale AetherSDR o que informe sobre el recurso faltante.
- El diálogo de ayuda ahora sigue el tema actual. Sus colores cambian automáticamente al cambiar de tema en `Settings > Appearance`.

## Relacionados

- [Lea el documento completo de ayuda de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conozca las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configure modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Comprenda cómo contribuir con informes de errores y PR](understand-how-to-contribute-bug-reports-and-prs.md)
