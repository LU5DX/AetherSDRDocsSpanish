# Leer el documento de ayuda completo de AetherSDR

El sistema de ayuda de AetherSDR incluye varias guías sin conexión que cubren la configuración, la cancelación de ruido, los modos de datos y más. Use el menú Help para abrir cualquier tema sin necesidad de conexión a internet.

## Antes de comenzar

- AetherSDR debe estar instalado y en ejecución. No se requiere conexión a un radio.

## Pasos

1. Haga clic en `Help` en la barra de menús.
2. Seleccione cualquiera de los siguientes elementos para abrir la guía correspondiente:
   - `Help > Getting Started...`
   - `Help > AetherSDR Help...`
   - `Help > Understanding Noise Cancellation...`
   - `Help > Configuring AetherSDR Controls...`
   - `Help > Configuring Data Modes...`
   - `Help > Contributing to AetherSDR...`
3. Lea el contenido en el visor Markdown. Desplácese según sea necesario.
4. Para buscar dentro del tema abierto, escriba una palabra o frase en el campo `Find:`.
5. Haga clic en `Next` para ir a la siguiente coincidencia, o haga clic en `Previous` para ir a la coincidencia anterior. La búsqueda se reinicia al llegar al final o al inicio del documento.
6. Haga clic en `Close` para cerrar el diálogo.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| `AETHERSDR OFFLINE HELP` (encabezado superior) | Encabezado de marca que se muestra sobre el título del tema. Solo lectura. |
| Title | Muestra el nombre del tema de ayuda abierto. Solo lectura. |
| Subtitle | Descripción de una línea: "Bundled help is available even when your station computer is offline." Solo lectura. |
| Campo `Find:` | Escriba un término de búsqueda para localizar texto dentro del tema actual. El texto de marcador de posición dice "Subject or term". El borde se torna rojo cuando no hay coincidencias. |
| `Next` | Encuentra la siguiente ocurrencia del término de búsqueda. Se activa solo cuando el campo `Find:` contiene texto. Atajo de teclado: Return. |
| `Previous` | Encuentra la ocurrencia anterior del término de búsqueda. Se activa solo cuando el campo `Find:` contiene texto. Atajo de teclado: Shift+Return. |
| Visor Markdown | Renderiza el tema de ayuda cargado. Los enlaces externos se abren en su navegador predeterminado. |
| Hint / footer | Indica: "Tip: The Help menu keeps each guide separate so you can reopen just the topic you need." Solo lectura. |
| `Close` | Cierra el diálogo de ayuda. |

## Consejos

- Cada elemento del menú Help abre un diálogo separado, por lo que puede tener más de un tema abierto al mismo tiempo.
- Presione el atajo estándar de búsqueda (`Ctrl+F` en Linux y Windows, `Cmd+F` en macOS) mientras el diálogo está enfocado para mover el cursor directamente al campo `Find:`.
- Si no se encuentra un término de búsqueda, el borde del campo `Find:` se torna rojo y el área de estado muestra "No matches". Borrar el campo restablece el estado.

## Relacionados

- [Abrir la guía de inicio incluida](open-bundled-getting-started-guide.md)
- [Conocer las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configurar modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Entender cómo contribuir con informes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
