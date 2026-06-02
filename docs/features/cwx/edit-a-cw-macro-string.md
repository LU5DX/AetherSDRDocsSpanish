# Editar una cadena de macro CW

El panel CWX almacena hasta 12 cadenas de macro, una para cada tecla de función F1 a F12. Esta página muestra cómo abrir el editor de macros y cambiar el texto que se envía al presionar un botón de macro.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel CWX requiere una conexión activa con la radio.
- El slice activo debe usar modo CW, CWL o CWU, o el panel CWX ya debe estar abierto en la ventana principal.

## Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior. El panel cambia a la vista del editor de macros.
2. Localice la fila de la macro que desea modificar. Cada fila está etiquetada como **F1** a **F12**.
3. Haga clic dentro del campo de texto junto a la etiqueta de la tecla de función.
4. Edite el texto de la macro. El campo acepta texto plano y accesos directos de prosignas. Consulte la leyenda de prosignas que se muestra en la vista Setup para conocer los caracteres abreviados disponibles (`=`, `+`, `(`, `&`, `$`).
5. Presione Tab o haga clic en otro campo. El nuevo texto se guarda inmediatamente en la configuración correspondiente (`CwxMacro_F1` a `CwxMacro_F12`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| **F1** … **F12** campos de texto de macro | Almacena el texto CW enviado al presionar esa tecla de función | `CwxMacro_F1` … `CwxMacro_F12` | — | Texto plano con accesos directos de prosignas |
| **Delay:** | Retardo entre macros en milisegundos | `CwxDelay` | 5 ms | 0 – 2000 ms |
| **QSK** | Activa QSK (ruptura total) | `CwxQsk` | — | On / Off |
| **Speed:** | Velocidad de envío CW | `CwxSpeedWpm` | 20 WPM | 5 – 100 WPM |

## Consejos

- Para enviar una macro inmediatamente después de editarla, haga clic en **Send** en la barra inferior para volver a la vista de envío y luego presione la tecla F correspondiente.
- Presionar **Setup** mientras **Live** está activo desactiva el envío en vivo y regresa a la vista de envío antes de mostrar el editor de macros. Cualquier texto ya ingresado carácter por carácter no se retransmite.
- Presionar Escape cancela cualquier transmisión CW en curso sin afectar el texto de macro almacenado.

## Cómo interactúan Send y Live (v0.9.2.1)

El comportamiento del botón **Send** cambió en la v0.9.2.1.

- Si **Live** está **desactivado** al hacer clic en **Send**, el panel envía el búfer escrito inmediatamente, como antes.
- Si **Live** está **activado** al hacer clic en **Send**, el panel primero desactiva el envío en vivo y regresa a la vista de envío normal. El búfer **no** se retransmite. Esto evita que los caracteres ya enviados en vivo, uno a la vez, se envíen nuevamente.

El botón **Live** ahora es un conmutador. Su estado marcado refleja el estado de envío en vivo que mantiene el modelo de radio, por lo que el botón permanece sincronizado si el estado cambia desde fuera del panel (por ejemplo, desde una macro o un comando remoto).

## Comportamiento de los accesos directos de las teclas de función (v26.5.2.1)

El panel CWX registra accesos directos a nivel de aplicación para F1 a F12 y Escape. Estos accesos directos se habilitan y deshabilitan mediante la ventana principal según el modo de operación del slice activo, no según la visibilidad del panel.

- Cuando el slice activo usa modo CW, CWL o CWU, los accesos directos están habilitados.
- Cuando el slice activo usa cualquier otro modo (como SSB o AM para el panel DVK), los accesos directos están deshabilitados.
- Los accesos directos se activan independientemente de si el panel CWX está visible, siempre que el slice activo esté en modo CW.
- Esto evita conflictos de acceso directo con el panel DVK, que registra su propio conjunto de accesos directos F1 a F12 para macros de voz.

## Menú contextual en burbujas del historial de envío (v26.5.2.1)

Haga clic derecho en cualquier burbuja del área de desplazamiento del historial de envío para abrir un menú contextual con dos opciones:

- **Resend** — Envía nuevamente todo el texto de esa burbuja. La burbuja reaparece al final del historial como una nueva entrada con la marca de tiempo actual.
- **Clear History** — Elimina todas las burbujas del historial del área de desplazamiento. El espaciador en la parte inferior del diseño del historial permanece.

## Visualización de transmisión abortada (v26.6.1)

Al presionar Escape durante una transmisión CW, la burbuja de esa transmisión en el área de desplazamiento del historial de envío ahora muestra un tachado visual en la parte no enviada del texto.

- La parte enviada del texto aparece en estilo normal.
- La parte no enviada aparece con una línea de tachado.

Esto deja claro qué caracteres se transmitieron realmente antes del aborto.

## Relacionados

- [Activar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Consultar los accesos directos de caracteres de prosignas](look-up-the-prosign-character-shortcuts.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar QSK de ruptura total](enable-qsk-full-break-in.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
