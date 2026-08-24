# Habilitar QSK Full Break-in

QSK (full break-in) permite que la radio reciba entre cada dit y dah mientras transmite CW. Habilítelo en la vista Setup de CWX para que la radio cambie a recepción durante las pausas de su envío.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa a la radio.
- Configure el slice TX en modo CW, CWL o CWU para que el panel CWX esté disponible.

## Pasos

1. Abra el panel CWX en la ventana principal.
2. Haga clic en **Setup** en la parte inferior del panel para cambiar a la vista Setup.
3. Haga clic en **QSK** para activarlo. El botón se resalta cuando está activo.

Para desactivar QSK, haga clic en **QSK** nuevamente.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Clave de configuración |
|---------|----------------|----------------|------------------------|
| **QSK** | Activa o desactiva QSK (full break-in). | Off | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |
| **Speed:** | Velocidad de CW en WPM. | 20 | `CwxSpeedWpm` |
| **Send (vista)** | Cambia al área de envío en vivo con historial y campo de texto. | – | – |
| **Live (vista)** | Cambia a la vista de envío en vivo. | – | – |
| **Setup (vista)** | Cambia al editor de macros y a la configuración de QSK. | – | – |
| **Desplazamiento del historial de envío** | Muestra búferes de envío anteriores con resaltado de caracteres. | – | – |
| **Área de texto de envío** | Escriba caracteres CW; Enter envía el búfer. | – | – |
| **F1 … F12 (macros)** | Envía la macro preescrita para esa tecla de función. | – | `CwxMacro_F1..F12` |
| **Editores de macros F1 … F12** | Editores de la vista Setup para cada macro. | – | `CwxMacro_F1..F12` |
| **Leyenda de prosignos** | Muestra atajos para prosignos CW comunes (=, +, (, &, $). | – | – |

## Cómo interactúan Send y Live

Los botones **Send** y **Live** no funcionan como un simple grupo mutuamente excluyente. Su comportamiento depende del estado actual del panel:

- **Live** es un conmutador. Haga clic una vez para activar el keying en vivo carácter por carácter; haga clic nuevamente para desactivarlo. El estado marcado del botón siempre refleja el estado en vivo del modelo, incluso si el estado se cambió externamente.
- **Send** se comporta de manera diferente según si **Live** está activo al hacer clic:
  - Si **Live** está actualmente **off**, hacer clic en **Send** envía el búfer escrito de inmediato.
  - Si **Live** está actualmente **on**, hacer clic en **Send** primero desactiva el modo en vivo y devuelve el panel a la vista de envío normal. El búfer **no** se retransmite, porque algunos caracteres ya pueden haberse enviado carácter por carácter.
- Hacer clic en **Setup** siempre desactiva el modo en vivo antes de cambiar a la vista Setup.

## Comportamiento de las burbujas de historial

Cada mensaje enviado aparece como una burbuja de historial en el área **Send history scroll**. Las burbujas muestran el texto CW y una marca de tiempo. A medida que se envían los caracteres, la burbuja se actualiza para mostrar qué caracteres se han transmitido.

### Burbujas abortadas (tecla Escape)

Presione **Escape** durante la transmisión para abortar el búfer actual. La burbuja del mensaje abortado muestra:
- Los caracteres que ya se enviaron aparecen normalmente.
- Los caracteres que aún no se enviaron aparecen con formato de tachado (una línea a través del texto).

Esta distinción visual le ayuda a ver qué llegó al aire y qué se cortó.

### Menú contextual de las burbujas de historial

Haga clic derecho en cualquier burbuja para abrir un menú contextual con las siguientes acciones:

- **Resend** — Envía el mensaje seleccionado nuevamente y agrega una nueva burbuja de historial con la marca de tiempo actual.
- **Clear History** — Elimina todas las burbujas de historial del área de desplazamiento.

## Comportamiento de los atajos F1–F12 y Escape

Las teclas de función F1–F12 y la tecla **Escape** están disponibles como atajos en toda la aplicación. Los atajos se habilitan o deshabilitan según el modo del slice TX, no según la visibilidad del panel. Esto garantiza que las teclas funcionen tanto si el panel CWX está visible como si no, evitando conflictos con el panel DVK (Digital Voice Keyer).

- Cuando el slice TX está en modo CW, CWL o CWU: F1–F12 activan las macros CW correspondientes, y **Escape** aborta el búfer de envío actual.
- Cuando el slice TX está en un modo de voz: F1–F12 activan las macros DVK en su lugar.
- La MainWindow gestiona automáticamente los atajos según el modo del slice TX.

## Configuración del paso de velocidad

El panel CWX admite prefijos modificadores de velocidad en las macros. El valor de paso del cuadro giratorio **Speed:** determina cuánto cambia la velocidad al usar caracteres de modificación de velocidad. Para configurar el paso:

1. Haga clic derecho en el cuadro giratorio **Speed:** para abrir el menú contextual.
2. Seleccione **Speed step...** para abrir el diálogo Speed Step.
3. Ingrese un valor entre 1 y 20 WPM.
4. Haga clic en **OK**.

El valor del paso se guarda y persiste entre sesiones.

## Relacionado

- [Descripción general de CWX](overview.md)
- [Enviar un búfer de CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
