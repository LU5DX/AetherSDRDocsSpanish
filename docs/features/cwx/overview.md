# Resumen de CWX

CWX es la interfaz de manipulador CW integrada de AetherSDR. Permite enviar texto escrito o macros predefinidas a través del manipulador de la FLEX-8600, controlar la velocidad de envío, definir el retardo entre macros y activar QSK de inserción total, todo sin salir de la aplicación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión activa con la radio.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en el área central de la ventana principal cuando hay un slice en modo CW activo.

## Cómo funciona

CWX presenta tres vistas, seleccionables mediante los botones en la parte inferior del panel: Send, Live y Setup. El control giratorio Speed: y los botones de selección de vista están siempre visibles, sin importar qué vista esté activa.

**Vista Send:** muestra un historial desplazable de búferes enviados anteriormente, representados como burbujas de chat, con un área de entrada de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten. Si Live está activo, al hacer clic en Send primero se desactiva el envío en vivo sin retransmitir ningún texto que ya se haya manipulado carácter por carácter. Si Live ya está desactivado, al hacer clic en Send se envía el búfer de inmediato.

**Vista Live:** alterna el envío en vivo carácter por carácter. Cuando Live está activado, cada carácter que escribe se manipula de inmediato, sin esperar a que presione Enter. Al hacer clic en Setup o Send mientras Live está activo, el envío en vivo se desactiva automáticamente antes de cambiar de vista.

**Vista Setup:** muestra los 12 editores de macros para las teclas F, el control Delay: y el conmutador QSK. Edite el texto de las macros aquí y configure las opciones de temporización del manipulador. Abrir la vista Setup siempre desactiva el envío en vivo.

**Atajos F1–F12:** cuando el slice activo está en modo CW o CWL, al presionar F1 a F12 en el teclado se envía la macro correspondiente de inmediato, sin importar qué vista se muestre. Estos atajos solo están activos mientras el panel CWX está visible. Si cambia a otro panel que también use F1–F12 (como el panel DVK), los atajos de CWX se desactivan automáticamente para evitar conflictos.

**Escape:** Presionar Escape cancela la transmisión CW actual y limpia el búfer de envío. Esto solo funciona cuando el panel CWX está visible.

## Qué hace cada control

| Control | Descripción | Ajuste persistente |
|---|---|---|
| Send | Envía el búfer escrito si Live está desactivado. Si Live está activo, desactiva el envío en vivo y cambia a la vista de envío sin retransmitir los caracteres ya manipulados. | — |
| Live | Botón de alternancia. Activa el envío en vivo carácter por carácter cuando está encendido; lo desactiva cuando está apagado. El estado del botón se mantiene sincronizado con el modelo de la radio. | — |
| Setup | Cambia al editor de macros y a la vista de configuración de QSK. Desactiva el envío en vivo si está activo. | — |
| Speed: | Velocidad de envío CW en PPM. Rango: 5–100 PPM. Valor predeterminado: 20 PPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envío | Visualización desplazable de los búferes de envío anteriores con resaltado por carácter. Solo lectura. | — |
| Área de texto de envío | Campo de entrada de texto. Presione Enter para enviar el búfer escrito. | — |
| F1 … F12 (botones de macro) | Envía la macro almacenada para esa tecla de función. Activo mediante atajo de teclado cuando el panel CWX está visible y el slice está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macros F1 … F12 | Campos de texto en la vista Setup para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Delay: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Activa QSK de inserción total cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra los atajos de caracteres para prosignos CW comunes (=, +, (, &, $). | — |

## Consejos

- Presionar Escape durante una transmisión de macro limpia el búfer de inmediato. Debido a que el estado del manipulador alterna rápidamente entre ditos y dahs, Escape se dispara de forma incondicional sin esperar un estado de transmisión específico, por lo que detiene el envío de manera confiable.
- Los atajos de teclado F1–F12 solo se activan cuando el panel CWX está visible y el slice activo está en modo CW o CWL. Cambiar el slice a un modo que no sea CW, u ocultar el panel CWX (por ejemplo, al abrir el panel DVK), los desactiva automáticamente.
- Si cambia a la vista Setup o hace clic en Send mientras Live está activo, el envío en vivo se desactiva automáticamente. No retransmitirá accidentalmente caracteres que el manipulador ya haya enviado.
- El estado del botón Live refleja directamente el modelo de la radio. Si el modelo informa que el envío en vivo está activo cuando el panel se carga por primera vez, el botón Live ya aparecerá presionado.

## Relacionados

- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en PPM](change-cw-send-speed-in-wpm.md)
- [Activar QSK de inserción total](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
