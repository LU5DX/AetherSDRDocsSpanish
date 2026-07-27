# Resumen de CWX

CWX es la interfaz de manipulador CW integrada de AetherSDR. Le permite enviar texto escrito o macros predefinidas a través del manipulador de la FLEX-8600, controlar la velocidad de transmisión, configurar el retardo entre macros, activar el QSK de ruptura total y gestionar el historial de envíos, todo sin salir de la aplicación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión activa a la radio.
- Configure el segmento activo en modo CW, CWL o CWU. El panel de CWX aparece en el área central de la ventana principal cuando hay un segmento en modo CW activo.

## Cómo funciona

CWX presenta tres vistas, seleccionadas mediante los botones en la parte inferior del panel: Send, Live y Setup. El control giratorio Speed: y los botones selectores de vista están siempre visibles, independientemente de la vista activa.

**Vista Send** — Muestra un historial desplazable de búferes enviados previamente, representados como burbujas de chat, con un área de entrada de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten. Si Live está activo, al hacer clic en Send primero se desactiva el envío en vivo sin retransmitir ningún texto que ya se haya manipulado carácter por carácter. Si Live ya está desactivado, al hacer clic en Send se envía el búfer inmediatamente. Haga clic derecho en cualquier burbuja del historial para reenviar ese texto o borrar todo el historial.

**Vista Live** — Activa o desactiva el envío en vivo carácter por carácter. Cuando Live está habilitado, cada carácter que escribe se manipula inmediatamente en lugar de retenerse hasta que presione Enter. Al hacer clic en Setup o Send mientras Live está activo, se desactiva automáticamente el envío en vivo antes de cambiar de vista.

**Vista Setup** — Muestra los 12 editores de macros para teclas F, el control Delay: y el interruptor QSK. Edite el texto de las macros aquí y configure las opciones de temporización del manipulador. Al abrir la vista Setup siempre se desactiva el envío en vivo.

**Atajos F1–F12** — Cuando el segmento TX está en modo CW o CWL, al presionar F1 a F12 en el teclado se envía la macro correspondiente de inmediato, independientemente de la vista que se muestre actualmente, e incluso si el panel de CWX está oculto. Estos atajos son habilitados por MainWindow según el modo del segmento TX, manteniéndolos mutuamente excluyentes con otros paneles que usan las mismas teclas (como el panel DVK) para evitar ambigüedades en los atajos de Qt.

**Escape** — Al presionar Escape se aborta la transmisión CW actual y se limpia el búfer de envío. Cuando se aborta una transmisión, la parte no enviada del búfer aparece con un efecto tachado en la burbuja del historial. Esto solo funciona cuando los atajos de CWX están activos.

## Qué hace cada control

| Control | Descripción | Configuración persistente |
|---|---|---|
| Send | Envía el búfer escrito si Live está desactivado. Si Live está activo, desactiva el envío en vivo y cambia a la vista send sin retransmitir los caracteres ya manipulados. | — |
| Live | Botón de conmutación. Activa el envío en vivo carácter por carácter cuando está activo; lo desactiva cuando está inactivo. El estado del botón se mantiene sincronizado con el modelo de la radio. | — |
| Setup | Cambia a la vista del editor de macros y configuración de QSK. Desactiva el envío en vivo si está activo. | — |
| Speed: | Velocidad de envío CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envío | Pantalla desplazable de búferes de envío anteriores con resaltado por carácter. Haga clic derecho en una burbuja para reenviar ese texto o borrar todo el historial. Solo lectura. | — |
| Área de texto de envío | Campo de entrada de texto. Presione Enter para enviar el búfer escrito. | — |
| F1 … F12 (botones de macro) | Envía la macro almacenada para esa tecla de función. Activo mediante atajo de teclado cuando el segmento TX está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macros F1 … F12 | Campos de texto en la vista Setup para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Delay: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Activa el QSK de ruptura total cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra atajos de caracteres para prosignos CW comunes (=, +, (, &, $). | — |

## Consejos

- Al presionar Escape durante una transmisión de macro se limpia el búfer de inmediato. Debido a que el estado del manipulador alterna rápidamente entre puntos y rayas, Escape se activa incondicionalmente en lugar de esperar un estado de transmisión específico, por lo que detiene el envío de manera confiable.
- Cuando se aborta una transmisión con Escape, la burbuja del historial para esa transmisión muestra los caracteres ya enviados normalmente y la parte no enviada con un efecto tachado. El límite del tachado coincide exactamente con la cantidad de caracteres enviados antes del aborto.
- Los atajos de teclado F1–F12 se activan siempre que el segmento TX esté en modo CW o CWL, independientemente de si el panel de CWX está visible. Esto le permite activar macros mientras opera otros paneles. Los atajos se desactivan automáticamente cuando cambia el segmento TX a un modo que no sea CW.
- Haga clic derecho en cualquier burbuja del historial para reenviar su contenido, o para borrar todo el historial de envíos de una vez.
- Si cambia a la vista Setup o hace clic en Send mientras Live está activo, el envío en vivo se desactiva automáticamente. No retransmitirá accidentalmente caracteres que el manipulador ya haya enviado.
- El estado del botón Live refleja directamente el modelo de la radio. Si el modelo informa que el envío en vivo está activo cuando el panel se carga por primera vez, el botón Live ya aparecerá presionado.
- El botón Send está marcado para indicar que activa el transmisor, distinguiéndolo de otros controles relacionados con la transmisión en la interfaz.

## Relacionados

- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar el QSK de ruptura total](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
- Reenviar un búfer CW anterior
- Borrar el historial de envío CW
