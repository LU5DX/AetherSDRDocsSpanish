# Descripción general de CWX

CWX es el interface de manipulador CW integrado de AetherSDR. Le permite enviar texto escrito o macros predefinidas a través del manipulador de la FLEX-8600, controlar la velocidad de transmisión, configurar el retardo entre macros, activar el QSK de inserción total y gestionar el historial de envíos, todo sin salir de la aplicación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión activa con la radio.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en el área central de la ventana principal cuando hay un slice en modo CW activo.

## Cómo funciona

CWX presenta tres vistas, seleccionadas mediante los botones en la parte inferior del panel: Send, Live y Setup. El cuadro giratorio Speed: y los botones selectores de vista son siempre visibles independientemente de la vista activa.

**Vista Send** — Muestra un historial desplazable de búferes enviados previamente en forma de burbujas de chat, con un área de entrada de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten. Si Live está actualmente activado, al hacer clic en Send primero se desactiva el envío en vivo sin retransmitir ningún texto que ya se haya tecleado carácter por carácter. Si Live ya está desactivado, al hacer clic en Send se envía el búfer inmediatamente. Haga clic derecho en cualquier burbuja del historial para reenviar ese texto o borrar todo el historial.

**Vista Live** — Activa o desactiva el envío en vivo carácter por carácter. Cuando Live está habilitado, cada carácter que escribe se envía inmediatamente, en lugar de retenerse hasta que presione Enter. Al hacer clic en Setup o Send mientras Live está activo, se desactiva automáticamente el envío en vivo antes de cambiar de vista.

**Vista Setup** — Muestra los 12 editores de macros de las teclas F, el control Delay: y el conmutador QSK. Edite el texto de las macros aquí y configure las opciones de temporización del manipulador. Al abrir la vista Setup siempre se desactiva el envío en vivo.

**Atajos F1–F12** — Cuando el slice activo está en modo CW o CWL, al presionar F1 a F12 en el teclado se envía la macro correspondiente inmediatamente, independientemente de la vista mostrada en ese momento, incluso si el panel CWX está oculto. Estos atajos son habilitados por la MainWindow según el modo del slice activo, manteniéndolos mutuamente excluyentes con otros paneles que usan las mismas teclas (como el panel DVK) para evitar ambigüedades con los atajos de Qt.

**Escape** — Al presionar Escape se aborta la transmisión CW actual y se limpia el búfer de envío. Esto solo funciona cuando los atajos de CWX están activos.

## Qué hace cada control

| Control | Descripción | Ajuste persistente |
|---|---|---|
| Send | Envía el búfer escrito si Live está desactivado. Si Live está activado, desactiva el envío en vivo y cambia a la vista de envío sin retransmitir los caracteres ya tecleados. | — |
| Live | Botón de conmutación. Activa el envío en vivo carácter por carácter cuando está encendido; lo desactiva cuando está apagado. El estado del botón se mantiene sincronizado con el modelo de la radio. | — |
| Setup | Cambia al editor de macros y a la vista de configuración de QSK. Desactiva el envío en vivo si está activo. | — |
| Speed: | Velocidad de envío CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Historial desplazable de envíos | Pantalla desplazable de búferes de envío anteriores con resaltado por carácter. Haga clic derecho en una burbuja para reenviar ese texto o borrar todo el historial. Solo lectura. | — |
| Área de texto de envío | Campo de entrada de texto. Presione Enter para enviar el búfer escrito. | — |
| F1 … F12 (botones de macro) | Envía la macro almacenada para esa tecla de función. Activo mediante atajo de teclado cuando el slice está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macros F1 … F12 | Campos de texto en la vista Setup para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Delay: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Activa el QSK de inserción total cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra los atajos de caracteres para prosignos CW comunes (=, +, (, &, $). | — |

## Consejos

- Al presionar Escape durante una transmisión de macro se limpia el búfer inmediatamente. Debido a que el estado del manipulador alterna rápidamente entre puntos y rayas, Escape se activa incondicionalmente sin esperar un estado de transmisión específico, por lo que detiene el envío de manera confiable.
- Los atajos de teclado F1–F12 se activan siempre que el slice activo esté en modo CW o CWL, independientemente de si el panel CWX está visible. Esto le permite activar macros mientras opera otros paneles. Los atajos se desactivan automáticamente cuando cambia el slice a un modo que no sea CW.
- Haga clic derecho en cualquier burbuja del historial para reenviar su contenido o para borrar todo el historial de envíos de una vez.
- Si cambia a la vista Setup o hace clic en Send mientras Live está activo, el envío en vivo se desactiva automáticamente. No retransmitirá accidentalmente caracteres que el manipulador ya haya enviado.
- El estado del botón Live refleja directamente el modelo de la radio. Si el modelo informa que el envío en vivo está activo cuando el panel se carga por primera vez, el botón Live ya aparecerá presionado.

## Relacionado

- [Send a typed CW buffer live](send-a-typed-cw-buffer-live.md)
- [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Edit a CW macro string](edit-a-cw-macro-string.md)
- [Change CW send speed in WPM](change-cw-send-speed-in-wpm.md)
- [Enable QSK full break-in](enable-qsk-full-break-in.md)
- [Look up the prosign character shortcuts](look-up-the-prosign-character-shortcuts.md)
- [Resend a previous CW buffer](resend-a-previous-cw-buffer.md)
- [Clear CW send history](clear-cw-send-history.md)
