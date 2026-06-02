# Guía de inicio incluida abierta

AetherSDR incluye un conjunto de temas de ayuda sin conexión que se abren sin necesidad de conexión a internet. Esta página explica cómo abrir la guía de inicio.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión de radio.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Haga clic en `Getting Started...`.
3. Se abre el diálogo de ayuda, mostrando el tema de inicio en el visor de Markdown.
4. Para buscar dentro del tema, escriba un término en el campo `Find:` y haga clic en `Next` para avanzar entre coincidencias o en `Previous` para retroceder. Presione Return para avanzar a la siguiente coincidencia. Presione Shift+Return para ir a la coincidencia anterior.
5. Para cerrar el diálogo, haga clic en `Close`.

## Función de cada control

| Control | Comportamiento |
|---|---|
| `AETHERSDR OFFLINE HELP` (encabezado) | Encabezado de marca que se muestra sobre el título del tema. Solo lectura. |
| Título | Muestra el nombre del tema pasado al diálogo al abrirlo. Solo lectura. |
| Subtítulo | Descripción de una línea del tema. Solo lectura. |
| Visor de Markdown | Renderiza el contenido Markdown incluido para el tema seleccionado. Solo lectura; los enlaces externos se abren en su navegador. |
| Campo `Find:` | Escriba un asunto o término para buscar dentro del tema mostrado. Los botones `Next` y `Previous` están deshabilitados hasta que ingrese texto. |
| `Next` | Busca la siguiente aparición del término buscado. Vuelve al principio cuando se alcanza el final del documento. |
| `Previous` | Busca la aparición anterior del término buscado. Vuelve al final cuando se alcanza el inicio del documento. |
| Sugerencia / pie de página | Muestra una breve sugerencia de uso. Solo lectura. |
| `Close` | Cierra el diálogo de ayuda. |

## Consejos

- Cada entrada bajo el menú `Help` abre un diálogo separado para ese tema, por lo que puede mantener varios temas abiertos al mismo tiempo.
- El contenido de ayuda está incluido con la aplicación y no requiere conexión de red.
- Si no se puede cargar un archivo de ayuda, el visor muestra un aviso pidiéndole que reinstale AetherSDR o que informe sobre el recurso faltante.
- El diálogo de ayuda ahora sigue el tema actual. Sus colores cambian automáticamente cuando cambia de tema en `Settings > Appearance`.

## Relacionados

- [Lea el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conozca las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configure modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Comprenda cómo contribuir con informes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
