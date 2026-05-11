# Panel de Controlador de Voz Digital (DVK)

El panel del Controlador de Voz Digital graba y reproduce hasta 8 ranuras de controlador de voz en la radio. Puede renombrar ranuras, cargar archivos WAV, grabar nuevo audio y activar la reproducción mediante teclas F o botones en pantalla.

## Antes de comenzar

- La radio debe estar conectada. El panel DVK requiere una conexión activa con la radio.
- El panel DVK debe estar visible en la ventana principal para que los atajos de teclado funcionen. Cuando está oculto, los atajos de las teclas F se deshabilitan automáticamente para evitar conflictos con el panel CWX.

## Cómo entender el panel DVK

El panel DVK muestra ocho ranuras (F1 a F8). Cada ranura muestra:

- **Nombre de la ranura** – El nombre predeterminado es "Recording <n>". Puede renombrar cualquier ranura.
- **Duración de la ranura** – Muestra la duración de la grabación en segundos, o "Empty" si no existe ninguna grabación.
- **Barra de progreso** – Muestra el progreso de reproducción o grabación en vivo.

En la parte inferior del panel, un indicador de estado muestra el estado actual del DVK: "Idle", "Recording" o "Playing".

## Controles

| Control | Descripción |
|---|---|
| **Botones de ranura F1 … F8** | Seleccione y reproduzca la ranura correspondiente. Haga clic derecho para renombrar o cargar un archivo WAV. Haga clic en un botón de ranura que ya se esté reproduciendo para detener la reproducción. |
| **● REC** | Inicia la grabación en la ranura seleccionada actualmente. |
| **■ STOP** | Detiene la operación actual (grabación, reproducción o vista previa). |
| **▶ PLAY** | Reproduce la ranura seleccionada actualmente. |
| **◀ PREV** | Previsualiza la ranura seleccionada a través del altavoz local (sin transmisión). |
| **Campo de renombrar** | Campo de texto en línea que aparece al hacer clic derecho en una ranura y elegir renombrar. |

## Grabar una nueva ranura DVK

1. Seleccione la ranura deseada haciendo clic en el botón **F1** a **F8**.
2. Haga clic en **● REC** para iniciar la grabación.
3. Haga clic en **■ STOP** cuando haya terminado.

La ranura ahora contiene su grabación y muestra su duración.

## Reproducir una ranura de controlador de voz almacenada

1. Haga clic en el **botón de tecla F** de la ranura (por ejemplo, **F1**).
2. Alternativamente, seleccione la ranura haciendo clic en su botón, luego haga clic en **▶ PLAY**.

La transmisión comienza y la barra de progreso avanza. Haga clic en **■ STOP** o presione Escape para detener la reproducción.

## Previsualizar una ranura sin transmitir

1. Seleccione la ranura haciendo clic en su **botón de tecla F**.
2. Haga clic en **◀ PREV**.

La grabación se reproduce solo a través de su altavoz local; no se produce transmisión de RF.

## Detener una reproducción en curso

Detener la reproducción finaliza la transmisión inmediatamente y devuelve el DVK al estado Idle.

1. Haga clic en **■ STOP**.

La reproducción se detiene de inmediato. El indicador de estado vuelve a "Status: Idle" y la barra de progreso de la ranura se oculta.

**Alternativa con teclado:** Presione Escape. Si no hay un renombrado en línea activo, Escape detiene la reproducción actual.

**Alternativa con botón de tecla F:** Haga clic en el botón de tecla F activo de la ranura (por ejemplo, **F1**). Hacer clic en un botón de tecla F mientras esa ranura se está reproduciendo actúa como un conmutador y detiene la reproducción.

## Renombrar una ranura

1. Haga clic derecho en el **botón de tecla F** de la ranura.
2. Seleccione **Rename** en el menú contextual.
3. Escriba el nuevo nombre en el campo de texto que aparece.
4. Presione Enter para confirmar, o presione Escape para cancelar.

## Cargar un archivo WAV

1. Haga clic derecho en el **botón de tecla F** de la ranura.
2. Seleccione **Upload WAV** en el menú contextual.
3. Navegue y seleccione un archivo WAV en su computadora.
4. El archivo se carga en la radio y reemplaza cualquier grabación existente en esa ranura.

## Atajos de teclado

| Tecla | Función | Notas |
|---|---|---|
| **F1** a **F8** | Seleccionar y reproducir la ranura correspondiente | Los atajos solo están activos cuando el panel DVK está visible. Cuando está oculto, estas teclas están disponibles para otros paneles (como el panel CWX). |
| **Escape** | Detener la operación actual o cancelar un renombrado en línea | Si un campo de texto de renombrado está activo, Escape cancela el renombrado en lugar de detener la reproducción. |

## Indicador de estado

El indicador de estado en la parte inferior del panel muestra:

- **Idle** – No hay ninguna operación en curso.
- **Recording** – Se está grabando una ranura actualmente.
- **Playing** – Se está reproduciendo una ranura al aire actualmente.

## Consejos

- **■ STOP** funciona tanto para grabación y vista previa como para reproducción. Un solo botón cubre los tres estados activos.
- Presionar Escape solo detiene la operación activa si no hay un renombrado de ranura abierto. Si un campo de texto de renombrado está visible, Escape cancela el renombrado en su lugar.
- Los paneles DVK y CWX comparten atajos de teclas F, pero son mutuamente excluyentes en la vista de divisor. Los atajos del panel se habilitan automáticamente cuando el panel se muestra y se deshabilitan cuando está oculto, evitando conflictos.

## Relacionados

- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
