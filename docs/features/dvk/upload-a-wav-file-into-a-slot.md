# Cargar un archivo WAV en una ranura

Cargue un archivo WAV previamente grabado desde su computadora en una de las ranuras del teclado digital de voz (DVK) para reproducirlo al aire sin necesidad de grabarlo en vivo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK solo está disponible cuando hay una conexión activa con la radio.
- El panel DVK debe estar visible en la ventana principal. Aparece cuando DVK está habilitado o un modo de voz está activo.
- Tenga el archivo WAV listo en su computadora.

## Pasos

1. Localice la fila de la ranura donde desea cargar el archivo (F1 a F8).
2. Haga clic derecho en cualquier lugar del marco de la fila de esa ranura.
3. En el menú contextual que aparece, seleccione la opción de carga.
4. En el cuadro de diálogo de archivos que se abre, navegue hasta su archivo WAV y selecciónelo.
5. Confirme la selección. La etiqueta de duración de la ranura cambia de "Empty" a la duración del archivo cuando la transferencia se completa.

## Funciones de cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; clic derecho para abrir el menú contextual para renombrar o cargar WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre asignado a la ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación, o "Empty" si la ranura no tiene contenido. | Empty |
| Barras de progreso de ranura | Muestra el progreso de reproducción o grabación en vivo. Ocultas cuando la ranura está inactiva. | — |
| ● REC | Inicia la grabación en la ranura seleccionada. | — |
| ■ STOP | Detiene la grabación o reproducción. | — |
| ▶ PLAY | Reproduce la ranura seleccionada. | — |
| ◀ PREV | Previsualiza la ranura a través del altavoz local. | — |
| Edición de nombre | Cambio de nombre en línea de una ranura activado mediante el menú contextual. | — |
| Indicador de estado | Muestra el estado actual del DVK: Idle, Recording o Playing. | Idle |

## Atajos de teclado

El panel DVK registra los atajos de teclado F1–F12 y Escape. Estos atajos se habilitan o deshabilitan según el modo de la rodaja activa, asegurando que sean mutuamente excluyentes con los atajos F1–F12 del panel CWX. Cuando la rodaja activa está en un modo de voz, los atajos DVK están activos independientemente de si el panel DVK está visible.

| Tecla | Acción |
|---|---|
| F1 … F12 | Selecciona y reproduce la ranura correspondiente (F1 selecciona la ranura 1, F2 selecciona la ranura 2, etc.). La ranura debe contener una grabación. |
| Escape | Cancela una operación de cambio de nombre activa. Si no hay un cambio de nombre en curso, detiene cualquier grabación o reproducción del DVK. |

## Consejos

- Después de que la carga finalice, verifique que la etiqueta de duración de la ranura ya no muestre "Empty" antes de transmitir.
- Puede renombrar la ranura inmediatamente después de cargar haciendo clic derecho nuevamente en la fila y seleccionando la opción de cambio de nombre. Consulte [Renombrar una ranura](rename-a-slot.md).
- Use los atajos de teclado (F1–F8) para seleccionar y reproducir rápidamente mensajes almacenados al aire. La tecla Escape ofrece una forma conveniente de detener la operación.

## Solución de problemas

- **La duración de la ranura aún muestra "Empty" después de seleccionar un archivo** — Es posible que la transferencia a la radio haya fallado. Verifique que la conexión con la radio siga activa y luego intente la carga nuevamente.
- **El menú contextual no aparece** — Haga clic en otro lugar primero para deseleccionar cualquier control activo, luego haga clic derecho directamente en el marco de la fila de la ranura.
- **Los atajos de teclado (F1–F8, Escape) no funcionan** — Asegúrese de que la rodaja activa esté en un modo de voz. Los atajos DVK solo están habilitados cuando el modo de la rodaja admite la operación del teclado de voz. Si la rodaja está en modo CW, los atajos del panel CWX tienen prioridad.
- **El estado muestra "Transfer failed" en lugar de un mensaje de éxito** — La carga del archivo WAV encontró un error. Verifique que el formato del archivo sea un WAV válido y que la conexión con la radio esté activa, luego intente nuevamente.

## Relacionado

- [Descripción general del teclado digital de voz](overview.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Reproducir una ranura almacenada del teclado de voz](play-a-stored-voice-keyer-slot.md)
- [Renombrar una ranura](rename-a-slot.md)
