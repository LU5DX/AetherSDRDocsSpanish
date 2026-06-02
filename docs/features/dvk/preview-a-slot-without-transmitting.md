# Vista previa de un slot sin transmitir

Use esta página para probar un slot del DVK a través de su altavoz local antes de enviarlo al aire. La vista previa le permite confirmar el contenido de audio y el nivel sin accionar el transmisor.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK requiere una conexión activa con la radio.
- El slot que desea previsualizar debe contener una grabación. Los slots que muestran "Empty" no se pueden previsualizar.

## Pasos

1. Abra el panel Digital Voice Keyer en el área central de MainWindow.
2. Haga clic en la fila del slot (F1 a F8) que desea previsualizar. La fila seleccionada se resalta con un borde azul.
3. Haga clic en ◀ PREV.
4. Escuche el audio a través de su altavoz local. La barra de progreso del slot se vuelve azul y avanza durante la reproducción.
5. Cuando el slot finaliza, la reproducción se detiene automáticamente y el estado vuelve a "Status: Idle". Para detener antes, haga clic en ■ STOP o presione Escape.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de slot F1 … F8 | Selecciona el slot. Si el slot se está reproduciendo al aire, al hacer clic nuevamente se detiene. Haga clic derecho para renombrar o subir un archivo WAV. | No activa la vista previa. |
| Etiquetas de nombre de slot | Muestra el nombre de cada slot. | El nombre predeterminado es "Recording \<n\>". |
| Etiquetas de duración de slot | Muestra la duración de la grabación o "Empty". | Un slot que muestra "Empty" no se puede previsualizar. |
| Barras de progreso de slot | Muestra el progreso de reproducción en azul durante la vista previa. | Ocultas cuando está inactivo. |
| ● REC | Inicia la grabación en el slot seleccionado. | |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | También se activa con Escape. |
| ▶ PLAY | Reproduce el slot seleccionado al aire. | No es vista previa. |
| ◀ PREV | Inicia la vista previa del slot seleccionado a través del altavoz local. Haga clic nuevamente para detener. | No transmite. |
| Editar nombre | Cambio de nombre en línea de un slot activado mediante el menú contextual. | |
| Status: Idle / Recording / Playing | Muestra el estado actual del DVK en la parte inferior del panel. | |

## Atajos de teclado

El panel DVK registra los atajos de teclado F1–F12 y Escape. La disponibilidad de los atajos está controlada por el modo de operación del slice activo, no por la visibilidad del panel. Esto asegura que los atajos del DVK estén habilitados solo cuando el slice activo esté en un modo compatible, y sean mutuamente excluyentes con los atajos F1–F12 del panel CWX para evitar conflictos de teclas.

| Tecla | Acción |
|---|---|
| F1–F12 | Selecciona y reproduce el slot correspondiente (F1 = slot 1, F2 = slot 2, etc.). Los slots más allá de F8 (F9–F12) no son funcionales en la mayoría de las configuraciones. |
| Escape | Detiene la grabación, reproducción o vista previa. Si hay una edición de nombre activa, cancela el cambio de nombre. |

## Consejos

- Si hace clic en ◀ PREV en un slot que ya está en vista previa, se detiene la vista previa.
- Presionar Escape detiene una vista previa activa sin usar el ratón.
- Los botones de función F y los atajos de teclado F1–F12 activan la reproducción al aire, no la vista previa. Use ◀ PREV específicamente cuando no desee transmitir.
- Haga clic derecho en un botón de slot para renombrarlo o subir un archivo WAV.
- Los atajos de teclado funcionan independientemente de si el panel DVK está visible actualmente, siempre que el modo del slice activo los admita.

## Solución de problemas

- **◀ PREV no tiene efecto** — El slot seleccionado está vacío. Verifique que la etiqueta de duración del slot no muestre "Empty". Grabe audio o suba un archivo WAV primero, luego intente de nuevo.
- **No se escucha audio durante la vista previa** — La vista previa dirige el audio al altavoz local. Verifique que la salida de audio de su sistema esté configurada correctamente y no esté silenciada.
- **Los atajos de teclado F1–F12 no funcionan** — El modo de operación del slice activo puede no admitir los atajos del DVK. Cambie a un modo que admita la operación del DVK. Si los atajos F1–F12 del panel CWX están habilitados, los atajos del DVK se deshabilitan automáticamente.

## Relacionados

- [Digital Voice Keyer overview](overview.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
