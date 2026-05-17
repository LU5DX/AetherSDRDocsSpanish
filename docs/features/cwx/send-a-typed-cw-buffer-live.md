# Envío en vivo de un búfer de CW escrito

Use el panel CWX para escribir un mensaje en CW y transmitirlo de inmediato. Es la forma más rápida de enviar CW de texto libre sin tener que escribir una macro previamente.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa a la radio.
- Ajuste el slice activo al modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando hay un slice en modo CW activo.

## Pasos

1. En el panel CWX, asegúrese de que **Live** esté desactivado. Si **Live** está activo (botón marcado), haga clic en él para desactivarlo antes de escribir un mensaje almacenado en búfer.
2. Haga clic dentro del área **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignos que se muestra en el panel para conocer los atajos de prosignos (=, +, (, &, $).
4. Haga clic en **Send** o presione **Enter** para transmitir el búfer. La radio comienza a enviar inmediatamente.
5. Para abortar la transmisión en cualquier momento, presione **Escape**. Esto elimina el contenido del búfer y detiene el envío.

Después de la transmisión, el texto enviado aparece en el área **Send history scroll** sobre el campo de texto como una burbuja con marca de tiempo.

## Reenviar o borrar el historial

Haga clic derecho en cualquier burbuja del historial para abrir un menú contextual con dos opciones:

- **Resend** — Transmite el mismo texto nuevamente. El texto aparece como una nueva burbuja con marca de tiempo en el historial.
- **Clear History** — Elimina todas las burbujas del historial del área de desplazamiento.

## Comportamiento de Send según el modo Live

El botón **Send** se comporta de manera diferente según si **Live** está actualmente activado:

- **Live desactivado** — Al hacer clic en **Send** se envía el contenido del campo de texto como un búfer y se transmite.
- **Live activado** — Al hacer clic en **Send** primero se desactiva **Live** y se devuelve el panel a la vista de envío. El búfer *no* se retransmite; esto evita que el texto que ya fue ingresado carácter por carácter en modo en vivo se envíe una segunda vez. Después de hacer clic en **Send** en este estado, escriba su mensaje y haga clic en **Send** nuevamente para transmitir.

## Función de cada control

| Control | Función | Clave de configuración |
|---|---|---|
| **Send** (vista) | Muestra el área de envío en vivo con historial y campo de texto. | — |
| **Live** (vista) | Muestra la vista de envío en vivo. | — |
| **Setup** (vista) | Muestra el editor de macros y la configuración de QSK. | — |
| **Speed:** | Establece la velocidad de envío CW en WPM. | `CwxSpeedWpm` |
| Send text area | Escriba aquí su mensaje CW. Presione Enter para enviar. | — |
| Send history scroll | Muestra los búferes enviados previamente con resaltado de caracteres. Solo lectura. Haga clic derecho en una burbuja para Reenviar o Borrar historial. | — |
| **F1 … F12** (macros) | Envía la macro preescrita para esa tecla de función. | `CwxMacro_F1..F12` |
| **F1 … F12** editores de macros | Editores de la vista Setup para cada macro. | `CwxMacro_F1..F12` |
| **Delay:** | Establece el retardo entre macros en milisegundos. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Activa QSK (full break-in). Disponible en la vista Setup. | `CwxQsk` |
| Prosigns legend | Muestra atajos de caracteres para prosignos CW comunes (=, +, (, &, $). Solo lectura. | — |

## Atajos de teclado

Los atajos F1–F12 y Escape se activan cuando hay un slice en modo CW activo, independientemente de si el panel CWX está visible. Esto permite activar macros incluso cuando otro panel tiene el foco.

- **F1–F12** — Envían la macro preescrita para esa tecla de función mientras un slice en modo CW está activo.
- **Escape** — Elimina el búfer de forma incondicional. En un panel CWX inactivo no tiene efecto, por lo que presionarlo siempre es seguro.

## Consejos

- F1–F12 envían macros preescritas mientras un slice en modo CW está activo. Consulte [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** elimina el búfer de forma incondicional. En un panel CWX inactivo no tiene efecto, por lo que presionarlo siempre es seguro.
- Ajuste **Speed:** en la barra inferior sin cambiar de vista. El control giratorio es visible tanto en la vista de envío como en la de configuración.
- Cuando se reconecte a una radio, el botón **Live** refleja automáticamente el estado en vivo actual de la radio.
- Haga clic derecho en una burbuja del historial para reenviar texto anterior o borrar todo el historial.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo esté configurado en modo CW, CWL o CWU. El panel requiere un slice en modo CW y una conexión activa a la radio.
- **Al hacer clic en Send no se transmite** — Si **Live** estaba activado, el primer clic en **Send** solo desactiva **Live**. Haga clic en **Send** una segunda vez (o presione **Enter**) para transmitir el búfer.
- **Presionar Enter no hace nada** — Haga clic primero dentro del área de texto de envío para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo a nivel de aplicación. Si un cuadro de diálogo o widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.
- **Las macros F1–F12 no se activan** — Asegúrese de que el slice activo esté en modo CW, CWL o CWU. Los atajos están controlados por el modo del slice activo, no por la visibilidad del panel.

## Relacionados

- [CWX overview](overview.md)
- [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Edit a CW macro string](edit-a-cw-macro-string.md)
- [Change CW send speed in WPM](change-cw-send-speed-in-wpm.md)
- [Enable QSK full break-in](enable-qsk-full-break-in.md)
- [Look up the prosign character shortcuts](look-up-the-prosign-character-shortcuts.md)
