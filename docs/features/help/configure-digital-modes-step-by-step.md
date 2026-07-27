# Configurar modos digitales paso a paso

Esta página explica cómo abrir la guía incluida de AetherSDR para configurar modos digitales (de datos). La guía está disponible sin conexión y lo guía a través de la configuración paso a paso.

## Antes de comenzar

- AetherSDR debe estar instalado. No se requiere conexión de radio para leer los temas de ayuda.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Haga clic en `Configuring Data Modes...`.
3. Se abre el HelpDialog, que muestra la guía de modos de datos en el visor Markdown. El encabezado del diálogo muestra "AETHERSDR OFFLINE HELP" con el título y subtítulo del tema.
4. Lea la guía. Desplácese según sea necesario.
5. Para buscar dentro de la guía, escriba un término en el campo `Find:` y haga clic en `Next` para avanzar entre las coincidencias o en `Previous` para retroceder. Presione Return para pasar a la siguiente coincidencia; presione Shift+Return para ir a la coincidencia anterior.
6. Haga clic en `Close` cuando termine.

## Qué hace cada control

| Control         | Comportamiento                                                                                                                                           | Notas                                                                                                                                                        |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Campo `Find:`   | Ingrese un asunto o término para buscar dentro del tema mostrado. El borde del campo se vuelve rojo si no se encuentran coincidencias.                   |                                                                                                                                                              |
| `Next`          | Avanza a la siguiente coincidencia en el documento. Vuelve al principio cuando se llega al final. Habilitado solo cuando el campo `Find:` no está vacío.  |                                                                                                                                                              |
| `Previous`      | Retrocede a la coincidencia anterior en el documento. Vuelve al final cuando se llega al principio. Habilitado solo cuando el campo `Find:` no está vacío. |                                                                                                                                                              |
| `Close`         | Cierra el diálogo de ayuda.                                                                                                                               |                                                                                                                                                              |
| Find:           | Campo de búsqueda para encontrar texto en el documento de ayuda. Habilita los botones Next y Previous cuando no está vacío.                              | Ctrl+F enfoca el campo. Enter salta a la siguiente coincidencia; Shift+Enter salta a la anterior. QLineEdit con botón de borrar y marcador 'Subject or term'. |
| Next (Find)     | Salta a la siguiente coincidencia del término de búsqueda.                                                                                                | Deshabilitado cuando el campo de búsqueda está vacío. Vuelve del final al principio.                                                                         |
| Previous (Find) | Salta a la coincidencia anterior del término de búsqueda.                                                                                                 | Deshabilitado cuando el campo de búsqueda está vacío. Vuelve del principio al final.                                                                         |
| Estado Find     | Muestra 'No matches' (rojo) o 'Wrapped to top/bottom' cuando no se encuentran más coincidencias en la dirección actual.                                   |                                                                                                                                                              |

## Consejos

- Cada tema de ayuda se abre en su propio diálogo y recuerda su propia posición y tamaño de forma independiente. Puede volver a abrir `Help > Configuring Data Modes...` en cualquier momento sin afectar otras ventanas de ayuda abiertas.
- La ayuda incluida está disponible incluso cuando su computadora de estación no tiene acceso a internet.
- El diálogo utiliza el esquema de colores del tema actual para su fondo, texto y colores de acento.

## Relacionado

- [Abrir la guía de inicio rápido incluida](open-bundled-getting-started-guide.md)
- [Leer el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
