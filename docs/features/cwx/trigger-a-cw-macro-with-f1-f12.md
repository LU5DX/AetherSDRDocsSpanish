# Activar una macro de CW con F1–F12

Presione una tecla de función para enviar una cadena de macro de CW predefinida a través del radio sin necesidad de escribirla. Esto es útil para intercambios de concurso, llamadas CQ o cualquier texto que envíe de forma repetida.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en modo CW o CWL. Las teclas de función F1–F12 se ignoran silenciosamente en todos los demás modos.
- Cada macro debe tener texto almacenado en su ranura. Consulte [Editar una cadena de macro de CW](edit-a-cw-macro-string.md) si las ranuras están vacías.

## Pasos

1. Abra el panel CWX. Aparece automáticamente cuando el slice activo está en modo CW o CWL.
2. Presione la tecla de función (F1 a F12) en su teclado que corresponde a la macro que desea enviar. La macro se ejecuta de inmediato.
3. Para detener la transmisión a mitad del envío, presione Escape. Esto limpia el búfer de envío y detiene la salida.

Para enviar una macro usando los botones en pantalla en lugar del teclado:

1. Haga clic en **Setup** en la barra inferior del panel CWX.
2. Haga clic en el botón **F1** a **F12** junto a la macro que desea enviar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| F1 … F12 (teclado) | Envía la macro almacenada para esa tecla de función. Solo activa cuando el modo del slice es CW o CWL. | — | — | `CwxMacro_F1` … `CwxMacro_F12` |
| F1 … F12 (botones en pantalla) | Igual que las teclas del teclado; envía la macro correspondiente. | — | — | `CwxMacro_F1` … `CwxMacro_F12` |
| Speed: | Velocidad de envío de CW en WPM, aplicada a todos los envíos de macro. | 20 WPM | 5–100 WPM | `CwxSpeedWpm` |
| Delay: | Retardo entre macros en milisegundos. | 5 ms | 0–2000 ms | `CwxDelay` |
| QSK | Activa el modo de ruptura total (QSK). | Off | On / Off | `CwxQsk` |

## Consejos

- Los atajos F1–F12 son globales en la aplicación. No es necesario hacer clic dentro del panel CWX primero — las teclas funcionan siempre que AetherSDR tenga el foco y el slice activo esté en modo CW o CWL.
- Presionar Escape durante el envío de una macro es la forma más rápida de cancelar. Dado que el radio alterna rápidamente entre los estados de transmisión y listo durante CW, Escape funciona independientemente del estado de transmisión actual del radio.
- Ajuste **Speed:** en la barra inferior antes de enviar si necesita cambiar el WPM para la sesión actual.

## Solución de problemas

- **Presionar F1–F12 no hace nada** — Confirme que el slice activo está en modo CW o CWL. Los atajos se suprimen en todos los demás modos. Si otra aplicación ha capturado las teclas de función, lleve AetherSDR al primer plano.
- **La macro se envía pero no produce audio ni RF** — El texto de la macro para esa ranura puede estar vacío. Haga clic en **Setup** y verifique el campo de texto junto a la tecla F en cuestión. Consulte [Editar una cadena de macro de CW](edit-a-cw-macro-string.md).
- **La transmisión no se detiene después de presionar Escape** — Haga clic dentro de la ventana de AetherSDR para asegurarse de que tiene el foco del teclado y, a continuación, presione Escape de nuevo.

## Relacionados

- [Editar una cadena de macro de CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío de CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar QSK de ruptura total](enable-qsk-full-break-in.md)
- [Enviar un búfer de CW escrito en tiempo real](send-a-typed-cw-buffer-live.md)
