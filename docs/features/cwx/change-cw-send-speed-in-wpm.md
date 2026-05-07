# Cambiar la velocidad de envío de CW en WPM

Ajuste la velocidad de manipulación de CW para que la radio envíe a la velocidad en WPM que necesite. La configuración de velocidad está disponible en todo momento desde la barra inferior del panel CWX.

## Antes de comenzar

- Conéctese a una radio FLEX-8600. El panel CWX requiere una conexión activa a la radio.
- Abra el panel CWX. Aparece en el área de la ventana principal cuando la franja activa está en modo CW, CWL o CWU.

## Pasos

1. Localice el cuadro de número **Speed:** en la barra inferior del panel CWX.
2. Haga clic en el cuadro de número y escriba un valor, o use las flechas arriba/abajo para ajustar la velocidad.
3. La nueva velocidad surte efecto de inmediato. El valor se guarda como `CwxSpeedWpm`.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Speed:** | 20 | 5–100 WPM | `CwxSpeedWpm` | Establece la velocidad de manipulación de CW en palabras por minuto. |

## Comportamiento de los botones Send, Live y Setup

Los tres botones de vista en la barra superior del panel CWX cambiaron su comportamiento en la versión v0.9.2.1.

| Botón | Tipo | Comportamiento |
|---|---|---|
| **Send (view)** | Botón pulsador | Si el modo **Live** está actualmente desactivado, al hacer clic en **Send** se envía el búfer escrito de inmediato y se permanece en la vista Send. Si el modo **Live** está actualmente activado, al hacer clic en **Send** primero se desactiva el modo Live y se regresa a la vista de escritura normal sin retransmitir ningún texto que ya se haya manipulado carácter por carácter. |
| **Live (view)** | Botón de conmutación | Activa o desactiva el modo Live. Al activarse, el panel cambia a la vista Send y la radio comienza a manipular caracteres a medida que los escribe. Desactivar Live no borra el búfer. Navegar a **Setup** mientras Live está activo desactiva Live automáticamente. |
| **Setup (view)** | Botón pulsador | Muestra el editor de macros y la configuración de QSK. Abrir Setup siempre desactiva el modo Live antes de mostrar la vista Setup. |

> **Nota:** Antes de v0.9.2.1, **Send** era un botón seleccionable que actuaba como parte de un grupo de conmutación mutuamente excluyente con **Live** y **Setup**. Ahora es un botón pulsador simple cuya acción depende de si el modo Live está activo al hacer clic en él.

## El estado del modo Live se conserva al reconectar

Cuando se asocia un modelo al panel CWX (por ejemplo, después de conectarse a la radio), el botón **Live** se actualiza para reflejar el estado Live actual informado por la radio. Esto significa que si el modo Live estaba activo antes de una desconexión, el botón mostrará el estado correcto cuando se restablezca la conexión.

## Consejos

- El cuadro de número **Speed:** es visible en las tres vistas (Send, Live y Setup). No necesita cambiar de vista para modificar la velocidad.
- Presione Escape en cualquier momento para abortar una transmisión en curso sin cambiar la configuración de velocidad.
- Si está en modo Live y desea escribir por adelantado sin transmitir, haga clic en **Send** para salir del modo Live antes de continuar escribiendo. El panel no reenviará ningún carácter que ya se haya transmitido.

## Relacionados

- [Visión general de CWX](overview.md)
- [Enviar un búfer de CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Activar una macro de CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Habilitar QSK de ruptura total](enable-qsk-full-break-in.md)
