# Comprenda Cómo Contribuir con Informes de Errores y PRs

Esta página explica cómo abrir la guía de contribución incluida en AetherSDR. La guía cubre cómo reportar errores y enviar solicitudes de incorporación de cambios sin necesidad de conexión a internet.

## Antes de comenzar

- AetherSDR debe estar instalado. No se requiere conexión de radio.

## Pasos

1. Haga clic en `Help` en la barra de menú.
2. Haga clic en `Contributing to AetherSDR...`.
3. Se abrirá el HelpDialog, mostrando la guía de contribución en el visor Markdown. El diálogo utiliza el tema actual para todos los elementos visuales.
4. Para buscar dentro de la guía, escriba un término en el campo `Find:` y haga clic en `Next` para avanzar entre coincidencias o `Previous` para retroceder. Presione Return para encontrar la siguiente coincidencia. Presione Shift+Return para encontrar la coincidencia anterior.
5. Cuando haya terminado, haga clic en `Close`.

## Función de cada control

| Control                            | Comportamiento                                                                                                                                 | Notas                                                                                                                                              |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| `AETHERSDR OFFLINE HELP` (encabezado) | Encabezado de marca mostrado sobre el título.                                                                                                           |                                                                                                                                                    |
| `Title`                            | Muestra el título de la ventana (nombre del tema).                                                                                                       |                                                                                                                                                    |
| `Subtitle`                         | Descripción del tema en una línea.                                                                                                                   |                                                                                                                                                    |
| `Markdown viewer`                  | Renderiza el recurso Markdown cargado. Diseñado según el tema actual.                                                                  |                                                                                                                                                    |
| Campo `Find:`                      | Ingrese un asunto o término para buscar dentro del tema mostrado. El borde del campo se vuelve rojo cuando no hay coincidencias.                           | Ctrl+F enfoca el campo. Enter salta a la siguiente coincidencia; Shift+Enter salta a la anterior. QLineEdit con botón de borrado y marcador de posición 'Subject or term'. |
| `Next`                             | Avanza a la siguiente coincidencia en el documento. Vuelve al inicio cuando se llega al final. Habilitado solo cuando el campo `Find:` no está vacío.          | Deshabilitado cuando el campo de búsqueda está vacío. Vuelve del final al inicio.                                                                                 |
| `Previous`                         | Retrocede a la coincidencia anterior en el documento. Vuelve al final cuando se llega al inicio. Habilitado solo cuando el campo `Find:` no está vacío. | Deshabilitado cuando el campo de búsqueda está vacío. Vuelve del inicio al final.                                                                                 |
| `Find status`                      | Muestra 'No matches' (rojo) o 'Wrapped to top/bottom' cuando no se encuentran más coincidencias en la dirección actual.                               |                                                                                                                                                    |
| `Hint / footer`                    | Muestra una sugerencia de uso breve.                                                                                                                     |                                                                                                                                                    |

## Consejos

- El menú Help mantiene cada guía en un diálogo separado. Cada diálogo recuerda su propia posición y tamaño de ventana de forma independiente. Puede reabrir solo este tema en cualquier momento sin interferir con otras ventanas de ayuda abiertas.
- La guía de contribución está disponible sin conexión. No necesita una conexión de red para leerla.
- Todos los colores del HelpDialog, incluidos el fondo del encabezado, los colores del texto, los colores de la barra de desplazamiento y el separador, están controlados por el tema activo. Para cambiar la apariencia, seleccione `Settings > Theme...`.

## Relacionados

- [Abra la guía de inicio incluida](open-bundled-getting-started-guide.md)
- [Lea el documento de ayuda completo de AetherSDR](read-the-full-aethersdr-help-document.md)
