# Renombrar una ranura

Asigne un nombre significativo a una ranura DVK para poder identificarla de un vistazo, en lugar de la etiqueta predeterminada "Recording \<n\>".

## Antes de comenzar

- El panel del Digital Voice Keyer debe estar visible en la ventana principal. Aparece cuando DVK está habilitado o un modo de voz está activo.
- Debe establecerse una conexión de radio.

## Pasos

1. En el panel del Digital Voice Keyer, localice la ranura que desea renombrar (F1 a F8).
2. Haga clic derecho en la fila de la ranura.
3. En el menú contextual, seleccione "Rename".
4. La etiqueta del nombre de la ranura es reemplazada por el campo de texto "Rename edit". Escriba el nuevo nombre.
5. Presione Enter para confirmar, o Escape para cancelar sin guardar.

## Función de cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Etiquetas de nombre de ranura | Muestra el nombre actual de cada ranura. | `Recording <n>` |
| Editar nombre | Campo de texto en línea que aparece cuando se activa un renombrado mediante el menú contextual. Escriba el nuevo nombre y presione Enter para aplicar. | — |
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; haga clic derecho para renombrar o subir un archivo WAV. | — |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o 'Empty' (Vacío). | Empty |
| Barras de progreso de ranura | Progreso en vivo de reproducción/grabación. | — |
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

Los siguientes atajos de teclado están activos según el modo de la franja activa (mutuamente excluyentes con los atajos del panel CWX):

- **F1 a F8** — Selecciona y reproduce la ranura correspondiente (F1 = ranura 1, F2 = ranura 2, etc.).
- **F9 a F12** — Selecciona y reproduce las ranuras 9 a 12 (si su radio admite más de 8 ranuras).
- **Escape** — Cancela una operación de renombrado si el campo de edición está abierto; de lo contrario, detiene cualquier grabación o reproducción de DVK.

Los atajos se habilitan automáticamente cuando la franja activa está en un modo de voz y se deshabilitan al cambiar a un modo CW, evitando conflictos con el panel CWX mientras permiten que las teclas funcionen independientemente de la visibilidad del panel.

## Consejos

- Hacer doble clic en la etiqueta del nombre de la ranura también abre directamente el campo "Rename edit".
- Presionar Escape mientras el campo "Rename edit" está abierto cancela el renombrado y restaura el nombre anterior.

## Relacionado

- [Descripción general del Digital Voice Keyer](overview.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Subir un archivo WAV a una ranura](upload-a-wav-file-into-a-slot.md)
