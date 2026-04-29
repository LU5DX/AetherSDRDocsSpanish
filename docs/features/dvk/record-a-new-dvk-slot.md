# Grabar un nuevo slot del DVK

Use el panel Digital Voice Keyer para grabar su voz en uno de hasta 12 slots, que luego podrá reproducir en el aire con un solo clic o pulsando una tecla F.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel DVK solo está disponible cuando hay una conexión de radio activa.
- El panel DVK debe estar visible en la ventana principal. Si no se muestra, cambie a un modo de voz o habilite el DVK en el radio.
- Su micrófono debe estar configurado y funcionando a través de la ruta de audio del radio.

## Pasos

1. En el panel DVK, haga clic en la fila del slot en el que desea grabar (F1 a F12). La fila seleccionada se resalta con un borde azul.
2. Haga clic en **● REC**. El botón se pone rojo y el indicador de estado cambia a **Recording**. Aparece la barra de progreso del slot y avanza a medida que se captura el audio.
3. Hable su mensaje al micrófono.
4. Haga clic en **■ STOP** cuando termine. El indicador de estado vuelve a **Idle**, la barra de progreso desaparece y la etiqueta de duración del slot se actualiza de **Empty** para mostrar la duración grabada.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de slot F1 … F12 | Selecciona y reproduce ese slot; haga clic derecho para renombrarlo o cargar un WAV. | — |
| Etiquetas de nombre de slot | Muestra el nombre de cada slot. | `Recording <n>` |
| Etiquetas de duración de slot | Muestra la duración de la grabación o **Empty** si el slot no tiene audio. | Empty |
| Barras de progreso de slot | Muestra el progreso en tiempo real de la grabación o reproducción. Oculta cuando está inactivo. | — |
| **● REC** | Inicia la grabación en el slot seleccionado. Se pone rojo mientras está activo. | — |
| **■ STOP** | Detiene la grabación o la reproducción. | — |
| **▶ PLAY** | Reproduce el slot seleccionado en el aire. | — |
| **◀ PREV** | Previsualiza el slot seleccionado a través del altavoz local sin transmitir. | — |

## Consejos

- El slot 1 está seleccionado de forma predeterminada cuando el panel DVK se abre por primera vez. Si hace clic en **● REC** sin seleccionar un slot diferente, la grabación se almacena en el slot 1.
- Presionar Escape cancela la grabación con el mismo efecto que **■ STOP**.
- Puede renombrar un slot después de grabar haciendo clic derecho en su fila y eligiendo la opción de renombrar en el menú contextual. La etiqueta de nombre del slot es editable directamente en su lugar.
- Los botones de tecla F solo activan la reproducción si el slot ya contiene una grabación. Un slot que aún muestra **Empty** en la etiqueta de duración no se reproducirá cuando se presione su tecla F.

## Solución de problemas

- **La etiqueta de duración permanece en Empty después de grabar** — Es posible que el radio no haya recibido audio. Verifique que la entrada de micrófono correcta esté seleccionada en `Settings > Radio Setup...` y que el radio no esté en un modo que deshabilite el micrófono.
- **● REC no hace nada al hacer clic** — No hay ningún slot seleccionado. Haga clic primero en una fila de slot y luego en **● REC**.
- **El estado muestra Recording pero no se captura audio** — Verifique que el micrófono no esté silenciado a nivel del sistema operativo y que el dispositivo de entrada de audio esté enrutado correctamente a través del radio.

## Relacionados

- [Descripción general del Digital Voice Keyer](overview.md)
- [Reproducir un slot de voice keyer almacenado](play-a-stored-voice-keyer-slot.md)
- [Previsualizar un slot sin transmitir](preview-a-slot-without-transmitting.md)
- [Renombrar un slot](rename-a-slot.md)
- [Cargar un archivo WAV en un slot](upload-a-wav-file-into-a-slot.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
