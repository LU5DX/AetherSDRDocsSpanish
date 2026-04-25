# Abrir la guía de inicio incluida

AetherSDR incluye un conjunto de temas de ayuda sin conexión que se abren sin necesidad de acceso a internet. Esta página explica cómo abrir la guía de inicio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión a un radio.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Haga clic en `Getting Started...`.
3. Se abre el diálogo de ayuda y muestra el tema de inicio en el visor de Markdown.
4. Para buscar dentro del tema, escriba un término en el campo `Find:` y haga clic en `Next` para avanzar entre los resultados o en `Previous` para retroceder. Presione Return para ir al siguiente resultado. Presione Shift+Return para ir al resultado anterior.
5. Para cerrar el diálogo, haga clic en `Close`.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `AETHERSDR OFFLINE HELP` (encabezado superior) | Encabezado de marca que se muestra sobre el título del tema. Solo lectura. |
| Title | Muestra el nombre del tema que se pasó al diálogo al abrirse. Solo lectura. |
| Subtitle | Descripción breve del tema en una sola línea. Solo lectura. |
| Markdown viewer | Renderiza el contenido Markdown incluido para el tema seleccionado. Solo lectura; los enlaces externos se abren en su navegador. |
| Campo `Find:` | Escriba un asunto o término para buscar dentro del tema mostrado. Los botones `Next` y `Previous` están desactivados hasta que ingrese texto. |
| `Next` | Encuentra la siguiente ocurrencia del término de búsqueda. Vuelve al inicio cuando se alcanza el final del documento. |
| `Previous` | Encuentra la ocurrencia anterior del término de búsqueda. Vuelve al final cuando se alcanza el inicio del documento. |
| Hint / footer | Muestra un breve consejo de uso. Solo lectura. |
| `Close` | Cierra el diálogo de ayuda. |

## Consejos

- Cada entrada del menú `Help` abre un diálogo independiente para ese tema, por lo que puede mantener varios temas abiertos al mismo tiempo.
- El contenido de ayuda está incluido con la aplicación y no requiere conexión de red.
- Si un archivo de ayuda no puede cargarse, el visor muestra un aviso que le solicita reinstalar AetherSDR o reportar el recurso faltante.

## Relacionados

- [Leer el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conocer las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configurar modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Entender cómo contribuir con reportes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
