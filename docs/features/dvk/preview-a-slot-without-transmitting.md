# Vista previa de un slot sin transmitir

Utilice esta página para escuchar un slot de DVK a través de su altavoz local antes de enviarlo al aire. La vista previa le permite confirmar el contenido y el nivel de audio sin poner en funcionamiento el transmisor.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El panel de DVK requiere una conexión activa con la radio.
- El slot que desea previsualizar debe contener una grabación. Los slots que muestran "Empty" no se pueden previsualizar.

## Pasos

1. Abra el panel del Digital Voice Keyer en el área central de la MainWindow.
2. Haga clic en la fila del slot (F1 a F8) que desea previsualizar. La fila seleccionada se resalta con un borde azul.
3. Haga clic en ◀ PREV.
4. Escuche el audio a través de su altavoz local. La barra de progreso del slot se vuelve azul y avanza durante la reproducción.
5. Cuando el slot termina, la reproducción se detiene automáticamente y el estado vuelve a "Status: Idle". Para detener antes, haga clic en ■ STOP o presione Escape.

## Función de cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de slot F1 … F8 | Selecciona el slot. Si el slot se está reproduciendo en el aire, al hacer clic de nuevo se detiene. | No inicia la vista previa. |
| Etiquetas de duración del slot | Muestra la duración de la grabación o "Empty". | Un slot que muestra "Empty" no se puede previsualizar. |
| Barras de progreso del slot | Muestra el progreso de la reproducción en azul durante la vista previa. | Ocultas en reposo. |
| ◀ PREV | Inicia la vista previa del slot seleccionado a través del altavoz local. Haga clic de nuevo para detener. | No transmite. |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | También se activa con Escape. |
| Status: Idle / Recording / Playing | Muestra el estado actual del DVK en la parte inferior del panel. | |

## Consejos

- Si hace clic en ◀ PREV en un slot que ya está en vista previa, la vista previa se detiene.
- Presionar Escape detiene una vista previa activa sin usar el ratón.
- Los botones de función F1–F8 y los atajos de teclado F1–F8 activan la reproducción al aire, no la vista previa. Use ◀ PREV específicamente cuando no desee transmitir.

## Solución de problemas

- **◀ PREV no tiene efecto** — El slot seleccionado está vacío. Verifique que la etiqueta de duración del slot no muestre "Empty". Grabe audio o cargue un archivo WAV primero, luego intente de nuevo.
- **No se escucha audio durante la vista previa** — La vista previa dirige el audio al altavoz local. Verifique que la salida de audio de su sistema esté configurada correctamente y no esté silenciada.

## Relacionados

- [Digital Voice Keyer overview](overview.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
