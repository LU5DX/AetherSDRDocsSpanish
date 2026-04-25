# Descripción general de la ayuda sin conexión de AetherSDR

AetherSDR incluye un lector de ayuda integrado que muestra documentación Markdown incluida en el programa sin necesidad de conexión a internet. Úselo para leer guías de inicio, aprender sobre los modos de cancelación de ruido, configurar modos de datos y más.

## Cómo funciona

Cada tema de ayuda se abre en su propia ventana HelpDialog. La ventana es independiente de la conexión al radio; puede leer la ayuda en cualquier momento, incluso cuando no hay ningún radio conectado.

Abra cualquier tema desde el menú Help:

- `Help > Getting Started...`
- `Help > AetherSDR Help...`
- `Help > Understanding Noise Cancellation...`
- `Help > Configuring AetherSDR Controls...`
- `Help > Configuring Data Modes...`
- `Help > Contributing to AetherSDR...`

Cada entrada abre una ventana independiente precargada con ese tema. Es posible tener varias ventanas de ayuda abiertas al mismo tiempo.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **AETHERSDR OFFLINE HELP** | Encabezado de marca que aparece sobre el título del tema. Indicador de solo lectura. |
| **Title** | Muestra el nombre del tema como título de la ventana. Solo lectura. |
| **Subtitle** | Descripción de una línea: "Bundled help is available even when your station computer is offline." Solo lectura. |
| **Find:** campo | Escriba un término o asunto para buscar dentro del tema actual. El borde del campo se vuelve rojo cuando no hay coincidencias. Se activa con el atajo de teclado estándar de búsqueda o haciendo clic en el campo. |
| **Next** | Encuentra la siguiente aparición del término buscado. Se habilita solo cuando el campo Find contiene texto. Presione Return en el campo Find para el mismo efecto. Regresa al inicio del documento cuando se llega al final. |
| **Previous** | Encuentra la aparición anterior del término buscado. Se habilita solo cuando el campo Find contiene texto. Presione Shift+Return en el campo Find para el mismo efecto. Regresa al final cuando se llega al inicio. |
| **Markdown viewer** | Muestra el tema de ayuda cargado. Solo lectura. Los enlaces externos se abren en el navegador del sistema. |
| **Hint / footer** | Muestra el consejo: "The Help menu keeps each guide separate so you can reopen just the topic you need." Solo lectura. |
| **Close** | Cierra la ventana de ayuda. |

## Consejos

- El campo Find busca únicamente en el tema actualmente abierto. Para buscar en una guía diferente, ábrala desde el menú Help y use Find en esa ventana.
- Si no se encuentra el término buscado desde la posición de desplazamiento actual, el visor regresa automáticamente al inicio o al final y muestra "Wrapped to top" o "Wrapped to bottom" como indicador de estado junto al campo Find. Si no hay ninguna coincidencia, muestra "No matches."
- No se guardan configuraciones asociadas al lector de ayuda. No se almacena nada al cerrarlo.

## Relacionado

- [Abrir la guía de inicio incluida en el programa](open-bundled-getting-started-guide.md)
- [Leer el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conocer las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configurar los modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Entender cómo contribuir con informes de errores y solicitudes de cambio](understand-how-to-contribute-bug-reports-and-prs.md)
