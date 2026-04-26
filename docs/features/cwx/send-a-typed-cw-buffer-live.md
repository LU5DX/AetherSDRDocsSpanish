# Enviar un búfer de CW escrito en tiempo real

Use el panel CWX para escribir un mensaje de CW y transmitirlo de inmediato. Esta es la forma más rápida de enviar CW de texto libre sin necesidad de escribir una macro previamente.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión de radio activa.
- Configure el slice activo en modo CW, CWL o CWU. El panel CWX aparece en la ventana principal cuando hay un slice en modo CW activo.

## Pasos

1. En el panel CWX, haga clic en **Send** para asegurarse de que la vista de envío esté activa. El botón **Send** se encuentra en la barra inferior del panel.
2. Haga clic dentro del **Send text area** — el campo de texto en la parte inferior de la vista de envío. El texto de marcador de posición dice "Type CW message...".
3. Escriba su mensaje. Use caracteres ASCII estándar. Consulte la leyenda de prosignos que se muestra en el panel para ver los atajos de prosignos (=, +, (, &, $).
4. Presione **Enter** para transmitir el búfer. La radio comienza a enviar de inmediato.
5. Para abortar la transmisión en cualquier momento, presione **Escape**. Esto limpia el búfer y detiene el envío.

Después de la transmisión, el texto enviado aparece en el área **Send history scroll**, encima del campo de texto, como una burbuja con marca de tiempo.

## Qué hace cada control

| Control | Qué hace | Clave de configuración |
|---|---|---|
| **Send** | Cambia a la vista de envío, que muestra el historial y el campo de texto. | — |
| **Live** | Cambia a la vista de envío en tiempo real. | — |
| **Setup** | Cambia a la vista del editor de macros y configuración de QSK. | — |
| **Speed:** | Establece la velocidad de envío de CW en WPM. Rango: 5–100 WPM. Valor predeterminado: 20 WPM. | `CwxSpeedWpm` |
| Send text area | Escriba aquí su mensaje de CW. Presione Enter para enviar. | — |
| Send history scroll | Muestra los búferes enviados anteriormente con marcas de tiempo. Solo lectura. | — |
| **Delay:** | Establece el retardo entre macros en milisegundos. Rango: 0–2000 ms. Valor predeterminado: 5 ms. Disponible en la vista Setup. | `CwxDelay` |
| **QSK** | Habilita QSK (break-in completo). Disponible en la vista Setup. | `CwxQsk` |
| Prosigns legend | Muestra los atajos de caracteres para los prosignos de CW más comunes. Solo lectura. | — |

## Consejos

- F1–F12 envían macros preescritas mientras haya un slice en modo CW activo. Los atajos de teclado funcionan en toda la aplicación en los modos CW y CWL. Consulte [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md).
- Presionar **Escape** limpia el búfer de forma incondicional. En un panel CWX sin actividad, es una operación inofensiva sin efecto, por lo que siempre es seguro presionarlo.
- Ajuste **Speed:** en la barra inferior sin necesidad de cambiar de vista. El cuadro de número es visible tanto en la vista de envío como en la vista de configuración.

## Solución de problemas

- **El panel CWX no aparece** — Confirme que el slice activo esté configurado en modo CW, CWL o CWU. El panel requiere un slice en modo CW y una conexión de radio activa.
- **Presionar Enter no hace nada** — Haga clic dentro del Send text area primero para darle el foco, luego presione Enter.
- **Escape no detiene la transmisión** — Escape activa un atajo a nivel de toda la aplicación. Si un cuadro de diálogo o un widget de texto captura la tecla primero, haga clic fuera de él y presione Escape nuevamente.

## Relacionados

- [Descripción general de CWX](overview.md)
- [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Editar una cadena de macro de CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío de CW en WPM](change-cw-send-speed-in-wpm.md)
- [Habilitar QSK de break-in completo](enable-qsk-full-break-in.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
