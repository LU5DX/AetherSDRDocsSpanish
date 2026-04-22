# Vista previa de un slot sin transmitir

Use esta página para auditar un slot del DVK a través de su altavoz local antes de enviarlo al aire. La vista previa le permite confirmar el contenido de audio y el nivel sin activar el transmisor.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel DVK requiere una conexión de radio activa.
- El slot que desea previsualizar debe contener una grabación. Los slots que muestran "Empty" no pueden previsualizarse.

## Pasos

1. Abra el panel Digital Voice Keyer en el área central de MainWindow.
2. Haga clic en la fila del slot (F1 hasta F8) que desea previsualizar. La fila seleccionada se resalta con un borde azul.
3. Haga clic en ◀ PREV.
4. Escuche el audio a través de su altavoz local. La barra de progreso del slot se vuelve azul y avanza durante la reproducción.
5. Cuando el slot finaliza, la reproducción se detiene automáticamente y el estado regresa a "Status: Idle". Para detenerla antes, haga clic en ■ STOP o presione Escape.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| Botones de slot F1 … F8 | Selecciona el slot. Si el slot se está reproduciendo al aire, hacer clic de nuevo lo detiene. | No activa la vista previa. |
| Etiquetas de duración del slot | Muestra la duración de la grabación o "Empty". | Un slot que muestra "Empty" no puede previsualizarse. |
| Barras de progreso del slot | Muestra el progreso de la reproducción en azul durante la vista previa. | Ocultas cuando está inactivo. |
| ◀ PREV | Inicia la vista previa del slot seleccionado a través del altavoz local. Haga clic de nuevo para detenerla. | No transmite. |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | También se activa con Escape. |
| Status: Idle / Recording / Playing | Muestra el estado actual del DVK en la parte inferior del panel. | |

## Consejos

- Si hace clic en ◀ PREV sobre un slot que ya está en vista previa, esta se detiene.
- Presionar Escape detiene una vista previa activa sin usar el ratón.
- Los botones de teclas F y los atajos de teclado F1–F8 activan la reproducción al aire, no la vista previa. Use ◀ PREV específicamente cuando no desee transmitir.

## Solución de problemas

- **◀ PREV no tiene efecto** — El slot seleccionado está vacío. Verifique que la etiqueta de duración del slot no muestre "Empty". Grabe audio o cargue un archivo WAV primero y vuelva a intentarlo.
- **No se escucha audio durante la vista previa** — La vista previa envía el audio al altavoz local. Verifique que la salida de audio del sistema esté correctamente configurada y no esté silenciada.

## Relacionados

- [Descripción general del Digital Voice Keyer](overview.md)
- [Grabar un nuevo slot del DVK](record-a-new-dvk-slot.md)
- [Cargar un archivo WAV en un slot](upload-a-wav-file-into-a-slot.md)
- [Reproducir un slot de voice keyer almacenado](play-a-stored-voice-keyer-slot.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
