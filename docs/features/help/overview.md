# Resumen de la ayuda sin conexión de AetherSDR

AetherSDR incluye un lector de ayuda integrado que muestra documentación en formato Markdown sin necesidad de conexión a internet. Úselo para leer guías de inicio, aprender sobre los modos de cancelación de ruido, configurar modos de datos y mucho más.

## Cómo funciona

Cada tema de ayuda se abre en su propia ventana HelpDialog. La ventana es independiente de la conexión con la radio; puede leer la ayuda en cualquier momento, incluso cuando no haya ninguna radio conectada.

Abra cualquier tema desde el menú Help:

- `Help > Getting Started...`
- `Help > AetherSDR Help...`
- `Help > Understanding Noise Cancellation...`
- `Help > Configuring AetherSDR Controls...`
- `Help > Configuring Data Modes...`
- `Help > Contributing to AetherSDR...`

Cada entrada abre una ventana independiente precargada con ese tema. Puede tener varias ventanas de ayuda abiertas al mismo tiempo.

## Función de cada control

| Control | Descripción |
|---|---|
| **AETHERSDR OFFLINE HELP** | Encabezado de marca mostrado sobre el título del tema. Indicador de solo lectura. |
| **Title** | Muestra el nombre del tema como título de la ventana. Solo lectura. |
| **Subtitle** | Descripción de una línea: "Bundled help is available even when your station computer is offline." Solo lectura. |
| **Find:** field | Escriba un asunto o término para buscar dentro del tema actual. El borde del campo se vuelve rojo cuando no hay coincidencias. Actívelo con el atajo de teclado estándar de Find o haciendo clic en el campo. |
| **Next** | Busca la siguiente ocurrencia del término buscado. Se habilita solo cuando el campo Find contiene texto. Presione Return en el campo Find para el mismo efecto. Vuelve al inicio del documento cuando se llega al final. |
| **Previous** | Busca la ocurrencia anterior del término buscado. Se habilita solo cuando el campo Find contiene texto. Presione Shift+Return en el campo Find para el mismo efecto. Vuelve al final cuando se llega al inicio. |
| **Markdown viewer** | Muestra el tema de ayuda cargado. Solo lectura. Los enlaces externos se abren en su navegador del sistema. |
| **Hint / footer** | Muestra el consejo: "The Help menu keeps each guide separate so you can reopen just the topic you need." Solo lectura. |
| **Close** | Cierra la ventana de ayuda. |

## Apariencia

El cuadro de diálogo Help utiliza colores que se adaptan al tema. El fondo del encabezado, los colores del texto y los colores de la barra de desplazamiento se estilizan según el tema actual de AetherSDR. El diseño general incluye tokens de tema para el fondo del encabezado, el color de acento, el texto primario y secundario, y las capas de fondo del visor principal y las barras de desplazamiento.

## Consejos

- El campo Find busca solo dentro del tema actualmente abierto. Para buscar en otra guía, ábrala desde el menú Help y use Find allí.
- Si no se encuentra un término de búsqueda desde la posición de desplazamiento actual, el visor vuelve automáticamente y muestra "Wrapped to top" o "Wrapped to bottom" como indicador de estado junto al campo Find. Si no hay ninguna coincidencia en absoluto, muestra "No matches."
- No hay configuraciones persistentes asociadas con el lector de ayuda. No se guarda nada al cerrarlo.

## Relacionados

- [Open bundled getting-started guide](open-bundled-getting-started-guide.md)
- [Read the full AetherSDR help document](read-the-full-aethersdr-help-document.md)
- [Learn the differences between NR2, NR4, DFNR and MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configure digital modes step-by-step](configure-digital-modes-step-by-step.md)
- [Understand how to contribute bug reports and PRs](understand-how-to-contribute-bug-reports-and-prs.md)
