# Cambiar la velocidad de envío CW en PPM

Ajuste la velocidad de manipulación CW para que el equipo transmita a la tasa de PPM (palabras por minuto) que necesita. El control de velocidad está disponible en todo momento desde la barra inferior del panel CWX.

## Antes de comenzar

- Conéctese a un equipo FLEX-8600. El panel CWX requiere una conexión activa con el equipo.
- Abra el panel CWX. Aparece en el área de la ventana principal cuando el slice activo está en modo CW, CWL o CWU.

## Pasos

1. Localice el spinbox **Speed:** en la barra inferior del panel CWX.
2. Haga clic en el spinbox y escriba un valor, o use las flechas arriba/abajo para ajustar la velocidad.
3. La nueva velocidad surte efecto de inmediato. El valor se guarda como `CwxSpeedWpm`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| **Speed:** | 20 | 5–100 WPM | `CwxSpeedWpm` | Establece la velocidad de manipulación CW en palabras por minuto. |

## Comportamiento de los botones Send, Live y Setup

Los tres botones de vista en la barra superior del panel CWX cambiaron su comportamiento a partir de la versión v0.9.2.1.

| Botón | Tipo | Comportamiento |
|---|---|---|
| **Send (view)** | Botón de acción | Si el modo **Live** está actualmente desactivado, al hacer clic en **Send** se envía el búfer escrito de inmediato y el panel permanece en la vista Send. Si el modo **Live** está actualmente activado, al hacer clic en **Send** primero se desactiva el modo Live y el panel regresa a la vista de escritura normal sin retransmitir ningún texto que ya haya sido manipulado carácter por carácter. |
| **Live (view)** | Botón de alternancia | Activa o desactiva el modo Live. Al activarse, el panel cambia a la vista Send y el equipo comienza a manipular los caracteres a medida que se escriben. Desactivar Live no borra el búfer. Si se navega a **Setup** mientras Live está activo, este se desactiva automáticamente. |
| **Setup (view)** | Botón de acción | Muestra el editor de macros y la configuración de QSK. Abrir Setup siempre desactiva el modo Live antes de mostrar la vista Setup. |

> **Nota:** Antes de la versión v0.9.2.1, **Send** era un botón seleccionable que funcionaba como parte de un grupo de alternancia mutuamente exclusivo junto con **Live** y **Setup**. Ahora es un botón de acción simple cuyo comportamiento depende de si el modo Live está activo en el momento de hacer clic.

## El estado del modo Live se conserva al reconectar

Cuando se asocia un modelo al panel CWX (por ejemplo, al conectarse al equipo), el botón **Live** se actualiza para reflejar el estado actual del modo Live reportado por el equipo. Esto significa que si el modo Live estaba activo antes de una desconexión, el botón mostrará el estado correcto cuando se restaure la conexión.

## Consejos

- El spinbox **Speed:** es visible en las tres vistas (Send, Live y Setup). No es necesario cambiar de vista para modificar la velocidad.
- Presione Escape en cualquier momento para interrumpir una transmisión en curso sin modificar la configuración de velocidad.
- Si está en modo Live y desea escribir texto por adelantado sin transmitir, haga clic en **Send** para salir del modo Live antes de continuar escribiendo. El panel no retransmitirá ningún carácter que ya haya sido enviado.

## Temas relacionados

- [Descripción general de CWX](overview.md)
- [Enviar un búfer CW escrito en modo Live](send-a-typed-cw-buffer-live.md)
- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Habilitar QSK de ruptura total](enable-qsk-full-break-in.md)
