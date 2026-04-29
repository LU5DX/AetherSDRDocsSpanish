# Editar una cadena de macro CW

El panel CWX almacena hasta 12 cadenas de macro, una para cada tecla de función F1 a F12. Esta página muestra cómo abrir el editor de macros y cambiar el texto que se envía al presionar un botón de macro.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel CWX requiere una conexión de radio activa.
- El slice activo debe usar el modo CW, CWL o CWU, o el panel CWX ya debe estar abierto en la ventana principal.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior. El panel cambia a la vista del editor de macros.
2. Localice la fila correspondiente a la macro que desea cambiar. Cada fila está etiquetada **F1** a **F12**.
3. Haga clic dentro del campo de texto junto a la etiqueta de la tecla de función.
4. Edite el texto de la macro. El campo acepta texto plano y atajos de prosigno. Consulte la leyenda de prosignos que se muestra en la vista Setup para conocer los caracteres de atajo disponibles (`=`, `+`, `(`, `&`, `$`).
5. Presione Tab o haga clic en otro campo. El nuevo texto se guarda inmediatamente en la configuración correspondiente (`CwxMacro_F1` a `CwxMacro_F12`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| Campos de texto de macro **F1** … **F12** | Almacena el texto CW que se envía al presionar esa tecla de función | `CwxMacro_F1` … `CwxMacro_F12` | — | Texto plano con atajos de prosigno |
| **Delay:** | Retardo entre macros en milisegundos | `CwxDelay` | 5 ms | 0 – 2000 ms |
| **QSK** | Activa QSK (ruptura total) | `CwxQsk` | — | On / Off |
| **Speed:** | Velocidad de envío CW | `CwxSpeedWpm` | 20 WPM | 5 – 100 WPM |

## Consejos

- Para enviar una macro inmediatamente después de editarla, haga clic en **Send** en la barra inferior para volver a la vista de envío y luego presione la tecla F correspondiente.
- Si presiona **Setup** mientras **Live** está activo, se desactiva el envío en vivo y se regresa a la vista de envío antes de mostrar el editor de macros. El texto que ya fue tecleado carácter por carácter no se retransmite.
- Presionar Escape interrumpe cualquier transmisión CW en curso sin afectar el texto de las macros almacenadas.

## Cómo interactúan Send y Live (v0.9.2.1)

El comportamiento del botón **Send** cambió en v0.9.2.1.

- Si **Live** está **desactivado** cuando hace clic en **Send**, el panel envía el búfer escrito de forma inmediata, como antes.
- Si **Live** está **activado** cuando hace clic en **Send**, el panel primero desactiva el envío en vivo y regresa a la vista de envío normal. El búfer **no** se retransmite. Esto evita que los caracteres que ya fueron tecleados en vivo, uno a la vez, se envíen nuevamente.

El botón **Live** ahora es un interruptor de alternancia. Su estado marcado refleja el estado de envío en vivo que mantiene el modelo de radio, por lo que el botón permanece sincronizado si el estado cambia desde fuera del panel (por ejemplo, desde una macro o un comando remoto).

## Relacionados

- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Consultar los atajos de caracteres de prosigno](look-up-the-prosign-character-shortcuts.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar QSK de ruptura total](enable-qsk-full-break-in.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
