# Descripción general de la ayuda sin conexión de AetherSDR

AetherSDR incluye un lector de ayuda integrado que muestra guías en formato Markdown directamente en la aplicación. La ayuda está disponible sin conexión a internet, por lo que puede consultarla en la mesa de trabajo o en el campo.

## Cómo funciona

Cada entrada del menú `Help` abre una instancia independiente del lector de ayuda, precargada con el tema correspondiente a ese elemento de menú. Los temas disponibles son:

| Elemento de menú | Tema |
|---|---|
| `Help > Getting Started...` | Primeros pasos con AetherSDR |
| `Help > AetherSDR Help...` | Documento de ayuda completo de AetherSDR |
| `Help > Understanding Noise Cancellation...` | Reducción de ruido NR2, NR4, DFNR y MNR |
| `Help > Configuring AetherSDR Controls...` | Referencia de controles de AetherSDR |
| `Help > Configuring Data Modes...` | Configuración de modos digitales |
| `Help > Contributing to AetherSDR...` | Informes de errores y contribuciones |

Cada diálogo se abre de forma independiente. Es posible tener más de un tema abierto al mismo tiempo.

La ventana se abre con un tamaño de 760 × 680 píxeles y puede reducirse hasta un mínimo de 520 × 420 píxeles.

Si AetherSDR no encuentra el archivo incluido para un tema, el visor de Markdown muestra un mensaje indicando que el archivo de ayuda no está disponible, junto con instrucciones para reinstalar la aplicación.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `AETHERSDR OFFLINE HELP` | Indicador (encabezado secundario) | Encabezado de marca que se muestra sobre el título del tema. Solo lectura. |
| Title | Indicador | Muestra el nombre del tema indicado al abrir el diálogo. Solo lectura. |
| Subtitle | Indicador | Línea fija: "Bundled help is available even when your station computer is offline." Solo lectura. |
| Visor de Markdown | Área de texto desplazable | Renderiza el tema Markdown cargado. Admite desplazamiento interno. Los enlaces externos se abren en el navegador predeterminado. |
| Hint / footer | Indicador | Muestra: "Tip: The Help menu keeps each guide separate so you can reopen just the topic you need." Solo lectura. |
| Close | Botón | Cierra el diálogo de ayuda. |

Ningún ajuste de este diálogo se guarda de forma persistente.

## Consejos

- Los elementos del menú `Help` son independientes. Abra `Help > Understanding Noise Cancellation...` y `Help > Configuring Data Modes...` en paralelo si necesita ambos.
- No se requiere conexión a la radio para abrir ningún tema de ayuda.

## Solución de problemas

- **El visor de Markdown muestra "Help file not available"** — El recurso de ayuda incluido en la instalación no se encuentra. Reinstale AetherSDR e inténtelo de nuevo.

## Relacionados

- [Abrir la guía de primeros pasos incluida](open-bundled-getting-started-guide.md)
- [Leer el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
- [Conocer las diferencias entre NR2, NR4, DFNR y MNR](learn-the-differences-between-nr2-nr4-dfnr-and-mnr.md)
- [Configurar los modos digitales paso a paso](configure-digital-modes-step-by-step.md)
- [Entender cómo contribuir con informes de errores y solicitudes de cambio](understand-how-to-contribute-bug-reports-and-prs.md)
