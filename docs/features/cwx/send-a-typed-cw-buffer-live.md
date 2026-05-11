# Enviar un búfer de CW escrito en vivo

Use el panel CWX para escribir un mensaje en CW y transmitirlo de inmediato. Es la forma más rápida de enviar CW de texto libre sin escribir previamente una macro.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa con la radio.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando hay un slice en modo CW activo.

## Pasos

1. En el panel CWX, asegúrese de que **Live** esté desactivado. Si **Live** está activo (botón marcado), haga clic en él para desactivarlo antes de escribir un mensaje en el búfer.
2. Haga clic dentro del **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignos que se muestra en el panel para obtener los atajos de prosignos (=, +, (, &, $).
4. Haga clic en **Send** o presione **Enter** para transmitir el búfer. La radio comienza a enviar inmediatamente.
5. Para abortar la transmisión en cualquier momento, presione **Escape**. Esto vacía el búfer y detiene el envío.

Después de la transmisión, el texto enviado aparece en el **Send history scroll** sobre el campo de texto como una burbuja con marca de tiempo.

## Cómo se comporta Send según el modo Live

El botón **Send** se comporta de manera diferente según si **Live** está activo actualmente:

- **Live está desactivado** — Al hacer clic en **Send** se envía el contenido del campo de texto como búfer y se transmite.
- **Live está activo** — Al hacer clic en **Send** primero se desactiva **Live** y se devuelve el panel a la vista de envío. El búfer *no* se retransmite; esto evita que el texto que ya fue tecleado carácter por carácter en modo live se envíe una segunda vez. Después de hacer clic en **Send** en este estado, escriba su mensaje y haga clic en **Send** nuevamente para transmitir.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| **Send** (vista) | Muestra el área de envío en vivo con historial y campo de texto. | — |
| **Live** (vista) | Muestra la vista de envío en vivo. | — |
| **Setup** (vista) | Muestra el editor de macros y la configuración de QSK. | — |
| **Speed:** | Establece la velocidad de envío de CW en WPM. | `CwxSpeedWpm` |
| Send text area | Escriba aquí su mensaje de CW. Presione Enter para enviar. | — |
| Send history scroll | Muestra los búferes enviados previamente con resaltado de caracteres. Solo lectura. | — |
| **F1 … F12** (macros) | Envía la macro preescrita para esa tecla de función. | `CwxMacro_F1..F12` |
| **F1 … F12** editores de macro | Editores de la vista Setup para cada macro. | `CwxMacro_F1..F12` |
| **Delay:** | Establece el retardo entre macros en milisegundos. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Activa QSK (full break-in). Disponible en la vista Setup. | `CwxQsk` |
| Leyenda de prosignos | Muestra atajos de caracteres para prosignos comunes de CW (=, +, (, &, $). Solo lectura. | — |

## Atajos de teclado

Los atajos F1–F12 y Escape solo están activos mientras el panel CWX está visible. Esto evita ambigüedades con otros paneles que puedan registrar las mismas teclas (como el panel Digital Voice Keyboard). Cuando cambie a otro panel en el divisor, los atajos de CWX se deshabilitan automáticamente.

- **F1–F12** — Envía la macro preescrita para esa tecla de función mientras un slice en modo CW está activo.
- **Escape** — Vacía el búfer de forma incondicional. En un panel CWX inactivo es una operación inofensiva, por lo que presionarlo siempre es seguro.

## Consejos

- F1–F12 envían macros preescritas mientras un slice en modo CW está activo. Consulte [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** vacía el búfer de forma incondicional. En un panel CWX inactivo es una operación inofensiva, por lo que presionarlo siempre es seguro.
- Ajuste **Speed:** en la barra inferior sin cambiar de vistas. El control numérico es visible tanto en la vista de envío como en la de configuración.
- Cuando se reconecta a una radio, el botón **Live** refleja automáticamente el estado live actual de la radio.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo esté configurado en modo CW, CWL o CWU. El panel requiere un slice en modo CW y una conexión de radio activa.
- **Hacer clic en Send no transmite** — Si **Live** estaba activo, el primer clic en **Send** solo desactiva **Live**. Haga clic en **Send** una segunda vez (o presione **Enter**) para transmitir el búfer.
- **Presionar Enter no hace nada** — Haga clic primero dentro del Send text area para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo de toda la aplicación. Si un cuadro de diálogo o widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.
- **Las macros F1–F12 no se activan** — Asegúrese de que la pestaña del panel CWX esté seleccionada activamente en el divisor. Los atajos se deshabilitan cuando el panel está oculto.

## Relacionados

- [CWX overview](overview.md)
- [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Edit a CW macro string](edit-a-cw-macro-string.md)
- [Change CW send speed in WPM](change-cw-send-speed-in-wpm.md)
- [Enable QSK full break-in](enable-qsk-full-break-in.md)
- [Look up the prosign character shortcuts](look-up-the-prosign-character-shortcuts.md)
