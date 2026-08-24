# Enviar un buffer CW escrito en vivo

Use el panel CWX para escribir un mensaje CW y transmitirlo de inmediato. Esta es la forma más rápida de enviar CW de texto libre sin preescribir una macro.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando hay un slice en modo CW activo.
- Establezca el **Speed step** (cuánto cambia la velocidad al presionar **+** o **-**) haciendo clic derecho en el cuadro giratorio **Speed:** y eligiendo un valor de 1 a 20 WPM. El valor predeterminado es 3 WPM. Esta configuración se guarda por panel y persiste entre reinicios.

## Pasos

1. En el panel CWX, asegúrese de que **Live** esté apagado. Si **Live** está activo (botón marcado), haga clic en él para desactivarlo antes de escribir un mensaje en buffer.
2. Haga clic dentro del **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignos que se muestra en el panel para los atajos de prosignos (=, +, (, &, $). Puede insertar modificadores de velocidad: `[20]` establece la velocidad en 20 WPM, `[15]` en 15 WPM, y así sucesivamente. El prefijo del modificador se elimina automáticamente del texto visible en la burbuja.
4. Haga clic en **Send** o presione **Enter** para transmitir el buffer. La radio comienza a enviar inmediatamente.
5. Para abortar la transmisión en cualquier momento, presione **Escape**. Esto limpia el buffer y detiene el envío. Cuando se aborta, la burbuja del historial muestra los caracteres enviados en texto normal y los caracteres no enviados con formato tachado.

Después de la transmisión, el texto enviado aparece en el área de **Send history scroll** sobre el campo de texto como una burbuja con marca de tiempo. La burbuja muestra el texto realmente transmitido con los prefijos de modificador de velocidad eliminados.

## Reenviar o limpiar el historial

Haga clic derecho en cualquier burbuja del historial para abrir un menú contextual con dos opciones:

- **Resend** — Transmite el mismo texto nuevamente. El texto aparece como una nueva burbuja con marca de tiempo en el historial.
- **Clear History** — Elimina todas las burbujas del historial del área de desplazamiento.

## Cómo se comporta Send según el modo Live

El botón **Send** se comporta de manera diferente dependiendo de si **Live** está actualmente activado:

- **Live está apagado** — Al hacer clic en **Send** se envía el contenido del campo de texto como buffer y se transmite.
- **Live está activado** — Al hacer clic en **Send** primero se apaga **Live** y se devuelve el panel a la vista de envío. El buffer *no* se retransmite; esto evita que el texto que ya fue tecleado carácter por carácter en modo live se envíe una segunda vez. Después de hacer clic en **Send** en este estado, escriba su mensaje y haga clic en **Send** nuevamente para transmitir.

## Indicadores visuales de transmisión abortada

Cuando presiona **Escape** durante la transmisión, la burbuja del historial muestra qué caracteres fueron enviados y cuáles no:

- **Caracteres enviados** — Aparecen en texto normal.
- **Caracteres no enviados** — Aparecen con formato tachado (tachados). Esto proporciona una retroalimentación visual clara sobre exactamente qué se transmitió y qué se abortó.

El formato tachado funciona correctamente para mensajes de una sola línea (indicativos, RST, números de serie). Para mensajes multilínea con ajuste de línea, el tachado puede no alinearse perfectamente en las líneas de continuación.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| **Send** (vista) | Muestra el área de envío en vivo con historial y campo de texto. | — |
| **Live** (vista) | Muestra la vista de envío en vivo. | — |
| **Setup** (vista) | Muestra el editor de macros y la configuración de QSK. | — |
| **Speed:** | Establece la velocidad de envío CW en WPM. | `CwxSpeedWpm` |
| **Speed step** (clic derecho en **Speed:**) | Establece cuánto cambia la velocidad al presionar **+** o **-** en WPM. Rango 1-20, predeterminado 3. | `CwxPanel` → `speedStep` (por panel) |
| Send text area | Escriba aquí su mensaje CW. Presione Enter para enviar. | — |
| Send history scroll | Muestra buffers enviados previamente con resaltado de caracteres. Solo lectura. Haga clic derecho en una burbuja para Resend o Clear History. | — |
| **F1 … F12** (macros) | Envía la macro preescrita para esa tecla de función. | `CwxMacro_F1..F12` |
| **F1 … F12** editores de macros | Editores de la vista Setup para cada macro. | `CwxMacro_F1..F12` |
| **Delay:** | Establece el retardo entre macros en milisegundos. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Habilita QSK (full break-in). Disponible en la vista Setup. | `CwxQsk` |
| Leyenda de prosignos | Muestra atajos de caracteres para prosignos de CW comunes (=, +, (, &, $). Solo lectura. | — |

## Atajos de teclado

Los atajos F1–F12 y Escape se activan cuando el slice TX está en modo CW (CW o CWL). Esto le permite activar macros incluso cuando otro panel tiene el foco.

- **F1–F12** — Envían la macro preescrita para esa tecla de función mientras el slice TX está en modo CW.
- **Escape** — Limpia el buffer incondicionalmente y aborta cualquier transmisión en curso. En un panel CWX inactivo es una operación inofensiva, por lo que presionarlo siempre es seguro.
- **+** y **-** — Ajustan la velocidad CW hacia arriba o hacia abajo por el valor del paso configurado (haga clic derecho en el cuadro giratorio **Speed:** para cambiar el paso). Funciona en cualquier vista.

## Consejos

- F1–F12 envían macros preescritas mientras el slice TX está en modo CW. Vea [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** limpia el buffer incondicionalmente. En un panel CWX inactivo es una operación inofensiva, por lo que presionarlo siempre es seguro.
- Ajuste **Speed:** en la barra inferior sin cambiar de vista. El cuadro giratorio es visible tanto en la vista de envío como en la de configuración.
- Use **+** y **-** para ajustar rápidamente la velocidad en incrementos de 3 WPM (o su paso configurado) sin hacer clic en el cuadro giratorio.
- Cuando se reconecta a una radio, el botón **Live** refleja automáticamente el estado live actual de la radio.
- Haga clic derecho en una burbuja del historial para reenviar texto pasado o limpiar todo el historial.
- Los modificadores de velocidad insertados en el texto escrito (por ejemplo, `[20]CQ [15]TEST`) se eliminan de la visualización de la burbuja del historial. Solo aparece el texto realmente transmitido.
- El botón **Send** en el panel CWX está marcado para indicar que activa el transmisor. La etiqueta "Send" en sí no coincide con ninguna palabra clave reservada, evitando conflictos con otros controles de activación del TX.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo esté configurado en modo CW, CWL o CWU. El panel requiere un slice en modo CW y una conexión de radio activa.
- **Hacer clic en Send no transmite** — Si **Live** estaba activado, el primer clic en **Send** solo apaga **Live**. Haga clic en **Send** una segunda vez (o presione **Enter**) para transmitir el buffer.
- **Presionar Enter no hace nada** — Haga clic dentro del Send text area primero para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo de toda la aplicación. Si un diálogo o widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.
- **Las macros F1–F12 no se activan** — Asegúrese de que el slice TX esté en modo CW, CWL o CWU. Los atajos están controlados por el modo del slice TX, no por la visibilidad del panel.
- **La burbuja abortada no muestra tachado** — Verifique que presionó Escape durante la transmisión activa. El tachado solo aparece para el texto que aún no se había enviado cuando ocurrió el aborto.
- **El ajuste del paso de velocidad no hace nada** — Haga clic derecho en el cuadro giratorio **Speed:** y seleccione un valor del menú contextual. La configuración se guarda por panel.

## Relacionado

- [CWX overview](overview.md)
- [Trigger a CW macro with F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Edit a CW macro string](edit-a-cw-macro-string.md)
- [Change CW send speed in WPM](change-cw-send-speed-in-wpm.md)
- [Enable QSK full break-in](enable-qsk-full-break-in.md)
- [Look up the prosign character shortcuts](look-up-the-prosign-character-shortcuts.md)
