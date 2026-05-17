# Panel de Grabador de Voz Digital (DVK)

El panel de Grabador de Voz Digital permite grabar y reproducir hasta 8 ranuras de grabador de voz en la radio. Puede renombrar las ranuras, cargar archivos WAV, grabar audio nuevo y activar la reproducción mediante las teclas F o los botones en pantalla.

## Antes de comenzar

- La radio debe estar conectada. El panel DVK requiere una conexión activa con la radio.
- Los atajos de teclado F1-F12 se activan según el modo de la porción seleccionada actualmente, independientemente de si el panel DVK está visible. Esto garantiza que los atajos del DVK sean mutuamente excluyentes con los atajos del panel CWX y evita conflictos entre ellos.

## Comprensión del panel DVK

El panel DVK muestra ocho ranuras (F1 a F8). Cada ranura muestra:

- **Nombre de la ranura** – El nombre predeterminado es "Recording <n>". Puede renombrar cualquier ranura.
- **Duración de la ranura** – Muestra la duración de la grabación en segundos, o "Empty" si no hay ninguna grabación.
- **Barra de progreso** – Muestra el progreso de la reproducción o grabación en vivo.

En la parte inferior del panel, un indicador de estado muestra el estado actual del DVK: "Idle", "Recording" o "Playing".

## Controles

| Control | Descripción |
|---|---|
| **Botones de ranura F1 … F8** | Seleccionan y reproducen la ranura correspondiente. Haga clic derecho para renombrar o cargar un archivo WAV. Haga clic en un botón de ranura que ya se está reproduciendo para detener la reproducción. |
| **● REC** | Inicia la grabación en la ranura seleccionada actualmente. |
| **■ STOP** | Detiene la operación en curso (grabación, reproducción o vista previa). |
| **▶ PLAY** | Reproduce la ranura seleccionada actualmente. |
| **◀ PREV** | Previsualiza la ranura seleccionada a través del altavoz local (sin transmisión). |
| **Editar nombre** | Campo de texto emergente que aparece al hacer clic derecho en una ranura y seleccionar renombrar. |

## Grabar una nueva ranura DVK

1. Seleccione la ranura deseada haciendo clic en el botón **F1** a **F8**.
2. Haga clic en **● REC** para iniciar la grabación.
3. Haga clic en **■ STOP** cuando haya terminado.

La ranura ahora contiene su grabación y muestra su duración.

## Reproducir una ranura de grabador de voz almacenada

1. Haga clic en el **botón de tecla F** de la ranura (por ejemplo, **F1**).
2. Alternativamente, seleccione la ranura haciendo clic en su botón y luego haga clic en **▶ PLAY**.

La transmisión comienza y la barra de progreso avanza. Haga clic en **■ STOP** o presione Escape para detener la reproducción.

## Previsualizar una ranura sin transmitir

1. Seleccione la ranura haciendo clic en su **botón de tecla F**.
2. Haga clic en **◀ PREV**.

La grabación se reproduce solo a través del altavoz local — no se produce transmisión de RF.

## Detener una reproducción en curso

Detener la reproducción finaliza la transmisión inmediatamente y devuelve el DVK al estado "Idle".

1. Haga clic en **■ STOP**.

La reproducción se detiene inmediatamente. El indicador de estado vuelve a "Status: Idle" y la barra de progreso de la ranura se oculta.

**Alternativa — teclado:** Presione Escape. Si no hay un cambio de nombre en línea activo, Escape detiene la reproducción actual.

**Alternativa — botón de tecla F:** Haga clic en el botón de tecla F activo de la ranura (por ejemplo, **F1**). Hacer clic en un botón de tecla F mientras esa ranura se está reproduciendo actúa como un conmutador y detiene la reproducción.

## Renombrar una ranura

1. Haga clic derecho en el **botón de tecla F** de la ranura.
2. Seleccione **Rename** del menú contextual.
3. Escriba el nuevo nombre en el campo de texto que aparece.
4. Presione Enter para confirmar, o presione Escape para cancelar.

## Cargar un archivo WAV

1. Haga clic derecho en el **botón de tecla F** de la ranura.
2. Seleccione **Upload WAV** del menú contextual.
3. Navegue hasta un archivo WAV en su computadora y selecciónelo.
4. El archivo se carga en la radio y reemplaza cualquier grabación existente en esa ranura.

## Atajos de teclado

| Tecla | Función | Notas |
|---|---|---|
| **F1** a **F8** | Seleccionan y reproducen la ranura correspondiente | Los atajos se activan según el modo de la porción activa, independientemente de la visibilidad del panel. Esto evita conflictos con los atajos F1-F12 del panel CWX. |
| **Escape** | Detiene la operación actual, o cancela un cambio de nombre en línea | Si un campo de texto de cambio de nombre está activo, Escape cancela el cambio de nombre en lugar de detener la reproducción. |

## Indicador de estado

El indicador de estado en la parte inferior del panel muestra:

- **Idle** – No hay ninguna operación en curso.
- **Recording** – Se está grabando una ranura actualmente.
- **Playing** – Se está reproduciendo una ranura al aire actualmente.

## Consejos

- **■ STOP** funciona tanto para grabación y vista previa como para reproducción. Un solo botón cubre los tres estados activos.
- Presionar Escape solo detiene la operación activa si no hay un cambio de nombre de ranura abierto actualmente. Si un campo de texto de cambio de nombre está visible, Escape cancela el cambio de nombre en su lugar.
- Los paneles DVK y CWX comparten los atajos F1-F12. Los atajos se habilitan o deshabilitan según el modo de la porción activa para que se activen independientemente de la visibilidad del panel, manteniéndose mutuamente excluyentes para evitar la ambigüedad de atajos en Qt.

## Relacionados

- [Reproducir una ranura de grabador de voz almacenada](play-a-stored-voice-keyer-slot.md)
- [Previsualizar una ranura sin transmitir](preview-a-slot-without-transmitting.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
