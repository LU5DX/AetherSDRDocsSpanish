# Leer el documento de ayuda completo de AetherSDR

El HelpDialog es un lector de Markdown sin conexión integrado en AetherSDR. Úselo para consultar las guías de referencia incluidas sin necesidad de conexión a Internet.

## Antes de comenzar

- No se requiere conexión a radio para abrir temas de ayuda.
- AetherSDR debe estar instalado con sus archivos de ayuda incluidos intactos. Si falta un archivo de ayuda, el visor muestra un mensaje de error en lugar del contenido del tema.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Haga clic en `Help > AetherSDR Help...`.
3. Se abre la ventana de ayuda. El encabezado muestra la etiqueta **AETHERSDR OFFLINE HELP** sobre el título y el subtítulo del tema.
4. Desplácese por el visor de Markdown para leer el contenido.
5. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **AETHERSDR OFFLINE HELP** | Indicador | Etiqueta de marca que se muestra sobre el título del tema. No es interactiva. |
| Title | Indicador | Muestra el nombre del tema de ayuda abierto. |
| Subtitle | Indicador | Descripción de una línea: "Bundled help is available even when your station computer is offline." |
| Markdown viewer | Área de texto | Renderiza el archivo Markdown incluido para el tema. Solo lectura. Los enlaces externos se abren en el navegador predeterminado. |
| Hint / footer | Indicador | Muestra el consejo: "The Help menu keeps each guide separate so you can reopen just the topic you need." |
| `Close` | Botón | Cierra la ventana de ayuda. |

## Consejos

- Cada tema de ayuda se abre en su propia ventana. Puede abrir varios temas uno al lado del otro eligiendo diferentes elementos del menú `Help` sin cerrar la ventana anterior.
- Los seis temas están disponibles desde el menú `Help`: `Help > Getting Started...`, `Help > AetherSDR Help...`, `Help > Understanding Noise Cancellation...`, `Help > Configuring AetherSDR Controls...`, `Help > Configuring Data Modes...` y `Help > Contributing to AetherSDR...`.

## Solución de problemas

- **El visor muestra "Help file not available" en lugar del contenido** — Falta un archivo de ayuda incluido en la instalación. Reinstale AetherSDR y confirme que todos los archivos estén presentes, o reporte el archivo faltante al proyecto.

## Relacionados

- [Abrir la guía de inicio rápido incluida](open-bundled-getting-started-guide.md)
- [Conocer las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configurar modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Entender cómo contribuir con informes de errores y PRs](understand-how-to-contribute-bug-reports-and-prs.md)
