# Lea el documento de ayuda completo de AetherSDR

El sistema de ayuda de AetherSDR incluye varias guías sin conexión que cubren configuración, cancelación de ruido, modos de datos y más. Use el menú Help para abrir cualquier tema sin necesidad de conexión a internet.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución. No se requiere conexión a la radio.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Seleccione cualquiera de los siguientes elementos para abrir la guía correspondiente:
   - `Help > Getting Started...`
   - `Help > AetherSDR Help...`
   - `Help > Understanding Noise Cancellation...`
   - `Help > Configuring AetherSDR Controls...`
   - `Help > Configuring Data Modes...`
   - `Help > Contributing to AetherSDR...`
3. Lea el contenido en el visor de Markdown. Desplácese según sea necesario.
4. Para buscar dentro del tema abierto, escriba una palabra o frase en el campo `Find:`.
5. Haga clic en `Next` para saltar a la siguiente coincidencia, o en `Previous` para ir a la coincidencia anterior. La búsqueda se reinicia al llegar al final o al inicio del documento.
6. Haga clic en `Close` para cerrar el cuadro de diálogo.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `AETHERSDR OFFLINE HELP` (encabezado superior) | Encabezado de marca mostrado sobre el título del tema. Solo lectura. |
| Título | Muestra el nombre del tema de ayuda abierto. Solo lectura. |
| Subtítulo | Descripción de una línea: "La ayuda incluida está disponible incluso cuando su computadora de estación está sin conexión." Solo lectura. |
| Campo `Find:` | Escriba un término de búsqueda para localizar texto dentro del tema actual. El texto de marcador de posición dice "Asunto o término". El borde se vuelve rojo cuando no hay coincidencias. |
| `Next` | Busca la siguiente aparición del término de búsqueda. Habilitado solo cuando el campo `Find:` contiene texto. Método abreviado de teclado: Return. |
| `Previous` | Busca la aparición anterior del término de búsqueda. Habilitado solo cuando el campo `Find:` contiene texto. Método abreviado de teclado: Shift+Return. |
| Visor de Markdown | Muestra el tema de ayuda cargado. Los enlaces externos se abren en su navegador predeterminado. |
| Sugerencia / pie de página | Dice: "Consejo: El menú Help mantiene cada guía separada para que pueda reabrir solo el tema que necesita." Solo lectura. |
| `Close` | Cierra el cuadro de diálogo de ayuda. |

## Apariencia y temas

El cuadro de diálogo de ayuda ahora sigue el tema activo en lugar de usar colores fijos. Todos los colores de encabezados, separadores, navegador y pie de página están determinados por las variables del tema. El contenedor del cuadro de diálogo está registrado bajo `dialog/help` en el sistema de temas. Esto garantiza un estilo visual consistente cuando cambia entre temas claro y oscuro o utiliza archivos de tema personalizados.

## Consejos

- Cada elemento del menú Help abre un cuadro de diálogo separado, por lo que puede tener más de un tema abierto al mismo tiempo.
- Presione el método abreviado estándar de búsqueda (Ctrl+F en Linux y Windows, Cmd+F en macOS) mientras el cuadro de diálogo está enfocado para mover el cursor directamente al campo `Find:`.
- Si no se encuentra un término de búsqueda, el borde del campo `Find:` se vuelve rojo y el área de estado muestra "Sin coincidencias". Al borrar el campo se restablece el estado.

## Relacionados

- [Abra la guía de inicio incluida](open-bundled-getting-started-guide.md)
- [Conozca las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configure modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Comprenda cómo contribuir con informes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
