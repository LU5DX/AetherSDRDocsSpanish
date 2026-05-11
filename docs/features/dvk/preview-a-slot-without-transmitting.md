# Vista previa de una ranura sin transmitir

Utilice esta página para probar una ranura del DVK a través de su altavoz local antes de enviarla al aire. La vista previa le permite confirmar el contenido y el nivel de audio sin activar el transmisor.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK requiere una conexión activa con la radio.
- La ranura que desea previsualizar debe contener una grabación. Las ranuras que muestran "Empty" no se pueden previsualizar.

## Pasos

1. Abra el panel Digital Voice Keyer en el área central de la MainWindow.
2. Haga clic en la fila de la ranura (F1 a F8) que desea previsualizar. La fila seleccionada se resalta con un borde azul.
3. Haga clic en ◀ PREV.
4. Escuche el audio a través de su altavoz local. La barra de progreso de la ranura se vuelve azul y avanza durante la reproducción.
5. Cuando la ranura finaliza, la reproducción se detiene automáticamente y el estado vuelve a "Status: Idle". Para detenerla antes, haga clic en ■ STOP o presione Escape.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona la ranura. Si la ranura se está reproduciendo al aire, al hacer clic de nuevo se detiene. | No activa la vista previa. |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | El nombre predeterminado es "Recording \<n\>". |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o "Empty". | Una ranura que muestra "Empty" no se puede previsualizar. |
| Barras de progreso de ranura | Muestra el progreso de reproducción en azul durante la vista previa. | Ocultas cuando está inactivo. |
| ● REC | Inicia la grabación en la ranura seleccionada. | |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | También se activa con Escape. |
| ▶ PLAY | Reproduce la ranura seleccionada al aire. | No proporciona vista previa. |
| ◀ PREV | Inicia la vista previa de la ranura seleccionada a través del altavoz local. Vuelva a hacer clic para detenerla. | No transmite. |
| Rename edit | Cambio de nombre en línea de una ranura activado mediante el menú contextual. | |
| Status: Idle / Recording / Playing | Muestra el estado actual del DVK en la parte inferior del panel. | |

## Atajos de teclado

El panel DVK registra los atajos de teclado F1–F12 y Escape cuando el panel está visible. Estos atajos se deshabilitan automáticamente cuando el panel está oculto, evitando conflictos con otros paneles que usan las mismas teclas (como el panel CWX).

| Tecla | Acción |
|---|---|
| F1–F12 | Selecciona y reproduce la ranura correspondiente (F1 = ranura 1, F2 = ranura 2, etc.). Las ranuras más allá de F8 (F9–F12) no son funcionales en la mayoría de las configuraciones. |
| Escape | Detiene la grabación, reproducción o vista previa. Si hay un cambio de nombre activo, cancela el cambio de nombre. |

## Consejos

- Si hace clic en ◀ PREV en una ranura que ya está en vista previa, se detiene la vista previa.
- Presionar Escape detiene una vista previa activa sin usar el ratón.
- Los botones de teclas F y los atajos de teclado F1–F12 activan la reproducción al aire, no la vista previa. Use ◀ PREV específicamente cuando no desee transmitir.
- Haga clic derecho en un botón de ranura para cambiarle el nombre o cargar un archivo WAV.

## Solución de problemas

- **◀ PREV no tiene efecto** — La ranura seleccionada está vacía. Verifique que la etiqueta de duración de la ranura no muestre "Empty". Grabe audio o cargue un archivo WAV primero, luego vuelva a intentarlo.
- **No se escucha audio durante la vista previa** — La vista previa dirige el audio al altavoz local. Verifique que la salida de audio de su sistema esté configurada correctamente y no esté silenciada.
- **Los atajos de teclado F1–F12 no funcionan** — El panel DVK debe estar visible. Si el panel CWX u otro panel se muestra actualmente, los atajos del DVK están deshabilitados. Cambie al panel DVK para usar sus atajos.

## Relacionados

- [Digital Voice Keyer overview](overview.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
