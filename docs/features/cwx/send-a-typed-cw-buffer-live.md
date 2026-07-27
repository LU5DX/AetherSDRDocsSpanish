# Enviar un búfer de CW escrito en vivo

Use el panel CWX para escribir un mensaje en CW y transmitirlo de inmediato. Es la forma más rápida de enviar texto libre en CW sin necesidad de escribir un macro previamente.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa con la radio.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando hay un slice en modo CW activo.
- Ajuste el **Speed step** (cuánto cambia la velocidad al presionar **+** o **-**). Haga clic derecho en el cuadro **Speed:** y elija un valor entre 1 y 20 WPM. El valor predeterminado es 3 WPM. Esta configuración se guarda por panel y persiste entre reinicios.

## Pasos

1. En el panel CWX, asegúrese de que **Live** esté desactivado. Si **Live** está activo (botón marcado), haga clic en él para desactivarlo antes de escribir un mensaje en búfer.
2. Haga clic dentro del **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignos que se muestra en el panel para conocer los accesos directos de prosignos (=, +, (, &, $). Puede insertar modificadores de velocidad: `[20]` establece la velocidad a 20 WPM, `[15]` a 15 WPM, etc. El prefijo del modificador se elimina automáticamente del texto de la burbuja mostrada.
4. Haga clic en **Send** o presione **Enter** para transmitir el búfer. La radio comienza a enviar de inmediato.
5. Para abortar la transmisión en cualquier momento, presione **Escape**. Esto limpia el búfer y detiene el envío. Cuando se aborta, la burbuja del historial muestra los caracteres enviados en texto normal y los caracteres no enviados con formato tachado.

Después de la transmisión, el texto enviado aparece en el área **Send history scroll**, encima del campo de texto, como una burbuja con marca de tiempo. La burbuja muestra el texto realmente transmitido con los prefijos de modificador de velocidad eliminados.

## Reenviar o borrar el historial

Haga clic derecho en cualquier burbuja del historial para abrir un menú contextual con dos opciones:

- **Resend** — Vuelve a transmitir el mismo texto. El texto aparece como una nueva burbuja con marca de tiempo en el historial.
- **Clear History** — Elimina todas las burbujas del historial del área de desplazamiento.

## Comportamiento de Send según el modo Live

El botón **Send** se comporta de manera diferente según si **Live** está activado actualmente:

- **Live desactivado** — Al hacer clic en **Send** se envía el contenido del campo de texto como un búfer y se transmite.
- **Live activado** — Al hacer clic en **Send**, primero se desactiva **Live** y el panel vuelve a la vista de envío. El búfer *no* se retransmite; esto evita que el texto que ya se tecleó carácter por carácter en modo live se envíe una segunda vez. Después de hacer clic en **Send** en este estado, escriba su mensaje y vuelva a hacer clic en **Send** para transmitir.

## Indicadores visuales de transmisión abortada

Cuando presiona **Escape** durante la transmisión, la burbuja del historial muestra qué caracteres se enviaron y cuáles no:

- **Caracteres enviados** — Aparecen en texto normal.
- **Caracteres no enviados** — Aparecen con formato tachado. Esto proporciona una retroalimentación visual clara sobre exactamente qué se transmitió y qué se abortó.

El formato tachado funciona correctamente para mensajes de una sola línea (indicativos, RST, números de serie). Para mensajes multilínea con ajuste de línea, el tachado puede no alinearse perfectamente en las líneas de continuación.

## Función de cada control

| Control | Función | Clave de configuración |
|---|---|---|
| **Send** (vista) | Muestra el área de envío en vivo con historial y campo de texto. | — |
| **Live** (vista) | Muestra la vista de envío en vivo. | — |
| **Setup** (vista) | Muestra el editor de macros y la configuración de QSK. | — |
| **Speed:** | Establece la velocidad de envío CW en WPM. | `CwxSpeedWpm` |
| **Speed step** (clic derecho en **Speed:**) | Establece cuánto cambia la velocidad al presionar **+** o **-** en WPM. Rango 1-20, predeterminado 3. | `CwxPanel` → `speedStep` (por panel) |
| Send text area | Escriba aquí su mensaje CW. Presione Enter para enviar. | — |
| Send history scroll | Muestra búferes enviados anteriormente con resaltado de caracteres. Solo lectura. Haga clic derecho en una burbuja para Reenviar o Borrar historial. | — |
| **F1 … F12** (macros) | Envía el macro preescrito para esa tecla de función. | `CwxMacro_F1..F12` |
| **F1 … F12** editores de macro | Editores de vista de configuración para cada macro. | `CwxMacro_F1..F12` |
| **Delay:** | Establece la demora entre macros en milisegundos. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Habilita QSK (full break-in). Disponible en la vista Setup. | `CwxQsk` |
| Prosigns legend | Muestra accesos directos de caracteres para prosignos CW comunes (=, +, (, &, $). Solo lectura. | — |

## Atajos de teclado

Los atajos F1–F12 y Escape se activan cuando el slice TX está en modo CW (CW o CWL). Esto le permite activar macros incluso cuando otro panel tiene el foco.

- **F1–F12** — Envía el macro preescrito para esa tecla de función mientras el slice TX está en modo CW.
- **Escape** — Limpia el búfer incondicionalmente y aborta cualquier transmisión en curso. En un panel CWX inactivo, es una operación inofensiva, por lo que presionarlo siempre es seguro.
- **+** y **-** — Ajustan la velocidad CW hacia arriba o hacia abajo según el valor del paso de velocidad configurado (haga clic derecho en el cuadro **Speed:** para cambiar el paso). Funciona en cualquier vista.

## Consejos

- F1–F12 envían macros preescritos mientras el slice TX está en modo CW. Consulte [Activar un macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** limpia el búfer incondicionalmente. En un panel CWX inactivo, es una operación inofensiva, por lo que presionarlo siempre es seguro.
- Ajuste **Speed:** en la barra inferior sin cambiar de vista. El cuadro es visible tanto en la vista de envío como en la de configuración.
- Use **+** y **-** para ajustar rápidamente la velocidad en incrementos de 3 WPM (o el paso configurado) sin hacer clic en el cuadro.
- Cuando se vuelva a conectar a una radio, el botón **Live** refleja automáticamente el estado live actual de la radio.
- Haga clic derecho en una burbuja del historial para reenviar texto anterior o borrar todo el historial.
- Los modificadores de velocidad insertados en el texto escrito (p. ej., `[20]CQ [15]TEST`) se eliminan de la visualización de la burbuja del historial. Solo aparece el texto realmente transmitido.
- El botón **Send** en el panel CWX está marcado para indicar que activa el transmisor. La etiqueta "Send" en sí no coincide con ninguna palabra clave reservada, lo que evita conflictos con otros controles de activación TX.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo esté configurado en modo CW, CWL o CWU. El panel requiere un slice en modo CW y una conexión activa con la radio.
- **Al hacer clic en Send no transmite** — Si **Live** estaba activado, el primer clic en **Send** solo desactiva **Live**. Haga clic en **Send** una segunda vez (o presione **Enter**) para transmitir el búfer.
- **Presionar Enter no hace nada** — Haga clic dentro del área de texto de envío primero para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo de toda la aplicación. Si un cuadro de diálogo o widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.
- **Los macros F1–F12 no se activan** — Asegúrese de que el slice TX esté en modo CW, CWL o CWU. Los atajos están controlados por el modo del slice TX, no por la visibilidad del panel.
- **La burbuja abortada no muestra tachado** — Verifique que presionó Escape durante la transmisión activa. El tachado solo aparece para el texto que aún no se había enviado cuando ocurrió el aborto.
- **El ajuste del paso de velocidad no hace nada** — Haga clic derecho en el cuadro **Speed:** y seleccione un valor del menú contextual. La configuración se guarda por panel.

## Relacionados

- [Descripción general de CWX](overview.md)
- [Activar un macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Habilitar QSK full break-in](enable-qsk-full-break-in.md)
- [Consultar los accesos directos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
