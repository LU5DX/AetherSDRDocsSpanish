# Resumen de la Ayuda sin Conexión de AetherSDR

AetherSDR incluye un lector de ayuda integrado que muestra documentación en Markdown empaquetada sin necesidad de conexión a internet. Úselo para leer guías de inicio, aprender sobre los modos de cancelación de ruido, configurar modos de datos y más.

## Cómo funciona

Cada tema de ayuda se abre en su propia ventana HelpDialog. La ventana es independiente de la conexión con la radio: puede leer la ayuda en cualquier momento, incluso cuando no hay ninguna radio conectada.

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
| **AETHERSDR OFFLINE HELP** | Encabezado de marca mostrado sobre el título del tema. Indicador de solo lectura. |
| **Título** | Muestra el nombre del tema como título de la ventana. Solo lectura. |
| **Subtítulo** | Descripción de una línea: "La ayuda empaquetada está disponible incluso cuando su computadora no está conectada a internet". Solo lectura. |
| **Campo Buscar:** | Escriba un asunto o término para buscar dentro del tema actual. El borde del campo se vuelve rojo cuando no hay coincidencias. Actívelo con el atajo de teclado estándar de Buscar o haciendo clic en el campo. |
| **Siguiente** | Busca la siguiente aparición del término de búsqueda. Habilitado solo cuando el campo Buscar contiene texto. Presione Retorno en el campo Buscar para el mismo efecto. Vuelve al inicio del documento cuando se llega al final. |
| **Anterior** | Busca la aparición anterior del término de búsqueda. Habilitado solo cuando el campo Buscar contiene texto. Presione Mayús+Retorno en el campo Buscar para el mismo efecto. Vuelve al final cuando se llega al inicio. |
| **Visor de Markdown** | Muestra el tema de ayuda cargado. Solo lectura. Los enlaces externos se abren en su navegador del sistema. |
| **Pista / pie de página** | Muestra el consejo: "El menú Help mantiene cada guía separada para que pueda reabrir solo el tema que necesita". Solo lectura. |
| **Cerrar** | Cierra la ventana de ayuda. |

## Consejos

- El campo Buscar solo busca dentro del tema actualmente abierto. Para buscar en una guía diferente, ábrala desde el menú Help y use Buscar allí.
- Si no se encuentra un término de búsqueda desde la posición de desplazamiento actual, el visor vuelve automáticamente y muestra "Vuelto al inicio" o "Vuelto al final" como indicador de estado junto al campo Buscar. Si no hay ninguna coincidencia, muestra "Sin coincidencias".
- No hay configuraciones persistentes asociadas con el lector de ayuda. No se guarda nada cuando lo cierra.

## Relacionados

- [Abrir la guía de inicio empaquetada](open-bundled-getting-started-guide.md)
- [Leer el documento completo de ayuda de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conozca las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configurar modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Comprenda cómo contribuir con informes de errores y PR](understand-how-to-contribute-bug-reports-and-prs.md)
