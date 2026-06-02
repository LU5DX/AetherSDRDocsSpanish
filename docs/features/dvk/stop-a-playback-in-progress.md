# Panel del Pulsador de Voz Digital (DVK)

El panel del Pulsador de Voz Digital graba y reproduce hasta 8 ranuras de pulsador de voz en la radio. Puede renombrar ranuras, cargar archivos WAV, grabar nuevo audio e iniciar la reproducción mediante las teclas F o los botones en pantalla.

## Antes de comenzar

- La radio debe estar conectada. El panel DVK requiere una conexión activa con la radio.
- Los atajos de teclado F1-F12 están activos según el modo de la división seleccionada actualmente, independientemente de si el panel DVK está visible. Esto asegura que los atajos DVK sean mutuamente excluyentes con los atajos del panel CWX y evita conflictos entre atajos.

## Cómo entender el panel DVK

El panel DVK muestra ocho ranuras (F1 a F8). Cada ranura muestra:

- **Nombre de la ranura** – El nombre predeterminado es "Recording <n>". Puede renombrar cualquier ranura.
- **Duración de la ranura** – Muestra la duración de la grabación en segundos, o "Vacía" si no existe ninguna grabación.
- **Barra de progreso** – Muestra el progreso de la reproducción o grabación en vivo.

En la parte inferior del panel, un indicador de estado muestra el estado actual del DVK: "Inactivo", "Grabando" o "Reproduciendo".

## Controles

| Control | Descripción |
|---|---|
| **Botones de ranura F1 … F8** | Selecciona y reproduce la ranura correspondiente. Haga clic derecho para renombrar o cargar un archivo WAV. Haga clic en un botón de ranura que ya se esté reproduciendo para detenerla. |
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

## Reproducir una ranura de pulsador de voz almacenada

1. Haga clic en el **botón de tecla F** de la ranura (por ejemplo, **F1**).
2. Alternativamente, seleccione la ranura haciendo clic en su botón, luego haga clic en **▶ PLAY**.

La transmisión comienza y la barra de progreso avanza. Haga clic en **■ STOP** o presione Escape para detener la reproducción.

## Previsualizar una ranura sin transmitir

1. Seleccione la ranura haciendo clic en su **botón de tecla F**.
2. Haga clic en **◀ PREV**.

La grabación se reproduce solo a través de su altavoz local; no se produce ninguna transmisión de RF.

## Detener una reproducción en curso

Detener la reproducción interrumpe la transmisión inmediatamente y devuelve el DVK al estado Inactivo.

1. Haga clic en **■ STOP**.

La reproducción se detiene de inmediato. El indicador de estado vuelve a "Estado: Inactivo" y la barra de progreso de la ranura se oculta.

**Alternativa – teclado:** Presione Escape. Si no hay una edición de nombre en línea activa, Escape detiene la reproducción actual.

**Alternativa – botón de tecla F:** Haga clic en el botón de tecla F activo de la ranura (por ejemplo, **F1**). Hacer clic en un botón de tecla F mientras esa ranura se está reproduciendo actúa como un conmutador y detiene la reproducción.

## Renombrar una ranura

1. Haga clic derecho en el **botón de tecla F** de la ranura.
2. Seleccione **Rename** en el menú contextual.
3. Escriba el nuevo nombre en el campo de texto que aparece.
4. Presione Enter para confirmar, o presione Escape para cancelar.

## Cargar o descargar un archivo WAV

1. Haga clic derecho en el **botón de tecla F** de la ranura.
2. Seleccione **Upload WAV** para cargar un archivo WAV desde su computadora a la radio. Navegue hasta y seleccione un archivo WAV. El archivo reemplaza cualquier grabación existente en esa ranura.
3. Seleccione **Download WAV** para descargar el archivo WAV de la ranura desde la radio a su computadora. Navegue hasta una carpeta de destino y guarde el archivo. El archivo se descarga en formato WAV con el nombre de la ranura.

## Atajos de teclado

| Tecla | Función | Notas |
|---|---|---|
| **F1** a **F8** | Selecciona y reproduce la ranura correspondiente | Los atajos están activos según el modo de la división activa, independientemente de la visibilidad del panel. Esto evita conflictos con los atajos F1-F12 del panel CWX. |
| **Escape** | Detiene la operación actual, o cancela una edición de nombre en línea | Si un campo de texto de renombre está activo, Escape cancela el renombre en lugar de detener la reproducción. |

## Indicador de estado

El indicador de estado en la parte inferior del panel muestra:

- **Inactivo** – No hay ninguna operación en curso.
- **Grabando** – Una ranura se está grabando actualmente.
- **Reproduciendo** – Una ranura se está reproduciendo actualmente al aire.

## Consejos

- El botón **■ STOP** funciona para grabación y vista previa, así como para reproducción. Un solo botón cubre los tres estados activos.
- Presionar Escape solo detiene la operación activa si no hay un renombre de ranura abierto actualmente. Si un campo de texto de renombre está visible, Escape cancela el renombre en su lugar.
- Los paneles DVK y CWX comparten los atajos F1-F12. Los atajos se habilitan o deshabilitan según el modo de la división activa, de modo que se activen independientemente de la visibilidad del panel, mientras permanecen mutuamente excluyentes para evitar la ambigüedad de atajos de Qt.

## Relacionado

- [Reproducir una ranura de pulsador de voz almacenada](play-a-stored-voice-keyer-slot.md)
- [Previsualizar una ranura sin transmitir](preview-a-slot-without-transmitting.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
