# Cambiar la velocidad de envío CW en WPM

Ajuste la velocidad de manipulacion CW para que la radio envíe a la velocidad WPM que necesite. La configuración de velocidad está disponible en todo momento desde la barra inferior del panel CWX.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa con la radio.
- Abra el panel CWX. Aparece en el área de la ventana principal cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. Localice el control **Speed:** en la barra inferior del panel CWX.
2. Haga clic en el control y escriba un valor, o use las flechas arriba/abajo para ajustar la velocidad.
3. La nueva velocidad se aplica de inmediato. El valor se guarda como `CwxSpeedWpm`.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Speed:** | 20 | 5–100 WPM | `CwxSpeedWpm` | Establece la velocidad de manipulacion CW en palabras por minuto. |
| **Delay:** | 0 | 0–10000 ms | `CwxDelay` | Establece el retardo entre macros en milisegundos. |
| **QSK** | Off | – | `CwxQsk` | Activa o desactiva QSK (full break-in). |

## Comportamiento de los botones Send, Live y Setup

Los tres botones de vista en la barra superior del panel CWX cambiaron su comportamiento en la versión v0.9.2.1.

| Botón | Tipo | Comportamiento |
|---|---|---|
| **Send (view)** | Botón pulsador | Si el modo **Live** está actualmente desactivado, al hacer clic en **Send** se envía inmediatamente el búfer escrito y permanece en la vista Send. Si el modo **Live** está actualmente activado, al hacer clic en **Send** primero se desactiva el modo Live y se vuelve a la vista normal de escritura sin retransmitir ningún texto que ya se haya manipulado carácter por carácter. |
| **Live (view)** | Botón de alternancia | Activa o desactiva el modo Live. Al activarlo, el panel cambia a la vista Send y la radio comienza a manipular los caracteres a medida que los escribe. Desactivar Live no borra el búfer. Navegar a **Setup** mientras Live está activo desactiva Live automáticamente. |
| **Setup (view)** | Botón pulsador | Muestra el editor de macros y la configuración de QSK. Abrir Setup siempre desactiva el modo Live antes de mostrar la vista Setup. |

> **Nota:** Antes de v0.9.2.1, **Send** era un botón seleccionable que actuaba como parte de un grupo de alternancia mutuamente excluyente con **Live** y **Setup**. Ahora es un botón pulsador simple cuya acción depende de si el modo Live está activo cuando se hace clic en él.

## El estado del modo Live se conserva al reconectar

Cuando se adjunta un modelo al panel CWX (por ejemplo, después de conectarse a la radio), el botón **Live** se actualiza para reflejar el estado Live actual informado por la radio. Esto significa que si el modo Live estaba activo antes de una desconexión, el botón mostrará el estado correcto cuando se restablezca la conexión.

## Menú contextual del historial de envíos

Cada entrada en el área de desplazamiento del historial de envíos admite un menú contextual con clic derecho con dos acciones:

- **Resend** – Vuelve a enviar el búfer de texto seleccionado. Se añade una nueva entrada de historial al área de desplazamiento.
- **Clear History** – Elimina todas las entradas del historial del área de desplazamiento. No afecta a la radio.

## Atajos de teclado

El panel CWX registra atajos globales de la aplicación para las teclas F1–F12 y la tecla Escape. Estos atajos se activan cuando el slice activo está en modo CW, CWL o CWU, independientemente de si el panel CWX está visible. Esto evita conflictos de atajos con otros paneles, como el panel de macros DVK, que utiliza las mismas teclas F1–F12 para sus propios fines. El estado de habilitación es gestionado por la MainWindow según el modo del slice activo.

| Atajo | Comportamiento |
|---|---|
| **F1–F12** | Envía la macro correspondiente (F1–F12) cuando el slice activo está en modo CW o CWL. |
| **Escape** | Borra el búfer de texto actual (cancela cualquier transmisión en curso). |

## Consejos

- El control **Speed:** está visible en las tres vistas (Send, Live y Setup). No necesita cambiar de vista para ajustar la velocidad.
- Presione Escape en cualquier momento para cancelar una transmisión en curso sin cambiar la configuración de velocidad.
- Si está en modo Live y desea escribir por adelantado sin transmitir, haga clic en **Send** para salir del modo Live antes de continuar escribiendo. El panel no reenviará ningún carácter que ya se haya transmitido.
- La leyenda de Prosigns muestra atajos para prosignos CW comunes: = (BT), + (AR), ( (KN), & (AS), $ (SK).
- Haga clic derecho en cualquier burbuja del historial para reenviar ese texto o borrar todo el historial.

## Relacionado

- [Visión general de CWX](overview.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Habilitar QSK full break-in](enable-qsk-full-break-in.md)
