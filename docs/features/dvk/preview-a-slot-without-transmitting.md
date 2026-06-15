# Vista previa de un espacio sin transmitir

Use esta página para probar un espacio DVK a través de su altavoz local antes de enviarlo al aire. La vista previa le permite confirmar el contenido y el nivel de audio sin activar el transmisor.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK requiere una conexión activa con la radio.
- El espacio que desea previsualizar debe contener una grabación. Los espacios que muestran "Empty" no se pueden previsualizar.

## Pasos

1. Abra el panel Digital Voice Keyer en el área central de MainWindow.
2. Haga clic en la fila del espacio (F1 a F8) que desea previsualizar. La fila seleccionada se resalta con un borde azul.
3. Haga clic en ◀ PREV.
4. Escuche el audio a través de su altavoz local. La barra de progreso del espacio se vuelve azul y avanza durante la reproducción.
5. Cuando el espacio termine, la reproducción se detiene automáticamente y el estado vuelve a "Status: Idle". Para detener antes, haga clic en ■ STOP o presione Escape.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de espacio F1 … F8 | Selecciona el espacio. Si el espacio se está reproduciendo al aire, al hacer clic nuevamente se detiene. Haga clic derecho para renombrar o subir un archivo WAV. | No activa la vista previa. |
| Etiquetas de nombre de espacio | Muestra el nombre de cada espacio. | El nombre predeterminado es "Recording \<n\>". |
| Etiquetas de duración de espacio | Muestra la duración de la grabación o "Empty". | Un espacio que muestra "Empty" no se puede previsualizar. |
| Barras de progreso de espacio | Muestra el progreso de reproducción en azul durante la vista previa. | Ocultas cuando está inactivo. |
| ● REC | Inicia la grabación en el espacio seleccionado. | Si la radio rechaza el comando de grabación, el botón se libera visualmente y el área de estado muestra un mensaje de error. |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | También se activa con Escape. |
| ▶ PLAY | Reproduce el espacio seleccionado al aire. | No es vista previa. |
| ◀ PREV | Inicia la vista previa del espacio seleccionado a través del altavoz local. Haga clic nuevamente para detener. | No transmite. |
| Edición de nombre | Cambio de nombre en línea de un espacio activado mediante el menú contextual. | |
| Status: Idle / Recording / Playing | Muestra el estado actual del DVK en la parte inferior del panel. | Si un comando de grabación falla, muestra un mensaje de error como "Status: Rec (slot 3) failed — <razón>". |

## Atajos de teclado

El panel DVK registra los atajos de teclado F1–F12 y Escape. La disponibilidad de atajos está controlada por el modo de operación del slice activo, no por la visibilidad del panel. Esto garantiza que los atajos DVK estén habilitados solo cuando el slice activo esté en un modo compatible, y sean mutuamente excluyentes con los atajos F1–F12 del panel CVX para evitar conflictos de teclas.

| Tecla | Acción |
|---|---|
| F1–F12 | Selecciona y reproduce el espacio correspondiente (F1 = espacio 1, F2 = espacio 2, etc.). Los espacios más allá de F8 (F9–F12) no son funcionales en la mayoría de las configuraciones. |
| Escape | Detiene la grabación, reproducción o vista previa. Si hay una edición de nombre activa, cancela el cambio de nombre. |

## Consejos

- Si hace clic en ◀ PREV en un espacio que ya está en vista previa, detiene la vista previa.
- Presionar Escape detiene una vista previa activa sin usar el mouse.
- Los botones F-key y los atajos de teclado F1–F12 activan la reproducción al aire, no la vista previa. Use ◀ PREV específicamente cuando no desee transmitir.
- Haga clic derecho en un botón de espacio para renombrarlo o subir un archivo WAV.
- Los atajos de teclado funcionan independientemente de si el panel DVK está visible, siempre que el modo del slice activo los admita.
- Si la radio rechaza un comando de inicio de grabación, el área de estado muestra el motivo de la falla (por ejemplo, "Status: Rec (slot 3) failed — Unavailable"). El estado del botón se restablece automáticamente.

## Solución de problemas

- **◀ PREV no tiene efecto** — El espacio seleccionado está vacío. Verifique que la etiqueta de duración del espacio no muestre "Empty". Grabe audio o suba un archivo WAV primero, luego reintente.
- **No se escucha audio durante la vista previa** — La vista previa envía audio al altavoz local. Verifique que la salida de audio de su sistema esté correctamente configurada y no silenciada.
- **Los atajos de teclado F1–F12 no funcionan** — Es posible que el modo de operación del slice activo no admita atajos DVK. Cambie a un modo que admita operación DVK. Si los atajos F1–F12 del panel CVX están habilitados, los atajos DVK se deshabilitan automáticamente.
- **La grabación falla con un error de estado** — La radio rechazó el comando de grabación. Verifique el mensaje de error mostrado en el área de estado y asegúrese de que la radio esté en un estado válido para grabación DVK (por ejemplo, que no esté transmitiendo, que no esté en modo CW).

## Relacionados

- [Resumen del Digital Voice Keyer](overview.md)
- [Grabar un nuevo espacio DVK](record-a-new-dvk-slot.md)
- [Subir un archivo WAV en un espacio](upload-a-wav-file-into-a-slot.md)
- [Reproducir un espacio de voice keyer almacenado](play-a-stored-voice-keyer-slot.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
