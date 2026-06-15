# Panel de la Grabadora de Voz Digital (DVK)

El panel de la Grabadora de Voz Digital (DVK) graba y reproduce hasta 8 ranuras de grabación de voz en la radio. Puede renombrar ranuras, cargar archivos WAV, grabar nuevo audio e iniciar la reproducción mediante teclas F o botones en pantalla.

## Antes de comenzar

- La radio debe estar conectada. El panel DVK requiere una conexión activa con la radio.
- Los atajos de teclado F1-F12 están activos según el modo de la franja seleccionada actualmente, independientemente de la visibilidad del panel DVK. Esto garantiza que los atajos del DVK sean mutuamente excluyentes con los atajos del panel CWX y evita conflictos entre atajos.

## Cómo entender el panel DVK

El panel DVK muestra ocho ranuras (F1 a F8). Cada ranura muestra:

- **Nombre de la ranura** – El nombre predeterminado es "Recording <n>". Puede renombrar cualquier ranura.
- **Duración de la ranura** – Muestra la duración de la grabación en segundos, o "Empty" si no hay ninguna grabación.
- **Barra de progreso** – Muestra el progreso de la reproducción o grabación en vivo.

En la parte inferior del panel, un indicador de estado muestra el estado actual del DVK: "Idle", "Recording" o "Playing".

## Controles

| Control | Descripción |
|---|---|
| **Botones de ranura F1 … F8** | Selecciona y reproduce la ranura correspondiente. Haga clic derecho para renombrar o cargar un archivo WAV. Haga clic en un botón de ranura que ya se esté reproduciendo para detener la reproducción. |
| **● REC** | Inicia la grabación en la ranura seleccionada actualmente. |
| **■ STOP** | Detiene la operación actual (grabación, reproducción o vista previa). |
| **▶ PLAY** | Reproduce la ranura seleccionada actualmente. |
| **◀ PREV** | Previsualiza la ranura seleccionada a través del altavoz local (sin transmisión). |
| **Editar nombre** | Campo de texto en línea que aparece al hacer clic derecho en una ranura y seleccionar renombrar. |

## Grabar una nueva ranura DVK

1. Seleccione la ranura deseada haciendo clic en el botón **F1** a **F8**.
2. Haga clic en **● REC** para comenzar a grabar.
3. Haga clic en **■ STOP** cuando haya terminado.

La ranura ahora contiene su grabación y muestra su duración.

Si la radio rechaza la solicitud de grabación, el indicador de estado muestra un mensaje de error y el botón REC vuelve a su estado normal.

## Reproducir una ranura de voz almacenada

1. Haga clic en el **botón F** de la ranura (por ejemplo, **F1**).
2. Alternativamente, seleccione la ranura haciendo clic en su botón y luego haga clic en **▶ PLAY**.

La transmisión comienza y la barra de progreso avanza. Haga clic en **■ STOP** o presione Escape para detener la reproducción.

## Previsualizar una ranura sin transmitir

1. Seleccione la ranura haciendo clic en su **botón F**.
2. Haga clic en **◀ PREV**.

La grabación se reproduce solo a través del altavoz local, sin transmisión de RF.

## Detener una reproducción en curso

Al detener la reproducción, la transmisión se interrumpe inmediatamente y el DVK vuelve al estado Idle.

1. Haga clic en **■ STOP**.

La reproducción se detiene de inmediato. El indicador de estado vuelve a "Status: Idle" y la barra de progreso de la ranura se oculta.

**Alternativa — teclado:** Presione Escape. Si no hay un campo de cambio de nombre activo, Escape detiene la reproducción actual.

**Alternativa — botón F:** Haga clic en el botón F activo de la ranura (por ejemplo, **F1**). Hacer clic en un botón F mientras esa ranura se está reproduciendo actúa como un conmutador y detiene la reproducción.

## Renombrar una ranura

1. Haga clic derecho en el **botón F** de la ranura.
2. Seleccione **Rename** del menú contextual.
3. Escriba el nuevo nombre en el campo de texto que aparece.
4. Presione Enter para confirmar o Escape para cancelar.

## Cargar o descargar un archivo WAV

1. Haga clic derecho en el **botón F** de la ranura.
2. Seleccione **Upload WAV** para cargar un archivo WAV desde su computadora a la radio. Navegue hasta y seleccione un archivo WAV. El archivo reemplaza cualquier grabación existente en esa ranura.
3. Seleccione **Download WAV** para descargar el archivo WAV de la ranura desde la radio a su computadora. Navegue hasta una carpeta de destino y guarde el archivo. El archivo se descarga en formato WAV con el nombre de la ranura.

## Atajos de teclado

| Tecla | Función | Notas |
|---|---|---|
| **F1** a **F8** | Selecciona y reproduce la ranura correspondiente | Los atajos están activos según el modo de la franja activa, independientemente de la visibilidad del panel. Esto evita conflictos con los atajos F1-F12 del panel CWX. |
| **Escape** | Detiene la operación actual o cancela un cambio de nombre en línea | Si un campo de texto de cambio de nombre está activo, Escape cancela el cambio de nombre en lugar de detener la reproducción. |

## Indicador de estado

El indicador de estado en la parte inferior del panel muestra:

- **Idle** – No hay ninguna operación en curso.
- **Recording** – Se está grabando una ranura actualmente.
- **Playing** – Una ranura se está reproduciendo al aire actualmente.
- **Mensaje de error** – Si la radio rechaza un comando (por ejemplo, una solicitud de grabación), la pantalla muestra "Status: <verbo> (slot <n>) failed — <mensaje>" durante la duración de ese evento.

## Consejos

- **■ STOP** funciona tanto para grabación y vista previa como para reproducción. Un solo botón cubre los tres estados activos.
- Presionar Escape solo detiene la operación activa si no hay un cambio de nombre de ranura abierto actualmente. Si un campo de texto de cambio de nombre está visible, Escape cancela el cambio de nombre.
- Los paneles DVK y CWX comparten atajos F1-F12. Los atajos se habilitan o deshabilitan según el modo de la franja activa para que se activen independientemente de la visibilidad del panel, mientras se mantienen mutuamente excluyentes para evitar ambigüedad en los atajos de Qt.
- Si un comando como iniciar una grabación es rechazado por la radio, el indicador de estado muestra un mensaje de error específico y todos los botones vuelven a su estado visual correcto.

## Relacionado

- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
