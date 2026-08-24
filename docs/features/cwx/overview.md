# Resumen de CWX

CWX es la interfaz integrada de manipulador de CW de AetherSDR. Le permite enviar texto escrito o macros predefinidas a través del manipulador de la FLEX-8600, controlar la velocidad de envío, configurar el retardo entre macros, activar QSK full break-in y gestionar el historial de envíos, todo sin salir de la aplicación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión de radio activa.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en el área central de la ventana principal cuando hay un slice en modo CW activo.

## Cómo funciona

CWX presenta tres vistas, seleccionadas mediante los botones en la parte inferior del panel: Send, Live y Setup. El cuadro de giro Speed: y los botones de selección de vista están siempre visibles independientemente de la vista activa.

**Vista Send** — Muestra un historial desplazable de buffers enviados previamente, mostrados como burbujas de chat, con un área de entrada de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten. Si Live está actualmente activado, hacer clic en Send primero desactiva el envío en vivo sin retransmitir ningún texto que ya haya sido manipulado carácter por carácter. Si Live ya está desactivado, hacer clic en Send envía el buffer inmediatamente. Haga clic derecho en cualquier burbuja del historial para reenviar ese texto o borrar todo el historial.

**Vista Live** — Activa o desactiva el envío en vivo carácter por carácter. Cuando Live está habilitado, cada carácter que escribe se manipula inmediatamente en lugar de mantenerse hasta que presione Enter. Hacer clic en Setup o Send mientras Live está activado desactiva automáticamente el envío en vivo antes de cambiar de vista.

**Vista Setup** — Muestra los 12 editores de macros de teclas F, el control Delay: y la alternancia QSK. Edite el texto de las macros aquí y configure las opciones de temporización del manipulador. Abrir la vista Setup siempre desactiva el envío en vivo. Cada editor de macros tiene una altura mínima de aproximadamente dos líneas de texto, lo que garantiza que el texto de las macros permanezca legible incluso cuando la ventana de la aplicación está en su altura mínima.

**Atajos F1–F12** — Cuando el slice TX está en modo CW o CWL, presionar F1 a F12 en el teclado envía la macro correspondiente inmediatamente, independientemente de la vista mostrada, e incluso si el panel CWX está oculto. Estos atajos son habilitados por la ventana principal según el modo del slice TX, lo que los mantiene mutuamente excluyentes con otros paneles que usan las mismas teclas (como el panel DVK) para evitar la ambigüedad de atajos de Qt.

**Escape** — Presionar Escape aborta la transmisión CW actual y limpia el buffer de envío. Cuando se aborta una transmisión, la parte no enviada del buffer aparece con efecto tachado en la burbuja del historial. Esto funciona solo cuando los atajos de CWX están activos.

## Qué hace cada control

| Control | Descripción | Configuración persistida |
|---|---|---|
| Send | Envía el buffer escrito si Live está desactivado. Si Live está activado, desactiva el envío en vivo y cambia a la vista de envío sin retransmitir los caracteres ya manipulados. | — |
| Live | Botón de alternancia. Activa el envío en vivo carácter por carácter cuando está activado; lo desactiva cuando está desactivado. El estado del botón se mantiene sincronizado con el modelo de la radio. | — |
| Setup | Cambia a la vista de edición de macros y configuración de QSK. Desactiva el envío en vivo si está activo. | — |
| Speed: | Velocidad de envío de CW en WPM. Rango: 5–100 WPM. Predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envíos | Pantalla desplazable de buffers de envío anteriores con resaltado por carácter. Haga clic derecho en una burbuja para reenviar ese texto o borrar todo el historial. Solo lectura. | — |
| Área de texto de envío | Campo de entrada de texto. Presione Enter para enviar el buffer escrito. | — |
| F1 … F12 (botones de macros) | Envía la macro almacenada para esa tecla de función. Activo mediante atajo de teclado cuando el slice TX está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macros F1 … F12 | Campos de texto en la vista Setup para escribir o editar cada cadena de macro. Cada editor mantiene una altura mínima de aproximadamente dos líneas de texto. | `CwxMacro_F1` – `CwxMacro_F12` |
| Delay: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Predeterminado: 5 ms. | `CwxDelay` |
| QSK | Activa QSK full break-in cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra los atajos de caracteres para prosignos CW comunes (=, +, (, &, $). | — |

## Consejos

- Presionar Escape durante una transmisión de macro limpia el buffer inmediatamente. Debido a que el estado del manipulador alterna rápidamente entre puntos y rayas, Escape se activa incondicionalmente en lugar de esperar un estado de transmisión específico, por lo que detiene el envío de manera confiable.
- Cuando se aborta una transmisión con Escape, la burbuja del historial de esa transmisión muestra los caracteres ya enviados normalmente y la parte no enviada con efecto tachado. El límite del tachado coincide exactamente con cuántos caracteres se enviaron antes de la interrupción.
- Los atajos de teclado F1–F12 se activan siempre que el slice TX esté en modo CW o CWL, independientemente de si el panel CWX está visible. Esto le permite activar macros mientras opera otros paneles. Los atajos se desactivan automáticamente cuando cambia el slice TX a un modo que no sea CW.
- Haga clic derecho en cualquier burbuja del historial para reenviar su contenido o para borrar todo el historial de envíos de una vez.
- Si cambia a la vista Setup o hace clic en Send mientras Live está activado, el envío en vivo se desactiva automáticamente. No retransmitirá accidentalmente caracteres que el manipulador ya haya enviado.
- El estado del botón Live refleja directamente el modelo de la radio. Si el modelo informa que el envío en vivo está activo cuando el panel se carga por primera vez, el botón Live ya aparecerá presionado.
- El botón Send está marcado para indicar que activa el transmisor, distinguiéndolo de otros controles relacionados con la transmisión en la interfaz.
- Los editores de macros están dimensionados para permanecer legibles incluso cuando la aplicación está en su altura mínima de ventana, de modo que pueda seguir editando macros sin desplazarse.

## Relacionado

- [Enviar un buffer de CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío de CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar QSK full break-in](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
- Reenviar un buffer de CW anterior
- Borrar el historial de envíos de CW
