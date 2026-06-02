# Enviar un búfer de CW escrito en vivo

Use el panel CWX para escribir un mensaje en CW y transmitirlo de inmediato. Es la forma más rápida de enviar texto CW libre sin escribir previamente una macro.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa a la radio.
- Configure el segmento activo en modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando un segmento en modo CW está activo.

## Pasos

1. En el panel CWX, asegúrese de que **Live** esté desactivado. Si **Live** está activo (botón marcado), haga clic en él para desactivarlo antes de escribir un mensaje almacenado en búfer.
2. Haga clic dentro del **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignas que se muestra en el panel para conocer los atajos de prosignas (=, +, (, &, $).
4. Haga clic en **Send** o presione **Enter** para transmitir el búfer. La radio comienza a enviar de inmediato.
5. Para abortar la transmisión en cualquier momento, presione **Escape**. Esto limpia el búfer y detiene el envío. Cuando se aborta, la burbuja del historial muestra los caracteres enviados en texto normal y los caracteres no enviados con formato tachado.

Después de la transmisión, el texto enviado aparece en el área **Send history scroll** sobre el campo de texto como una burbuja con marca de tiempo.

## Reenviar o borrar el historial

Haga clic derecho en cualquier burbuja del historial para abrir un menú contextual con dos opciones:

- **Resend** — Transmite el mismo texto nuevamente. El texto aparece como una nueva burbuja con marca de tiempo en el historial.
- **Clear History** — Elimina todas las burbujas del historial del área de desplazamiento.

## Cómo se comporta Send según el modo Live

El botón **Send** se comporta de manera diferente dependiendo de si **Live** está activo en ese momento:

- **Live está desactivado** — Al hacer clic en **Send** se envía el contenido del campo de texto como un búfer y se transmite.
- **Live está activo** — Al hacer clic en **Send** primero se desactiva **Live** y se devuelve el panel a la vista de envío. El búfer *no* se retransmite; esto evita que el texto que ya se introdujo carácter por carácter en modo live se envíe una segunda vez. Después de hacer clic en **Send** en este estado, escriba su mensaje y haga clic en **Send** nuevamente para transmitir.

## Indicadores visuales de transmisión abortada

Cuando presiona **Escape** durante la transmisión, la burbuja del historial muestra qué caracteres se enviaron y cuáles no:

- **Caracteres enviados** — Aparecen en texto normal.
- **Caracteres no enviados** — Aparecen con formato tachado (tachados). Esto proporciona retroalimentación visual clara sobre exactamente qué se transmitió y qué se abortó.

El formato tachado funciona correctamente para mensajes de una sola línea (indicativos, RST, números de serie). Para mensajes de varias líneas ajustados, el tachado puede no alinearse perfectamente en las líneas de continuación.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| **Send** (vista) | Muestra el área de envío en vivo con el historial y el campo de texto. | — |
| **Live** (vista) | Muestra la vista de envío en vivo. | — |
| **Setup** (vista) | Muestra el editor de macros y la configuración de QSK. | — |
| **Speed:** | Establece la velocidad de envío CW en WPM. | `CwxSpeedWpm` |
| Send text area | Escriba su mensaje CW aquí. Presione Enter para enviar. | — |
| Send history scroll | Muestra los búferes enviados anteriormente con resaltado de caracteres. Solo lectura. Haga clic derecho en una burbuja para Reenviar o Borrar historial. | — |
| **F1 … F12** (macros) | Envía la macro preescrita para esa tecla de función. | `CwxMacro_F1..F12` |
| **F1 … F12** editores de macros | Editores de la vista Setup para cada macro. | `CwxMacro_F1..F12` |
| **Delay:** | Establece el retardo entre macros en milisegundos. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Habilita QSK (full break-in). Disponible en la vista Setup. | `CwxQsk` |
| Prosigns legend | Muestra atajos de caracteres para prosignas CW comunes (=, +, (, &, $). Solo lectura. | — |

## Atajos de teclado

Los atajos F1–F12 y Escape se activan cuando un segmento en modo CW está activo, independientemente de si el panel CWX está visible. Esto le permite activar macros incluso cuando otro panel tiene el foco.

- **F1–F12** — Envía la macro preescrita para esa tecla de función mientras un segmento en modo CW está activo.
- **Escape** — Limpia el búfer incondicionalmente y aborta cualquier transmisión en curso. En un panel CWX inactivo es una operación inocua, por lo que presionarlo siempre es seguro.

## Consejos

- F1–F12 envían macros preescritas mientras un segmento en modo CW está activo. Consulte [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** limpia el búfer incondicionalmente. En un panel CWX inactivo es una operación inocua, por lo que presionarlo siempre es seguro.
- Ajuste **Speed:** en la barra inferior sin cambiar de vista. El control giratorio es visible tanto en la vista de envío como en la de configuración.
- Cuando se reconecta a una radio, el botón **Live** refleja automáticamente el estado live actual de la radio.
- Haga clic derecho en una burbuja del historial para reenviar texto pasado o borrar todo el historial.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el segmento activo esté configurado en modo CW, CWL o CWU. El panel requiere un segmento en modo CW y una conexión activa a la radio.
- **Al hacer clic en Send no se transmite** — Si **Live** estaba activo, el primer clic en **Send** solo desactiva **Live**. Haga clic en **Send** una segunda vez (o presione **Enter**) para transmitir el búfer.
- **Presionar Enter no hace nada** — Haga clic dentro del área de texto de envío primero para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo de toda la aplicación. Si un diálogo o widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.
- **Las macros F1–F12 no se activan** — Asegúrese de que el segmento activo esté en modo CW, CWL o CWU. Los atajos están controlados por el modo del segmento activo, no por la visibilidad del panel.
- **La burbuja abortada no muestra tachado** — Verifique que presionó Escape durante la transmisión activa. El tachado solo aparece para el texto que aún no se había enviado cuando ocurrió el aborto.

## Relacionados

- [CWX overview](overview.md)
- [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Edit a CW macro string](edit-a-cw-macro-string.md)
- [Change CW send speed in WPM](change-cw-send-speed-in-wpm.md)
- [Enable QSK full break-in](enable-qsk-full-break-in.md)
- [Look up the prosign character shortcuts](look-up-the-prosign-character-shortcuts.md)
