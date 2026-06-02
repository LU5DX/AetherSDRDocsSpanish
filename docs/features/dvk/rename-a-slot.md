# Cambiar el nombre de una ranura

Asigne un nombre significativo a una ranura de DVK para poder identificarla de un vistazo, en lugar de la etiqueta predeterminada "Recording <n>".

## Antes de comenzar

- El panel Digital Voice Keyer debe estar visible en la ventana principal. Aparece cuando DVK está habilitado o un modo de voz está activo.
- Debe establecerse una conexión de radio.

## Pasos

1. En el panel Digital Voice Keyer, localice la ranura que desea renombrar (F1 a F8).
2. Haga clic derecho en la fila de la ranura.
3. En el menú contextual, seleccione "Rename".
4. La etiqueta del nombre de la ranura se reemplaza por el campo de texto "Rename edit". Escriba el nuevo nombre.
5. Presione Enter para confirmar, o presione Escape para cancelar sin guardar.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Etiquetas de nombre de ranura | Muestra el nombre actual de cada ranura. | `Recording <n>` |
| Editar nombre (Rename edit) | Campo de texto en línea que aparece cuando se inicia un cambio de nombre mediante el menú contextual. Escriba el nuevo nombre y presione Enter para aplicarlo. | — |
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; haga clic derecho para renombrar o cargar un archivo WAV. | — |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o 'Empty'. | Empty |
| Barras de progreso de ranura | Progreso de reproducción/grabación en vivo. | — |
| ● REC | Inicia la grabación en la ranura seleccionada. | — |
| ■ STOP | Detiene la grabación o reproducción. | — |
| ▶ PLAY | Reproduce la ranura seleccionada. | — |
| ◀ PREV | Previsualiza la ranura a través del altavoz local. | — |

## Indicador de estado

El panel muestra un indicador de estado en la parte superior:

| Etiqueta | Estados posibles | Significado |
|---|---|---|
| Status: | Idle, Recording, Playing | Estado actual de DVK. |

## Atajos de teclado

Los siguientes atajos de teclado están activos según el modo de la rodaja activa (mutuamente excluyentes con los atajos del panel CWX):

- **F1 a F8** — Seleccionar y reproducir la ranura correspondiente (F1 = ranura 1, F2 = ranura 2, etc.).
- **F9 a F12** — Seleccionar y reproducir las ranuras 9 a 12 (si su radio admite más de 8 ranuras).
- **Escape** — Cancelar una operación de cambio de nombre si el campo de edición está abierto; de lo contrario, detener cualquier grabación o reproducción de DVK.

Los atajos se habilitan automáticamente cuando la rodaja activa está en un modo de voz y se deshabilitan al cambiar a un modo CW, evitando conflictos con el panel CWX mientras permiten que las teclas se activen independientemente de la visibilidad del panel.

## Consejos

- Hacer doble clic en la etiqueta del nombre de la ranura también abre directamente el campo "Rename edit".
- Presionar Escape mientras el campo "Rename edit" está abierto cancela el cambio de nombre y restaura el nombre anterior.

## Relacionado

- [Resumen del Digital Voice Keyer](overview.md)
- [Grabar una nueva ranura de DVK](record-a-new-dvk-slot.md)
- [Cargar un archivo WAV en una ranura](upload-a-wav-file-into-a-slot.md)
