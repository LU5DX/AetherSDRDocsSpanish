# Vista previa de un espacio sin transmitir

Utilice esta página para escuchar un espacio del DVK a través de su altavoz local antes de enviarlo al aire. La vista previa le permite confirmar el contenido de audio y el nivel sin activar el transmisor.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo de radio. El panel DVK requiere una conexión activa con la radio.
- El espacio que desea previsualizar debe contener una grabación. Los espacios que muestran "Empty" no se pueden previsualizar.

## Pasos

1. Abra el panel del Digital Voice Keyer en el área central de la MainWindow.
2. Haga clic en la fila del espacio (F1 a F8) que desea previsualizar. La fila seleccionada se resalta con un borde azul.
3. Haga clic en ◀ PREV.
4. Escuche el audio a través de su altavoz local. La barra de progreso del espacio se vuelve azul y avanza durante la reproducción.
5. Cuando el espacio termina, la reproducción se detiene automáticamente y el estado vuelve a "Status: Idle". Para detener antes, haga clic en ■ STOP o presione Escape.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de espacio F1 … F8 | Selecciona el espacio. Si el espacio se está reproduciendo actualmente al aire, al hacer clic de nuevo se detiene. | No activa la vista previa. |
| Etiquetas de nombre del espacio | Muestra el nombre de cada espacio. | El nombre predeterminado es "Recording \<n\>". |
| Etiquetas de duración del espacio | Muestra la duración de la grabación o "Empty". | Un espacio que muestra "Empty" no se puede previsualizar. |
| Barras de progreso del espacio | Muestra el progreso de reproducción en azul durante la vista previa. | Ocultas cuando está inactivo. |
| ● REC | Inicia la grabación en el espacio seleccionado. | |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | También se activa con Escape. |
| ▶ PLAY | Reproduce el espacio seleccionado al aire. | No previsualiza. |
| ◀ PREV | Inicia la vista previa del espacio seleccionado a través del altavoz local. Haga clic de nuevo para detener. | No transmite. |
| Rename edit | Cambio de nombre en línea de un espacio activado mediante el menú contextual. | |
| Status: Idle / Recording / Playing | Muestra el estado actual del DVK en la parte inferior del panel. | |

## Atajos de teclado

El panel DVK registra los atajos de teclado F1–F12 y Escape. La disponibilidad de los atajos se controla por el modo de operación del slice activo, no por la visibilidad del panel. Esto garantiza que los atajos del DVK estén habilitados solo cuando el slice activo está en un modo compatible, y son mutuamente excluyentes con los atajos F1–F12 del panel CWX para prevenir conflictos de teclas.

| Tecla | Acción |
|---|---|
| F1–F12 | Selecciona y reproduce el espacio correspondiente (F1 = espacio 1, F2 = espacio 2, etc.). Los espacios más allá de F8 (F9–F12) no son funcionales en la mayoría de las configuraciones. |
| Escape | Detiene la grabación, reproducción o vista previa. Si hay un cambio de nombre en línea activo, cancela el cambio de nombre. |

## Consejos

- Si hace clic en ◀ PREV en un espacio que ya está en vista previa, se detiene la vista previa.
- Presionar Escape detiene una vista previa activa sin usar el ratón.
- Los botones de función F y los atajos de teclado F1–F12 activan la reproducción al aire, no la vista previa. Use ◀ PREV específicamente cuando no desee transmitir.
- Haga clic derecho en un botón de espacio para renombrarlo o cargar un archivo WAV.
- Los atajos de teclado funcionan independientemente de si el panel DVK está visible actualmente, siempre que el modo del slice activo los admita.

## Solución de problemas

- **◀ PREV no tiene efecto**: el espacio seleccionado está vacío. Verifique que la etiqueta de duración del espacio no muestre "Empty". Grabe audio o cargue un archivo WAV primero, luego intente de nuevo.
- **No se escucha audio durante la vista previa**: la vista previa enruta el audio al altavoz local. Verifique que la salida de audio de su sistema esté correctamente configurada y no esté silenciada.
- **Los atajos de teclado F1–F12 no funcionan**: es posible que el modo de operación del slice activo no admita los atajos del DVK. Cambie a un modo que admita la operación del DVK. Si los atajos F1–F12 del panel CWX están habilitados, los atajos del DVK se deshabilitan automáticamente.

## Relacionado

- [Digital Voice Keyer overview](overview.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
