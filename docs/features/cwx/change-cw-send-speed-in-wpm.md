# Panel CWX

El panel CWX es la vista de operación en CW para una radio FLEX-8600. Permite enviar texto CW escrito, almacenar y activar hasta 12 macros de teclas F, controlar la velocidad de tecleo y habilitar QSK (full break-in).

## Abrir el panel CWX

El panel CWX aparece en el área principal de la ventana cuando el slice activo está en modo CW, CWL o CWU. Requiere una conexión activa con la radio.

## Cambiar la velocidad de envío CW en WPM

Ajuste la velocidad de tecleo CW para que la radio envíe a la velocidad en WPM que necesite. La configuración de velocidad está disponible en todo momento desde la barra inferior del panel CWX.

### Pasos

1. Localice el cuadro giratorio **Speed:** en la barra inferior del panel CWX.
2. Haga clic en el cuadro giratorio y escriba un valor, o use las flechas hacia arriba/abajo para ajustar la velocidad.
3. La nueva velocidad surte efecto de inmediato. El valor se guarda como `CwxSpeedWpm`.

## Función de cada control

| Control | Tipo | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| **Send (vista)** | Botón pulsador | – | – | – | Muestra el área de envío en vivo con historial y campo de texto. |
| **Live (vista)** | Botón pulsador | – | – | – | Muestra la vista de envío en vivo. |
| **Setup (vista)** | Botón pulsador | – | – | – | Muestra el editor de macros y la configuración de QSK. |
| **Speed:** | Cuadro giratorio | 20 | 5–100 WPM | `CwxSpeedWpm` | Establece la velocidad de tecleo CW en palabras por minuto. |
| **Desplazamiento de historial de envío** | Indicador | – | – | – | Muestra búferes de envío anteriores con resaltado de caracteres. |
| **Área de texto de envío** | Campo de texto | – | – | – | Escriba caracteres CW; Enter envía el búfer. |
| **F1 … F12 (macros)** | Botón pulsador | – | – | `CwxMacro_F1..F12` | Envía la macro preescrita para esa tecla de función. |
| **Editores de macros F1 … F12** | Campo de texto | – | – | `CwxMacro_F1..F12` | Editores de la vista Setup para cada macro. |
| **Delay:** | Cuadro giratorio | 0 | 0–10000 ms | `CwxDelay` | Establece el retardo entre macros en milisegundos. |
| **QSK** | Botón de alternancia | Desactivado | – | `CwxQsk` | Activa o desactiva QSK (full break-in). |
| **Leyenda de prosignos** | Indicador | – | – | – | Muestra atajos para prosignos CW comunes (=, +, (, &, $). |

## Cómo se comportan los botones Send, Live y Setup

Los tres botones de vista en la barra superior del panel CWX cambiaron su comportamiento en v0.9.2.1.

| Botón | Tipo | Comportamiento |
|---|---|---|
| **Send (vista)** | Botón pulsador | Si el modo **Live** está actualmente desactivado, al hacer clic en **Send** se envía el búfer escrito de inmediato y permanece en la vista Send. Si el modo **Live** está actualmente activado, al hacer clic en **Send** primero se desactiva el modo Live y se devuelve el panel a la vista normal de escritura sin retransmitir ningún texto que ya se haya tecleado carácter por carácter. |
| **Live (vista)** | Botón pulsador | Muestra la vista de envío en vivo. Al activarlo, el panel cambia a la vista Send y la radio comienza a teclear los caracteres a medida que los escribe. Desactivar Live no borra el búfer. Navegar a **Setup** mientras Live está activado desactiva Live automáticamente. |
| **Setup (vista)** | Botón pulsador | Muestra el editor de macros y la configuración de QSK. Abrir Setup siempre desactiva el modo Live antes de mostrar la vista Setup. |

> **Nota:** Antes de v0.9.2.1, **Send** era un botón seleccionable que formaba parte de un grupo de alternancia mutuamente excluyente con **Live** y **Setup**. Ahora es un botón pulsador normal cuya acción depende de si el modo Live está activo cuando hace clic en él.

## El estado del modo Live se conserva al reconectar

Cuando un modelo se adjunta al panel CWX (por ejemplo, después de conectarse a la radio), el botón **Live** se actualiza para reflejar el estado Live actual informado por la radio. Esto significa que si el modo Live estaba activo antes de una desconexión, el botón mostrará el estado correcto cuando se restablezca la conexión.

## Menú contextual del historial de envío

Cada entrada en el área de desplazamiento del historial de envío admite un menú contextual con clic derecho con dos acciones:

- **Resend** – Reenvía el búfer de texto seleccionado. Se agrega una nueva entrada de historial al desplazamiento.
- **Clear History** – Elimina todas las entradas del historial del área de desplazamiento. No afecta a la radio.

## Transmisiones abortadas mostradas con tachado

Si presiona Escape mientras la radio está enviando un búfer CW, la transmisión se aborta. En el área de desplazamiento del historial de envío, la burbuja de historial de esa transmisión muestra la parte enviada en texto normal y la parte no enviada con formato de tachado. Esto deja claro qué caracteres se transmitieron realmente antes del aborto.

## Las burbujas de historial muestran texto expandido de modificadores de velocidad

Cuando las macros o el texto escrito contienen prefijos de modificadores de velocidad (por ejemplo, `{10}...{20}...`), la burbuja de historial muestra el texto tal como se tecleó realmente, con los marcadores de cambio de velocidad eliminados y los segmentos unidos. Esto brinda una visualización limpia y legible de lo que se transmitió, sin la sobrecarga de indicadores de cambio de velocidad en línea.

## Atajos de teclado

El panel CWX registra atajos de aplicación globales para las teclas F1–F12 y la tecla Escape. Estos atajos se activan cuando el slice TX está en modo CW o CWL, independientemente de si el panel CWX es visible. El estado de habilitación lo gestiona la MainWindow según el modo del slice TX, lo que evita conflictos de atajos con otros paneles como el panel de macros DVK que usa las mismas teclas F1–F12 para sus propios fines.

| Atajo | Comportamiento |
|---|---|
| **F1–F12** | Envía la macro correspondiente (F1–F12) cuando el slice TX está en modo CW o CWL. |
| **Escape** | Borra el búfer de texto actual (aborta cualquier transmisión en curso). |

## Disposición de la vista Setup

La vista Setup contiene los 12 editores de macros de teclas F, el cuadro giratorio **Delay:**, la alternancia **QSK** y la leyenda de prosignos. Los editores de macros están dispuestos en una cuadrícula desplazable para que pueda acceder a los 12 incluso cuando el panel es bajo. Si la altura del panel está limitada, use la barra de desplazamiento para llegar a las macros que no son visibles.

## Consejos

- El cuadro giratorio **Speed:** es visible en las tres vistas (Send, Live y Setup). No necesita cambiar de vista para cambiar la velocidad.
- Presione Escape en cualquier momento para abortar una transmisión en curso sin cambiar la configuración de velocidad.
- Si está en modo Live y desea escribir por adelantado sin transmitir, haga clic en **Send** para salir del modo Live antes de continuar escribiendo. El panel no reenviará ningún carácter que ya se haya transmitido.
- La leyenda de prosignos muestra atajos para prosignos CW comunes: = (BT), + (AR), ( (KN), & (AS), $ (SK).
- Haga clic derecho en cualquier burbuja de historial para reenviar ese texto o borrar todo el historial.
- Después de abortar una transmisión, inspeccione la burbuja de historial para ver qué caracteres se enviaron (texto normal) y cuáles no (texto tachado).

## Relacionados

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Habilitar QSK full break-in](enable-qsk-full-break-in.md)
