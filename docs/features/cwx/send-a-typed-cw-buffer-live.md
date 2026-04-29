# Enviar un búfer de CW escrito en tiempo real

Use el panel CWX para escribir un mensaje en CW y transmitirlo de inmediato. Esta es la forma más rápida de enviar CW de texto libre sin escribir una macro con anticipación.

## Antes de comenzar

- Conéctese a un radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando hay un slice en modo CW activo.

## Pasos

1. En el panel CWX, asegúrese de que **Live** esté desactivado. Si **Live** está activo (botón marcado), haga clic en él para desactivarlo antes de escribir un mensaje en el búfer.
2. Haga clic dentro del **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignos que se muestra en el panel para conocer los atajos de prosignos (=, +, (, &, $).
4. Haga clic en **Send** o presione **Enter** para transmitir el búfer. El radio comienza a enviar de inmediato.
5. Para cancelar la transmisión en cualquier momento, presione **Escape**. Esto borra el búfer y detiene el envío.

Tras la transmisión, el texto enviado aparece en el área **Send history scroll**, sobre el campo de texto, como una burbuja con marca de tiempo.

## Comportamiento de Send según el modo Live

El botón **Send** se comporta de manera diferente según si **Live** está activo o no:

- **Live desactivado** — Al hacer clic en **Send** se envía el contenido del campo de texto como búfer y se transmite.
- **Live activado** — Al hacer clic en **Send** primero se desactiva **Live** y el panel regresa a la vista de envío. El búfer *no* se retransmite; esto evita que el texto que ya fue tecleado carácter por carácter en el modo live se envíe por segunda vez. Después de hacer clic en **Send** en este estado, escriba su mensaje y haga clic en **Send** nuevamente para transmitir.

## Función de cada control

| Control | Función | Clave de configuración |
|---|---|---|
| **Send** | Envía el búfer escrito para su transmisión cuando **Live** está desactivado. Si **Live** está activado, desactiva **Live** y regresa a la vista de envío sin retransmitir. | — |
| **Live** | Activa o desactiva el modo de envío en vivo. Mientras está activado, los caracteres se teclean a medida que se escriben. Al activar **Live** también se deselecciona **Setup** y se muestra la vista de envío. | — |
| **Setup** | Cambia al editor de macros y a la vista de configuración QSK. Al activar **Setup** también se desactiva **Live**. | — |
| **Speed:** | Establece la velocidad de envío de CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Send text area | Escriba aquí su mensaje en CW. Presione Enter para enviar. | — |
| Send history scroll | Muestra los búferes enviados anteriormente con marcas de tiempo. Solo lectura. | — |
| **Delay:** | Establece el retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Habilita QSK (break-in completo). Disponible en la vista Setup. | `CwxQsk` |
| Prosigns legend | Muestra los atajos de caracteres para los prosignos de CW más comunes. Solo lectura. | — |

## Consejos

- F1–F12 envían macros preescritas mientras hay un slice en modo CW activo. Los atajos de teclado funcionan en toda la aplicación en los modos CW y CWL. Consulte [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** borra el búfer de forma incondicional. En un panel CWX inactivo es una operación inocua, por lo que siempre es seguro presionarlo.
- Ajuste **Speed:** en la barra inferior sin cambiar de vista. El control numérico es visible tanto en la vista de envío como en la vista de configuración.
- Al reconectarse a un radio, el botón **Live** refleja automáticamente el estado live actual del radio.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo esté configurado en modo CW, CWL o CWU. El panel requiere un slice en modo CW y una conexión de radio activa.
- **Al hacer clic en Send no se transmite** — Si **Live** estaba activado, el primer clic en **Send** solo desactiva **Live**. Haga clic en **Send** una segunda vez (o presione **Enter**) para transmitir el búfer.
- **Presionar Enter no hace nada** — Haga clic dentro del Send text area primero para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo a nivel de toda la aplicación. Si un diálogo o un widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.

## Relacionados

- [Descripción general de CWX](overview.md)
- [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro de CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío de CW en WPM](change-cw-send-speed-in-wpm.md)
- [Habilitar QSK de break-in completo](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
