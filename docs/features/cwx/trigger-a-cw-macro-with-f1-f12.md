# Activar una macro CW con F1–F12

Presione una tecla de función para enviar una cadena CW predefinida sin necesidad de escribirla. Cada uno de los doce slots de tecla F almacena una macro; al presionar la tecla, se transmite esa macro a la velocidad actual.

## Antes de comenzar

- AetherSDR debe estar conectado al radio.
- El slice activo debe estar en modo CW o CWL. Las macros de teclas de función no se activan en otros modos.
- Cada slot de macro debe contener texto. Consulte [Editar una cadena de macro CW](edit-a-cw-macro-string.md) si los slots están vacíos.

## Pasos

1. Abra el panel CWX. Aparece en el área de la ventana principal cuando el slice activo está en modo CW o CWL.
2. Presione **F1** hasta **F12** en el teclado. AetherSDR envía la macro almacenada en el slot correspondiente a la velocidad indicada en **Speed:**.
3. Para detener la transmisión antes de que finalice, presione **Escape**. Esto vacía el búfer de envío de inmediato.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| **F1** … **F12** (botones de macro) | Hacer clic en un botón del panel CWX envía esa macro. Presionar la tecla de función correspondiente en el teclado produce el mismo resultado. | `CwxMacro_F1` … `CwxMacro_F12` | *(vacío)* | Cualquier texto codificable en CW o prosignos |
| **Speed:** | Velocidad de envío CW en WPM, aplicada a todas las transmisiones de macro. | `CwxSpeedWpm` | 20 WPM | 5–100 WPM |
| **Delay:** | Retardo entre macros en milisegundos. | `CwxDelay` | 5 ms | 0–2000 ms |
| **QSK** | Habilita el QSK de ruptura total. | `CwxQsk` | off | on / off |

## Consejos

- Los atajos de tecla F son de ámbito global en la aplicación. El panel CWX no necesita tener el foco para que las teclas se activen, pero el slice activo debe estar en modo CW o CWL.
- Presionar **Escape** durante la transmisión de una macro vacía el búfer. Dado que el radio alterna entre transmitir y estar listo durante cada dit y dah, la cancelación toma efecto en el siguiente intervalo — generalmente dentro de un elemento.
- También puede hacer clic directamente en los botones **F1** … **F12** dentro del panel CWX en lugar de usar el teclado.

## Resolución de problemas

- **Presionar F1–F12 no hace nada** — Confirme que el slice activo está en modo CW o CWL. Las macros quedan suprimidas en todos los demás modos (SSB, AM, FM, etc.).
- **La macro se activa pero no transmite nada** — El slot de macro está vacío. Abra la vista Setup e ingrese texto en el editor de macro correspondiente. Consulte [Editar una cadena de macro CW](edit-a-cw-macro-string.md).
- **Velocidad incorrecta** — Ajuste **Speed:** en la barra inferior del panel CWX. El valor se conserva como `CwxSpeedWpm`.

## Temas relacionados

- [Editar una cadena de macro CW](edit-a-cw-macro-string.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Habilitar QSK de ruptura total](enable-qsk-full-break-in.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
- [Consultar los atajos de caracteres de prosigno](look-up-the-prosign-character-shortcuts.md)
