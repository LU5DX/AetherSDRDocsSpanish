# Activar una macro de CW con F1–F12

Presione una tecla de función para enviar una cadena de macro de CW preescrita a través del radio sin tener que escribir. Esto es útil para intercambios en concursos, llamadas CQ o cualquier texto que envíe repetidamente.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en modo CW o CWL. Las teclas de función F1–F12 se ignoran silenciosamente en todos los demás modos.
- Cada macro debe tener texto almacenado en su ranura. Consulte [Editar una cadena de macro de CW](edit-a-cw-macro-string.md) si las ranuras están vacías.

## Pasos

1. Abra el panel CWX. Aparece automáticamente cuando el slice activo está en modo CW o CWL.
2. Presione la tecla de función (F1 a F12) en su teclado que corresponda a la macro que desea enviar. La macro se activa inmediatamente.
3. Para detener la transmisión a medio enviar, presione Escape. Esto limpia el búfer de envío y detiene la salida.

Para enviar una macro usando los botones en pantalla en lugar del teclado:

1. Haga clic en **Setup** en la barra inferior del panel CWX.
2. Haga clic en el botón **F1** a **F12** junto a la macro que desea enviar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| F1 … F12 (teclado) | Envía la macro almacenada para esa tecla de función. Activo cuando el slice activo está en modo CW o CWL, independientemente de la visibilidad del panel CWX. | — | — | `CwxMacro_F1` … `CwxMacro_F12` |
| F1 … F12 (botones en pantalla) | Igual que las teclas del teclado; envía la macro correspondiente. | — | — | `CwxMacro_F1` … `CwxMacro_F12` |
| Speed: | Velocidad de envío de CW en WPM, aplicada a todos los envíos de macro. | 20 WPM | 5–100 WPM | `CwxSpeedWpm` |
| Delay: | Retardo entre macros en milisegundos. | 5 ms | 0–2000 ms | `CwxDelay` |
| QSK | Habilita el modo de break-in completo (QSK). | Off | On / Off | `CwxQsk` |

## Cómo interactúan Send, Live y Setup

El comportamiento del botón **Send** cambió en la versión v0.9.2.1. Su acción ahora depende de si el modo **Live** está activo actualmente:

- **Live está desactivado** — Al hacer clic en **Send** se envía el contenido del área de texto de envío inmediatamente, exactamente como al presionar Enter.
- **Live está activo** — Al hacer clic en **Send**, primero se desactiva el modo Live y se devuelve el panel a la vista normal de envío. El búfer **no** se retransmite. Esto evita que el texto que ya se introdujo carácter por carácter en el modo Live se envíe una segunda vez.

El botón **Live** ahora es un conmutador. Al hacer clic en él nuevamente mientras Live está activo, se desactiva el modo Live. Cuando un modelo conectado cambia el estado en vivo externamente (por ejemplo, desde otro panel o un evento del radio), el botón **Live** se actualiza automáticamente para reflejar el estado actual.

Al hacer clic en **Setup**, siempre se desactiva el modo Live antes de mostrar la vista del editor de macros.

## Acciones de clic derecho en las burbujas del historial de envíos

En el área del historial de envíos, haga clic derecho en cualquier burbuja de CW enviada anteriormente para acceder a un menú contextual con dos opciones:

- **Resend** — Vuelve a enviar el mismo texto inmediatamente. El texto se agrega como una nueva burbuja en el historial de envíos con la marca de tiempo actual.
- **Clear History** — Elimina todas las burbujas del historial de envíos.

El menú tiene un tema oscuro que coincide con la interfaz de AetherSDR.

## Consejos

- Los atajos F1–F12 son de toda la aplicación y se habilitan según el modo del slice activo, no la visibilidad del panel. Esto significa que funcionan incluso si el panel CWX está minimizado o si otro panel está visible, siempre que el slice esté en modo CW o CWL. Los atajos son mutuamente excluyentes con el conjunto F1–F12 del panel DVK (utilizado en modos SSB/Digital) para evitar ambigüedades.
- Presionar Escape durante el envío de una macro es la forma más rápida de abortar. Debido a que el radio transita rápidamente entre los estados de transmisión y listo durante CW, Escape funciona independientemente del estado de transmisión actual del radio.
- Ajuste **Speed:** en la barra inferior antes de enviar si necesita cambiar las WPM para la sesión actual.
- Si estaba enviando en vivo y desea reenviar el mismo texto, escríbalo nuevamente en el área de texto de envío después de hacer clic en **Send** para salir del modo Live, luego haga clic en **Send** una segunda vez (o presione Enter).
- Use **Resend** desde el menú contextual del historial para repetir rápidamente una macro o un búfer escrito anteriormente sin tener que volver a escribir.

## Solución de problemas

- **Presionar F1–F12 no hace nada** — Confirme que el slice activo esté en modo CW o CWL. Los atajos están deshabilitados cuando un slice en modo SSB o Digital está activo. Si otra aplicación ha capturado las teclas de función, traiga AetherSDR al primer plano.
- **La macro se envía pero no produce audio ni RF** — El texto de la macro para esa ranura podría estar vacío. Haga clic en **Setup** y verifique el campo de texto junto a la tecla F en cuestión. Consulte [Editar una cadena de macro de CW](edit-a-cw-macro-string.md).
- **La transmisión no se detiene después de presionar Escape** — Haga clic dentro de la ventana de AetherSDR para asegurarse de que tenga el foco del teclado, luego presione Escape nuevamente.
- **Hizo clic en Send pero el búfer no se transmitió** — Si el modo Live estaba activo cuando hizo clic en **Send**, el panel sale del modo Live sin enviar. Haga clic en **Send** una vez más (o presione Enter) para transmitir el búfer.

## Relacionados

- [Editar una cadena de macro de CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío de CW en WPM](change-cw-send-speed-in-wpm.md)
- [Habilitar QSK break-in completo](enable-qsk-full-break-in.md)
- [Enviar un búfer de CW escrito en vivo](send-a-typed-cw-buffer-live.md)
