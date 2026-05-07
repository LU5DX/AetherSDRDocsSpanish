# Envíe un búfer de CW escrito en vivo

Utilice el panel CWX para escribir un mensaje en CW y transmitirlo de inmediato. Es la forma más rápida de enviar texto libre en CW sin tener que escribir un macro previamente.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa con la radio.
- Ajuste el slice activo al modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando un slice en modo CW está activo.

## Pasos

1. En el panel CWX, asegúrese de que **Live** esté desactivado. Si **Live** está activo (botón marcado), haga clic en él para desactivarlo antes de escribir un mensaje en búfer.
2. Haga clic dentro del área **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignos que se muestra en el panel para conocer los atajos de prosignos (=, +, (, &, $).
4. Haga clic en **Send** o presione **Enter** para transmitir el búfer. La radio comienza a enviar de inmediato.
5. Para abortar la transmisión en cualquier momento, presione **Escape**. Esto borra el búfer y detiene el envío.

Después de la transmisión, el texto enviado aparece en el área **Send history scroll** sobre el campo de texto como una burbuja con marca de tiempo.

## Cómo se comporta Send según el modo Live

El botón **Send** se comporta de manera diferente dependiendo de si **Live** está activo:

- **Live está desactivado** — Al hacer clic en **Send** se envía el contenido del campo de texto como un búfer y se transmite.
- **Live está activo** — Al hacer clic en **Send**, primero se desactiva **Live** y se devuelve el panel a la vista de envío. El búfer *no* se retransmite; esto evita que el texto que ya se escribió carácter por carácter en modo en vivo se envíe una segunda vez. Después de hacer clic en **Send** en este estado, escriba su mensaje y haga clic en **Send** nuevamente para transmitir.

## Función de cada control

| Control | Función | Clave de configuración |
|---|---|---|
| **Send** | Envía el búfer escrito para transmisión cuando **Live** está desactivado. Si **Live** está activo, desactiva **Live** y vuelve a la vista de envío sin retransmitir. | — |
| **Live** | Activa o desactiva el modo de envío en vivo. Mientras está activo, los caracteres se pulsan a medida que los escribe. Activar **Live** también deselecciona **Setup** y muestra la vista de envío. | — |
| **Setup** | Cambia al editor de macros y a la vista de configuración de QSK. Activar **Setup** también desactiva **Live**. | — |
| **Speed:** | Establece la velocidad de envío de CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Send text area | Escriba aquí su mensaje CW. Presione Enter para enviar. | — |
| Send history scroll | Muestra los búferes enviados anteriormente con marcas de tiempo. Solo lectura. | — |
| **Delay:** | Establece el retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Activa QSK (break-in completo). Disponible en la vista Setup. | `CwxQsk` |
| Prosigns legend | Muestra atajos de caracteres para prosignos comunes de CW. Solo lectura. | — |

## Consejos

- F1–F12 envían macros preescritos mientras un slice en modo CW está activo. Los atajos de teclado funcionan en toda la aplicación en modos CW y CWL. Consulte [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** borra el búfer de forma incondicional. En un panel CWX inactivo no tiene efecto, por lo que siempre es seguro presionarlo.
- Ajuste **Speed:** en la barra inferior sin cambiar de vista. El control giratorio es visible tanto en la vista de envío como en la de configuración.
- Cuando se reconecte a una radio, el botón **Live** refleja automáticamente el estado en vivo actual de la radio.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo esté configurado en modo CW, CWL o CWU. El panel requiere un slice en modo CW y una conexión activa con la radio.
- **Al hacer clic en Send no se transmite** — Si **Live** estaba activo, el primer clic en **Send** solo desactiva **Live**. Haga clic en **Send** una segunda vez (o presione **Enter**) para transmitir el búfer.
- **Presionar Enter no hace nada** — Haga clic primero dentro del área Send text area para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo en toda la aplicación. Si un cuadro de diálogo o un widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.

## Relacionados

- [CWX overview](overview.md)
- [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Edit a CW macro string](edit-a-cw-macro-string.md)
- [Change CW send speed in WPM](change-cw-send-speed-in-wpm.md)
- [Enable QSK full break-in](enable-qsk-full-break-in.md)
- [Look up the prosign character shortcuts](look-up-the-prosign-character-shortcuts.md)
