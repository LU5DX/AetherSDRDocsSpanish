# Cambiar nombre de una ranura

Asigne un nombre significativo a una ranura del DVK para identificarla de un vistazo, en lugar de la etiqueta predeterminada "Recording \<n\>".

## Antes de comenzar

- El panel del Digital Voice Keyer debe estar visible en la ventana principal. Aparece cuando el DVK está habilitado o un modo de voz está activo.
- Debe establecerse una conexión con la radio.

## Pasos

1. En el panel del Digital Voice Keyer, localice la ranura que desea renombrar (F1 a F8).
2. Haga clic derecho en la fila de la ranura.
3. En el menú contextual, seleccione "Rename".
4. La etiqueta del nombre de la ranura se reemplaza por el campo de texto "Rename edit". Escriba el nuevo nombre.
5. Presione Enter para confirmar, o presione Escape para cancelar sin guardar.

## Descripción de cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Etiquetas de nombre de ranura | Muestra el nombre actual de cada ranura. | `Recording <n>` |
| Rename edit | Campo de texto en línea que aparece cuando se activa un cambio de nombre desde el menú contextual. Escriba el nuevo nombre y presione Enter para aplicarlo. | — |
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; haga clic derecho para renombrar o cargar un archivo WAV. | — |
| Etiquetas de duración de ranura | Muestra la longitud de la grabación o 'Empty'. | Empty |
| Barras de progreso de ranura | Progreso en vivo de reproducción/grabación. | — |
| ● REC | Inicia la grabación en la ranura seleccionada. | — |
| ■ STOP | Detiene la grabación o reproducción. | — |
| ▶ PLAY | Reproduce la ranura seleccionada. | — |
| ◀ PREV | Previsualiza la ranura a través del altavoz local. | — |

## Indicador de estado

El panel muestra un indicador de estado en la parte superior:

| Etiqueta | Estados posibles | Significado |
|---|---|---|
| Status: | Idle, Recording, Playing | Estado actual del DVK. Si un comando falla, el estado muestra el mensaje de error (ej.: "Status: Record (slot 2) failed — reason"). Los botones del panel se restablecen para reflejar el estado actual después de una falla. |

## Atajos de teclado

Los siguientes atajos de teclado están activos según el modo de la rebanada activa (excluyentes con los atajos del panel CWX):

- **F1 a F8** — Selecciona y reproduce la ranura correspondiente (F1 = ranura 1, F2 = ranura 2, etc.).
- **F9 a F12** — Selecciona y reproduce las ranuras 9 a 12 (si su radio admite más de 8 ranuras).
- **Escape** — Cancela una operación de cambio de nombre si el campo de edición "Rename edit" está abierto; de lo contrario, detiene cualquier grabación o reproducción del DVK.

Los atajos se habilitan automáticamente cuando la rebanada activa está en un modo de voz y se deshabilitan al cambiar a un modo CW, evitando conflictos con el panel CWX mientras permiten que las teclas funcionen independientemente de la visibilidad del panel.

## Consejos

- Al hacer doble clic en la etiqueta del nombre de la ranura también se abre directamente el campo "Rename edit".
- Presionar Escape mientras el campo "Rename edit" está abierto cancela el cambio de nombre y restaura el nombre anterior.
- Si la radio rechaza un comando de grabación o reproducción (por ejemplo, otro cliente tiene el recurso DVK), el indicador de estado muestra un mensaje de error y los botones del panel vuelven a su estado anterior.

## Relacionados

- [Digital Voice Keyer overview](overview.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
