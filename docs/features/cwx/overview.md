# Resumen de CWX

CWX es el interfaz de manipulador CW integrado de AetherSDR. Permite enviar texto escrito o macros predefinidas a través del manipulador de la FLEX-8600, controlar la velocidad de envío, configurar el retardo entre macros, activar el QSK full break-in y gestionar el historial de envíos, todo ello sin salir de la aplicación.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. CWX requiere una conexión activa con la radio.
- Configure el slice activo en modo CW, CWL o CWU. El panel de CWX aparece en el área central de la ventana principal cuando hay un slice en modo CW activo.

## Cómo funciona

CWX presenta tres vistas, seleccionadas mediante los botones en la parte inferior del panel: Enviar, Directo y Configuración. El control giratorio Velocidad: y los botones selectores de vista están siempre visibles, independientemente de la vista activa.

**Vista Enviar** — Muestra un historial desplazable de búferes enviados previamente, representados como burbujas de chat, con un área de entrada de texto en la parte inferior. Escriba su mensaje y presione Enter para enviarlo. Los caracteres se resaltan en el historial a medida que se transmiten. Si Directo está activo, al hacer clic en Enviar primero se desactiva el envío directo sin retransmitir ningún texto que ya se haya manipulado carácter por carácter. Si Directo ya está desactivado, al hacer clic en Enviar se envía el búfer inmediatamente. Haga clic derecho en cualquier burbuja del historial para reenviar ese texto o borrar todo el historial.

**Vista Directo** — Activa o desactiva el envío directo carácter por carácter. Cuando Directo está habilitado, cada carácter que escribe se manipula inmediatamente, en lugar de mantenerse en espera hasta que presione Enter. Al hacer clic en Configuración o Enviar mientras Directo está activo, el envío directo se desactiva automáticamente antes de cambiar de vista.

**Vista Configuración** — Muestra los 12 editores de macros de las teclas F, el control Retardo: y el conmutador QSK. Edite el texto de las macros aquí y configure las opciones de temporización del manipulador. Al abrir la vista Configuración siempre se desactiva el envío directo.

**Atajos F1–F12** — Cuando el slice activo está en modo CW o CWL, al presionar F1 a F12 en el teclado se envía la macro correspondiente de inmediato, independientemente de la vista que se muestre actualmente, e incluso si el panel de CWX está oculto. Estos atajos son habilitados por MainWindow según el modo del slice activo, manteniéndolos mutuamente excluyentes con otros paneles que usan las mismas teclas (como el panel DVK) para evitar ambigüedades de atajos en Qt.

**Escape** — Al presionar Escape se aborta la transmisión CW actual y se limpia el búfer de envío. Cuando se aborta una transmisión, la parte no enviada del búfer aparece con un efecto de tachado en la burbuja del historial. Esto funciona solo cuando los atajos de CWX están activos.

## Qué hace cada control

| Control | Descripción | Ajuste guardado |
|---|---|---|
| Enviar | Envía el búfer escrito si Directo está desactivado. Si Directo está activo, desactiva el envío directo y cambia a la vista Enviar sin retransmitir los caracteres ya manipulados. | — |
| Directo | Botón de conmutación. Activa el envío directo carácter por carácter cuando está activo; lo desactiva cuando no lo está. El estado del botón se mantiene sincronizado con el modelo de la radio. | — |
| Configuración | Cambia al editor de macros y a la vista de configuración de QSK. Desactiva el envío directo si está activo. | — |
| Velocidad: | Velocidad de envío CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Desplazamiento del historial de envíos | Visualización desplazable de los búferes de envío anteriores con resaltado por carácter. Haga clic derecho en una burbuja para reenviar ese texto o borrar todo el historial. Solo lectura. | — |
| Área de texto de envío | Campo de entrada de texto. Presione Enter para enviar el búfer escrito. | — |
| F1 … F12 (botones de macro) | Envía la macro almacenada para esa tecla de función. Activo mediante atajo de teclado cuando el slice está en modo CW o CWL. | `CwxMacro_F1` – `CwxMacro_F12` |
| Editores de macro F1 … F12 | Campos de texto en la vista Configuración para escribir o editar cada cadena de macro. | `CwxMacro_F1` – `CwxMacro_F12` |
| Retardo: | Retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. | `CwxDelay` |
| QSK | Activa el QSK full break-in cuando está marcado. | `CwxQsk` |
| Leyenda de prosignos | Referencia de solo lectura que muestra los atajos de caracteres para prosignos CW comunes (=, +, (, &, $). | — |

## Consejos

- Al presionar Escape durante una transmisión de macro, el búfer se limpia inmediatamente. Debido a que el estado del manipulador alterna rápidamente entre dits y dahs, Escape se dispara de forma incondicional en lugar de esperar un estado de transmisión específico, por lo que detiene el envío de manera confiable.
- Cuando se aborta una transmisión con Escape, la burbuja del historial para esa transmisión muestra los caracteres ya enviados normalmente y la parte no enviada con un efecto de tachado. El límite del tachado coincide exactamente con la cantidad de caracteres enviados antes del aborto.
- Los atajos de teclado F1–F12 se disparan siempre que el slice activo esté en modo CW o CWL, independientemente de si el panel de CWX está visible. Esto le permite activar macros mientras opera otros paneles. Los atajos se desactivan automáticamente cuando cambia el slice a un modo que no sea CW.
- Haga clic derecho en cualquier burbuja del historial para reenviar su contenido o para borrar todo el historial de envíos de una sola vez.
- Si cambia a la vista Configuración o hace clic en Enviar mientras Directo está activo, el envío directo se desactiva automáticamente. No retransmitirá accidentalmente caracteres que el manipulador ya haya enviado.
- El estado del botón Directo refleja directamente el modelo de la radio. Si el modelo informa que el envío directo está activo cuando el panel se carga por primera vez, el botón Directo ya aparecerá presionado.

## Relacionado

- [Enviar un búfer CW escrito en directo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar el QSK full break-in](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
- Reenviar un búfer CW anterior
- Limpiar el historial de envíos CW
