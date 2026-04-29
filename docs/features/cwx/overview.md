# Descripción general de CWX

CWX es la interfaz de manipulador CW integrada en AetherSDR. Permite enviar texto escrito o macros predefinidos a través del manipulador del FLEX-8600, controlar la velocidad de envío, establecer el retardo entre macros y habilitar el QSK de ruptura total, todo sin salir de la aplicación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión de radio activa.
- Configure el slice (receptor parcial) activo en modo CW, CWL o CWU. El panel CWX aparece en el área central de la ventana principal cuando hay un slice en modo CW activo.

## Cómo funciona

CWX presenta tres vistas, seleccionadas mediante los botones en la parte inferior del panel: Send, Live y Setup. El control numérico Speed: y los botones de selección de vista están siempre visibles, independientemente de la vista activa.

**Vista Send** — Muestra un historial desplazable de los buffers enviados anteriormente, representados como burbujas de chat, con un área de entrada de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten. Si Live está activo en ese momento, hacer clic en Send primero desactiva el envío en vivo sin retransmitir los caracteres que ya fueron manipulados uno a uno. Si Live ya está desactivado, hacer clic en Send envía el buffer de inmediato.

**Vista Live** — Activa o desactiva el envío en vivo carácter por carácter. Cuando Live está habilitado, cada carácter que escriba se manipula de inmediato en lugar de retenerse hasta que presione Enter. Al hacer clic en Setup o en Send mientras Live está activo, el envío en vivo se deshabilita automáticamente antes de cambiar de vista.

**Vista Setup** — Muestra los 12 editores de macros de teclas F, el control Delay: y el selector QSK. Edite el texto de los macros aquí y configure las opciones de temporización del manipulador. Abrir la vista Setup siempre desactiva el envío en vivo.

**Atajos F1–F12** — Cuando el slice activo está en modo CW o CWL, presionar F1 a F12 en el teclado envía el macro correspondiente de inmediato, independientemente de la vista que se muestre en ese momento.

**Escape** — Presionar Escape interrumpe la transmisión CW en curso y vacía el buffer de envío. Esto funciona en toda la aplicación siempre que CWX esté activo.

## Función de cada control

| Control | Descripción | Configuración persistida |
|---|---|---|
| Send | Envía el buffer escrito si Live está desactivado. Si Live está activo, desactiva el envío en vivo y cambia a la vista de envío sin retransmitir los caracteres ya manipulados. | — |
| Live | Botón de alternancia. Habilita el envío en vivo carácter por carácter cuando está activo; lo deshabilita cuando está inactivo. El estado del botón se mantiene sincronizado con el modelo de radio. | — |
| Setup | Cambia al editor de macros y a la vista de configuración QSK. Desactiva el envío en vivo si está activo. | — |
| Speed: | Velocidad de envío CW en PPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envío | Pantalla desplazable de los buffers de envío anteriores con resaltado por carácter. Solo lectura. | — |
| Área de texto de envío | Campo de entrada de texto. Presione Enter para enviar el buffer escrito. | — |
| F1 … F12 (botones de macro) | Envía el macro almacenado para esa tecla de función. Se activan mediante atajo de teclado cuando el slice está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macro F1 … F12 | Campos de texto en la vista Setup para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Delay: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Habilita el QSK de ruptura total cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra los atajos de caracteres para los prosignos CW más comunes (=, +, (, &, $). | — |

## Consejos

- Presionar Escape durante la transmisión de un macro vacía el buffer de inmediato. Dado que el estado del manipulador alterna rápidamente entre puntos y rayas, Escape se ejecuta de forma incondicional en lugar de esperar un estado de transmisión específico, por lo que detiene el envío de manera confiable.
- Los atajos de teclado F1–F12 solo se activan cuando el slice activo está en modo CW o CWL. Al cambiar el slice a un modo no CW, se deshabilitan automáticamente.
- Si cambia a la vista Setup o hace clic en Send mientras Live está activo, el envío en vivo se desactiva de forma automática. No retransmitirá accidentalmente los caracteres que el manipulador ya haya enviado.
- El estado del botón Live refleja directamente el modelo de radio. Si el modelo indica que el envío en vivo está activo cuando el panel se carga por primera vez, el botón Live ya aparecerá presionado.

## Temas relacionados

- [Enviar un buffer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar un macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en PPM](change-cw-send-speed-in-wpm.md)
- [Habilitar el QSK de ruptura total](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
