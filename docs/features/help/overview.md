# Resumen de la Ayuda Desconectada de AetherSDR

AetherSDR incluye un lector de ayuda integrado que muestra documentación en formato Markdown sin necesidad de conexión a internet. Úselo para leer guías de inicio, aprender sobre los modos de cancelación de ruido, configurar modos de datos y más.

## Cómo funciona

Cada tema de ayuda se abre en su propia ventana HelpDialog. La ventana es independiente de la conexión con la radio: puede leer la ayuda en cualquier momento, incluso cuando no haya ninguna radio conectada.

Abra cualquier tema desde el menú Help:

- `Help > Getting Started...`
- `Help > AetherSDR Help...`
- `Help > Understanding Noise Cancellation...`
- `Help > Configuring AetherSDR Controls...`
- `Help > Configuring Data Modes...`
- `Help > Contributing to AetherSDR...`

Cada entrada abre una ventana separada precargada con ese tema. Puede tener varias ventanas de ayuda abiertas al mismo tiempo. Cada ventana recuerda su propia posición y tamaño de forma independiente: al cerrar y volver a abrir un tema, se restaura su geometría anterior.

## Función de cada control

| Control                      | Descripción                                                                                                                                                                                                                         | Notas                                                                                                                                                       |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **AETHERSDR OFFLINE HELP**   | Encabezado de marca que se muestra sobre el título del tema. Indicador de solo lectura.                                                                                                                                             |                                                                                                                                                             |
| **Título**                   | Muestra el nombre del tema como título de la ventana. Solo lectura.                                                                                                                                                                |                                                                                                                                                             |
| **Subtítulo**                | Descripción de una línea: "La ayuda integrada está disponible incluso cuando su equipo de estación está desconectado." Solo lectura.                                                                                                |                                                                                                                                                             |
| **Campo Buscar:**            | Escriba un asunto o término para buscar dentro del tema actual. El borde del campo se vuelve rojo cuando no hay coincidencias. Actívelo con el atajo de teclado Buscar estándar o haciendo clic en el campo.       | Ctrl+F enfoca el campo. Enter salta a la siguiente coincidencia; Shift+Enter salta a la anterior. QLineEdit con botón de borrar y marcador 'Asunto o término'. |
| **Siguiente**                | Salta a la siguiente coincidencia del término de búsqueda. Solo está habilitado cuando el campo Buscar contiene texto. Presione Enter en el campo Buscar para el mismo efecto. Vuelve del final al principio.                     | Deshabilitado cuando el campo de búsqueda está vacío.                                                                                                      |
| **Anterior**                 | Salta a la coincidencia anterior del término de búsqueda. Solo está habilitado cuando el campo Buscar contiene texto. Presione Shift+Enter en el campo Buscar para el mismo efecto. Vuelve del principio al final.                 | Deshabilitado cuando el campo de búsqueda está vacío.                                                                                                      |
| **Estado de búsqueda**       | Muestra 'Sin coincidencias' (en rojo) o 'Vuelto al principio/final' cuando no se encuentran más coincidencias en la dirección actual.                                                                                              |                                                                                                                                                             |
| **Visor Markdown**           | Representa el tema de ayuda cargado. Solo lectura. Los enlaces externos se abren en el navegador del sistema.                                                                                                                       |                                                                                                                                                             |
| **Sugerencia / pie de página** | Muestra el consejo: "El menú Help mantiene cada guía separada para que pueda reabrir solo el tema que necesita." Solo lectura.                                                                                                     |                                                                                                                                                             |
| **Cerrar**                   | Cierra la ventana de ayuda.                                                                                                                                                                                                        |                                                                                                                                                             |

## Apariencia

El diálogo de ayuda utiliza colores adaptados al tema. El fondo del encabezado, los colores del texto y los colores de la barra de desplazamiento se estilizan según el tema actual de AetherSDR. El diseño general incluye tokens del tema para el fondo del encabezado, color de acento, texto primario y secundario, y capas de fondo para el visor principal y las barras de desplazamiento.

## Consejos

- El campo Buscar solo busca en el tema abierto actualmente. Para buscar en otra guía, ábrala desde el menú Help y use Buscar allí.
- Si no se encuentra un término de búsqueda desde la posición de desplazamiento actual, el visor vuelve automáticamente y muestra "Vuelto al principio" o "Vuelto al final" como indicador de estado junto al campo Buscar. Si no hay ninguna coincidencia, muestra "Sin coincidencias".
- Cada tema de ayuda recuerda su propia posición y tamaño de ventana. Abra dos guías diferentes a la vez, muévalas a distintas ubicaciones de la pantalla y ciérrelas. La próxima vez que abra cada guía, volverá a su posición anterior.

## Relacionados

- [Abra la guía de inicio incluida](open-bundled-getting-started-guide.md)
- [Lea el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conozca las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configure los modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Comprenda cómo contribuir con informes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
