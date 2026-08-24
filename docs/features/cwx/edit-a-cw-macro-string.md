# Panel CWX

El panel CWX proporciona una interfaz completa para operar en CW. Le permite escribir texto CW, enviarlo carácter por carácter en vivo, almacenar y enviar hasta 12 macros de teclas F, controlar la velocidad y el QSK, y ver un historial desplazable de transmisiones enviadas con retroalimentación visual para envíos abortados.

## Cómo abrir el panel CWX

1. Asegúrese de que AetherSDR esté conectado a la radio.
2. Abra el panel CWX desde el menú de la ventana principal o la barra de herramientas.

## Vistas del panel

El panel CWX tiene tres vistas, seleccionadas mediante los botones en la parte inferior del panel:

- **Send (vista)** — Muestra el área de envío en vivo con el historial y el campo de texto.
- **Live (vista)** — Muestra la vista de envío en vivo para enviar carácter por carácter.
- **Setup (vista)** — Muestra el editor de macros y la configuración de QSK.

## Controles

### Velocidad

- **Control:** Cuadro de giro de velocidad
- **Clave de ajuste:** `CwxSpeedWpm`
- **Comportamiento:** Establece la velocidad de envío CW en WPM.

### Historial de envíos

- **Control:** Indicador de desplazamiento del historial de envíos
- **Comportamiento:** Muestra los búferes de envío anteriores con resaltado de caracteres. Cada entrada aparece como una burbuja de chat con una marca de tiempo.

### Área de texto de envío

- **Control:** Campo de texto
- **Comportamiento:** Escriba caracteres CW. Pulse Enter para enviar el búfer.

### Macros F1 a F12

- **Controles:** Botones pulsadores (en las vistas Send y Live) y campos de texto (en la vista Setup)
- **Claves de ajuste:** `CwxMacro_F1` a `CwxMacro_F12`
- **Comportamiento:** En las vistas Send y Live, al pulsar una tecla F se envía la macro preescrita. En la vista Setup, los campos de texto permiten editar el contenido de la macro.

### Retardo

- **Control:** Cuadro de giro
- **Clave de ajuste:** `CwxDelay`
- **Comportamiento:** Retardo entre macros en milisegundos.
- **Rango válido:** 0 – 2000 ms
- **Valor predeterminado:** 5 ms

### QSK

- **Control:** Botón de alternancia
- **Clave de ajuste:** `CwxQsk`
- **Comportamiento:** Activa el QSK (full break-in).

### Leyenda de prosignos

- **Control:** Indicador
- **Comportamiento:** Muestra los atajos para los prosignos CW comunes: `=`, `+`, `(`, `&`, `$`.

## Edición de una cadena de macro CW

El panel CWX almacena hasta 12 cadenas de macro, una para cada tecla de función F1 a F12. Esta sección muestra cómo abrir el editor de macros y cambiar el texto que se envía al pulsar un botón de macro.

### Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel CWX requiere una conexión activa con la radio.
- El slice de TX debe usar un modo CW (CW, CWL o CWU), o el panel CWX ya debe estar abierto en la ventana principal.

### Pasos

1. En el panel CWX, haga clic en **Setup** en la barra inferior. El panel cambia a la vista del editor de macros.
2. Localice la fila de la macro que desea cambiar. Cada fila está etiquetada como **F1** a **F12**.
3. Haga clic dentro del campo de texto junto a la etiqueta de la tecla de función.
4. Edite el texto de la macro. El campo acepta texto plano y atajos de prosignos. Consulte la leyenda de prosignos que se muestra en la vista Setup para conocer los caracteres de atajo disponibles (`=`, `+`, `(`, `&`, `$`).
5. Pulse Tab o haga clic en otro campo. El nuevo texto se guarda inmediatamente en la clave correspondiente (`CwxMacro_F1` a `CwxMacro_F12`).

### Consejos

- Para enviar una macro inmediatamente después de editarla, haga clic en **Send** en la barra inferior para volver a la vista de envío y luego pulse la tecla F correspondiente.
- Pulse **Setup** mientras **Live** está activo desactiva el envío en vivo y vuelve a la vista de envío antes de mostrar el editor de macros. El texto ya enviado carácter por carácter no se retransmite.
- Pulsar Escape aborta cualquier transmisión CW en curso sin afectar el texto de las macros almacenadas.

## Comportamiento de los atajos de teclas de función

El panel CWX registra atajos de toda la aplicación para F1 a F12 y Escape. Estos atajos se activan y desactivan mediante la ventana principal según el modo de funcionamiento del slice de TX, no según la visibilidad del panel.

- Cuando el slice de TX usa un modo CW (CW, CWL o CWU), los atajos están activados.
- Cuando el slice de TX usa cualquier otro modo (como SSB o AM para el panel DVK), los atajos están desactivados.
- Los atajos se activan independientemente de si el panel CWX está visible, siempre que el slice de TX esté en modo CW.
- Esto evita conflictos de atajos con el panel DVK, que registra su propio conjunto de atajos F1 a F12 para macros de voz.

## Interacción entre Send y Live

- Si **Live** está desactivado al hacer clic en **Send**, el panel envía el búfer escrito inmediatamente.
- Si **Live** está activado al hacer clic en **Send**, el panel primero desactiva el envío en vivo y vuelve a la vista de envío normal. El búfer no se retransmite. Esto evita que los caracteres ya enviados en vivo, uno a la vez, se envíen nuevamente.
- El botón **Live** es de alternancia. Su estado marcado refleja el estado de envío en vivo que mantiene el modelo de la radio, de modo que el botón permanece sincronizado si el estado cambia desde fuera del panel (por ejemplo, desde una macro o un comando remoto).

## Menú contextual en las burbujas del historial de envíos

Haga clic derecho en cualquier burbuja del área de desplazamiento del historial de envíos para abrir un menú contextual con dos opciones:

- **Resend** — Vuelve a enviar todo el texto de esa burbuja. La burbuja reaparece al final del historial como una nueva entrada con la marca de tiempo actual.
- **Clear History** — Elimina todas las burbujas del historial del área de desplazamiento. El espaciador en la parte inferior del diseño del historial permanece.

## Visualización de transmisión abortada

Al pulsar Escape durante una transmisión CW, la burbuja correspondiente a esa transmisión en el área de desplazamiento del historial de envíos muestra un tachado visual en la parte no enviada del texto.

- La parte enviada del texto aparece en estilo normal.
- La parte no enviada aparece con una línea de tachado.

Esto deja claro qué caracteres se transmitieron realmente antes del aborto.

## Relacionado

- [Disparar una macro CW con F1–F12](trigger-a-cw-macro-with-f1-f12.md)
- [Consultar los atajos de caracteres de prosignos](look-up-the-prosign-character-shortcuts.md)
- [Cambiar la velocidad de envío CW en WPM](change-cw-send-speed-in-wpm.md)
- [Activar QSK full break-in](enable-qsk-full-break-in.md)
- [Enviar un búfer CW escrito en vivo](send-a-typed-cw-buffer-live.md)
