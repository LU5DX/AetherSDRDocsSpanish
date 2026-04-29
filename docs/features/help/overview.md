# Descripción general de la ayuda sin conexión de AetherSDR

AetherSDR incluye un lector de ayuda integrado que muestra documentación Markdown empaquetada sin necesidad de conexión a internet. Úselo para leer guías de inicio, aprender sobre los modos de cancelación de ruido, configurar modos de datos y más.

## Cómo funciona

Cada tema de ayuda se abre en su propia ventana HelpDialog. La ventana es independiente de la conexión de radio — puede leer la ayuda en cualquier momento, incluso cuando no hay ninguna radio conectada.

Abra cualquier tema desde el menú Help:

- `Help > Getting Started...`
- `Help > AetherSDR Help...`
- `Help > Understanding Noise Cancellation...`
- `Help > Configuring AetherSDR Controls...`
- `Help > Configuring Data Modes...`
- `Help > Contributing to AetherSDR...`

Cada entrada abre una ventana separada precargada con ese tema. Puede tener varias ventanas de ayuda abiertas al mismo tiempo.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **AETHERSDR OFFLINE HELP** | Encabezado de marca que se muestra sobre el título del tema. Indicador de solo lectura. |
| **Title** | Muestra el nombre del tema como título de la ventana. Solo lectura. |
| **Subtitle** | Descripción de una línea: "Bundled help is available even when your station computer is offline." Solo lectura. |
| **Find:** field | Escriba un tema o término para buscar dentro del tema actual. El borde del campo se vuelve rojo cuando no hay coincidencias. Actívelo con el atajo de teclado estándar de búsqueda o haciendo clic en el campo. |
| **Next** | Busca la siguiente ocurrencia del término de búsqueda. Solo se habilita cuando el campo Find contiene texto. Presione Return en el campo Find para el mismo efecto. Vuelve al inicio del documento al llegar al final. |
| **Previous** | Busca la ocurrencia anterior del término de búsqueda. Solo se habilita cuando el campo Find contiene texto. Presione Shift+Return en el campo Find para el mismo efecto. Vuelve al final cuando se alcanza el inicio. |
| **Markdown viewer** | Renderiza el tema de ayuda cargado. Solo lectura. Los enlaces externos se abren en el navegador del sistema. |
| **Hint / footer** | Muestra el consejo: "The Help menu keeps each guide separate so you can reopen just the topic you need." Solo lectura. |
| **Close** | Cierra la ventana de ayuda. |

## Consejos

- El campo Find busca únicamente en el tema abierto en ese momento. Para buscar en una guía diferente, ábrala desde el menú Help y use Find allí.
- Si no se encuentra un término de búsqueda desde la posición de desplazamiento actual, el visor regresa automáticamente al inicio o al final y muestra "Wrapped to top" o "Wrapped to bottom" como indicador de estado junto al campo Find. Si no hay ninguna coincidencia, muestra "No matches."
- No se guardan configuraciones asociadas al lector de ayuda. No se almacena nada al cerrarlo.

## Relacionados

- [Abrir la guía de inicio empaquetada](open-bundled-getting-started-guide.md)
- [Leer el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conocer las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configurar modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Entender cómo contribuir con informes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
