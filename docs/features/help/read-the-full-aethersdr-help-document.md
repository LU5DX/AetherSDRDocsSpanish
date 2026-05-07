# Lea el documento de ayuda completo de AetherSDR

El sistema de ayuda de AetherSDR incluye varias guías sin conexión que cubren configuración, cancelación de ruido, modos de datos y más. Use el menú Help para abrir cualquier tema sin necesidad de conexión a internet.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución. No se requiere conexión de radio.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Seleccione cualquiera de los siguientes elementos para abrir la guía correspondiente:
   - `Help > Getting Started...`
   - `Help > AetherSDR Help...`
   - `Help > Understanding Noise Cancellation...`
   - `Help > Configuring AetherSDR Controls...`
   - `Help > Configuring Data Modes...`
   - `Help > Contributing to AetherSDR...`
3. Lea el contenido en el visor Markdown. Desplácese según sea necesario.
4. Para buscar dentro del tema abierto, escriba una palabra o frase en el campo `Find:`.
5. Haga clic en `Next` para saltar a la siguiente coincidencia, o en `Previous` para ir a la coincidencia anterior. La búsqueda se reinicia al llegar al final o al inicio del documento.
6. Haga clic en `Close` para cerrar el diálogo.

## Función de cada control

| Control | Comportamiento |
|---|---|
| `AETHERSDR OFFLINE HELP` (encabezado) | Encabezado de marca mostrado arriba del título del tema. Solo lectura. |
| Título | Muestra el nombre del tema de ayuda abierto. Solo lectura. |
| Subtítulo | Descripción de una línea: "La ayuda incluida está disponible incluso cuando su equipo de estación está sin conexión". Solo lectura. |
| Campo `Find:` | Escriba un término de búsqueda para localizar texto dentro del tema actual. El texto de marcador de posición dice "Subject or term". El borde se vuelve rojo cuando no hay coincidencias. |
| `Next` | Busca la siguiente aparición del término de búsqueda. Activado solo cuando el campo `Find:` contiene texto. Atajo de teclado: Enter. |
| `Previous` | Busca la aparición anterior del término de búsqueda. Activado solo cuando el campo `Find:` contiene texto. Atajo de teclado: Mayús+Enter. |
| Visor Markdown | Renderiza el tema de ayuda cargado. Los enlaces externos se abren en su navegador predeterminado. |
| Sugerencia / pie de página | Dice: "Consejo: El menú Help mantiene cada guía separada para que pueda reabrir solo el tema que necesita". Solo lectura. |
| `Close` | Cierra el diálogo de ayuda. |

## Consejos

- Cada elemento del menú Help abre un diálogo separado, por lo que puede tener más de un tema abierto al mismo tiempo.
- Presione el atajo de búsqueda estándar (Ctrl+F en Linux y Windows, Cmd+F en macOS) mientras el diálogo está enfocado para mover el cursor directamente al campo `Find:`.
- Si no se encuentra un término de búsqueda, el borde del campo `Find:` se vuelve rojo y el área de estado muestra "No matches". Al borrar el campo se restablece el estado.

## Relacionado

- [Abra la guía de inicio incluida](open-bundled-getting-started-guide.md)
- [Conozca las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configure modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Comprenda cómo contribuir con informes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
