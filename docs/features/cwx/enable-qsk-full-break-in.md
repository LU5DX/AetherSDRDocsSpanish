# Habilitar QSK (Full Break-in)

QSK (full break-in, o interrupción total) permite que la radio reciba entre cada punto y raya al transmitir en CW. Actívelo en la vista de configuración de CWX para que la radio cambie a recepción durante las pausas en su envío.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa a la radio.
- Configure el slice de TX en modo CW, CWL o CWU para que el panel CWX esté disponible.

## Pasos

1. Abra el panel CWX en la ventana principal.
2. Haga clic en **Setup** en la parte inferior del panel para cambiar a la vista de configuración.
3. Haga clic en **QSK** para activarlo. El botón se resalta cuando está activo.

Para desactivar QSK, haga clic en **QSK** nuevamente.

## Función de cada control

| Control | Comportamiento | Valor predeterminado | Clave de configuración |
|---------|---------------|----------------------|------------------------|
| **QSK** | Activa o desactiva QSK (full break-in). | Desactivado | `CwxQsk` |
| **Delay:** | Retardo entre macros en milisegundos. | 5 | `CwxDelay` |
| **Speed:** | Velocidad CW en WPM. | 20 | `CwxSpeedWpm` |
| **Send (vista)** | Cambia al área de envío en vivo con historial y campo de texto. | – | – |
| **Live (vista)** | Cambia a la vista de envío en vivo. | – | – |
| **Setup (vista)** | Cambia al editor de macros y configuración de QSK. | – | – |
| **Desplazamiento del historial de envío** | Muestra búferes de envío anteriores con resaltado de caracteres. | – | – |
| **Área de texto de envío** | Escriba caracteres CW; Enter envía el búfer. | – | – |
| **F1 … F12 (macros)** | Envía la macro preescrita para esa tecla de función. | – | `CwxMacro_F1..F12` |
| **Editores de macros F1 … F12** | Editores en la vista de configuración para cada macro. | – | `CwxMacro_F1..F12` |
| **Leyenda de prosignos** | Muestra atajos para prosignos CW comunes (=, +, (, &, $). | – | – |

## Cómo interactúan Send y Live

En la v26.6.1, los botones **Send** y **Live** ya no actúan como un simple grupo de selección mutua. Su comportamiento depende del estado actual del panel:

- **Live** es un conmutador. Haga clic una vez para habilitar la tecleo carácter por carácter en vivo; haga clic de nuevo para deshabilitarlo. El estado marcado del botón siempre refleja el estado en vivo del modelo, incluso si el estado fue cambiado externamente.
- **Send** se comporta de manera diferente según si **Live** está activo al hacer clic:
  - Si **Live** está actualmente **desactivado**, al hacer clic en **Send** se envía el búfer escrito de inmediato.
  - Si **Live** está actualmente **activado**, al hacer clic en **Send** primero se desactiva el modo en vivo y se devuelve el panel a la vista de envío normal. El búfer **no** se retransmite, porque algunos caracteres ya pueden haberse tecleado carácter por carácter.
- Al hacer clic en **Setup**, siempre se desactiva el modo en vivo antes de cambiar a la vista de configuración.

## Comportamiento de las burbujas de historial

Cada mensaje enviado aparece como una burbuja de historial en el área **Send history scroll**. Las burbujas muestran el texto CW y una marca de tiempo. A medida que se envían los caracteres, la burbuja se actualiza para mostrar qué caracteres se han transmitido.

### Burbujas abortadas (tecla Escape)

Presione **Escape** durante la transmisión para abortar el búfer actual. La burbuja del mensaje abortado muestra:
- Los caracteres que ya se enviaron aparecen normalmente.
- Los caracteres que aún no se enviaron aparecen con formato tachado (una línea sobre el texto).

Esta distinción visual le ayuda a ver qué llegó al aire y qué se interrumpió.

### Menú contextual de la burbuja de historial

Haga clic derecho en cualquier burbuja para abrir un menú contextual con las siguientes acciones:

- **Resend** — Envía nuevamente el mensaje seleccionado y agrega una nueva burbuja de historial con la marca de tiempo actual.
- **Clear History** — Elimina todas las burbujas de historial del área de desplazamiento.

## Comportamiento de los atajos F1–F12 y Escape

Las teclas de función F1–F12 y la tecla **Escape** están disponibles como atajos en toda la aplicación. Los atajos se habilitan o deshabilitan según el modo del slice de TX, no por la visibilidad del panel. Esto garantiza que las teclas funcionen independientemente de si el panel CWX está visible o no, mientras se evitan conflictos con el panel DVK (Digital Voice Keyer).

- Cuando el slice de TX está en modo CW, CWL o CWU: F1–F12 activan las macros CW correspondientes, y **Escape** aborta el búfer de envío actual.
- Cuando el slice de TX está en un modo de voz: F1–F12 activan las macros de DVK en su lugar.
- Los atajos son gestionados automáticamente por MainWindow según el modo del slice de TX.

## Configuración del paso de velocidad

El panel CWX admite prefijos modificadores de velocidad en las macros. El valor del paso en el control **Speed:** determina cuánto cambia la velocidad al usar caracteres de modificación de velocidad. Para configurar el paso:

1. Haga clic derecho en el control **Speed:** para abrir el menú contextual.
2. Seleccione **Speed step...** para abrir el diálogo de Speed Step.
3. Ingrese un valor entre 1 y 20 WPM.
4. Haga clic en **OK**.

El valor del paso se guarda y persiste entre sesiones.

## Relacionados

- [Visión general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
