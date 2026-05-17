# Grabar una nueva ranura de DVK

Use el panel del Digital Voice Keyer para grabar su voz en una de hasta 8 ranuras, que luego podrá reproducir al aire con un solo clic o pulsando una tecla F.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El panel DVK solo está disponible cuando hay una conexión activa con la radio.
- El panel DVK debe estar visible en la ventana principal. Si no se muestra, cambie a un modo de voz o active DVK en la radio.
- Su micrófono debe estar configurado y funcionando a través de la ruta de audio de la radio.

## Pasos

1. En el panel DVK, haga clic en la fila de la ranura donde desea grabar (F1 a F8). La fila seleccionada se resalta con un borde azul.
2. Haga clic en **● REC**. El botón se vuelve rojo y el indicador de estado cambia a **Recording**. Aparece la barra de progreso de la ranura y avanza a medida que se captura el audio.
3. Hable su mensaje al micrófono.
4. Haga clic en **■ STOP** cuando haya terminado. El indicador de estado vuelve a **Idle**, la barra de progreso desaparece y la etiqueta de duración de la ranura se actualiza de **Empty** para mostrar la duración grabada.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; clic derecho para renombrar o subir un archivo WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o **Empty** si la ranura no tiene audio. | Empty |
| Barras de progreso de ranura | Muestra el progreso de grabación o reproducción en vivo. Ocultas en reposo. | — |
| **● REC** | Inicia la grabación en la ranura seleccionada. Se vuelve rojo mientras está activo. | — |
| **■ STOP** | Detiene la grabación o reproducción. | — |
| **▶ PLAY** | Reproduce la ranura seleccionada al aire. | — |
| **◀ PREV** | Previsualiza la ranura seleccionada a través del altavoz local sin transmitir. | — |

## Consejos

- La ranura 1 está seleccionada por defecto cuando se abre el panel DVK. Si hace clic en **● REC** sin seleccionar otra ranura, la grabación se guarda en la ranura 1.
- Presionar Escape cancela la grabación con el mismo efecto que **■ STOP**.
- Puede renombrar una ranura después de grabar haciendo clic derecho en su fila y eligiendo rename en el menú contextual. La etiqueta del nombre de la ranura se puede editar en línea.
- Los atajos de teclas F (F1–F8 y Escape) están activos siempre que la franja activa esté en un modo de voz. El panel DVK no necesita estar visible para que los atajos funcionen. Si cambia a un modo CW, los atajos de DVK se deshabilitan automáticamente y los atajos de CWX se activan en su lugar, evitando conflictos.
- Los botones de teclas F solo activan la reproducción si la ranura ya contiene una grabación. Una ranura que aún muestra **Empty** en la etiqueta de duración no se reproducirá cuando se presione su tecla F.

## Solución de problemas

- **La etiqueta de duración permanece en Empty después de grabar** — Es posible que la radio no haya recibido audio. Verifique que la entrada de micrófono correcta esté seleccionada en `Settings > Radio Setup...` y que la radio no esté en un modo que deshabilite el micrófono.
- **● REC no hace nada al hacer clic** — No hay ninguna ranura seleccionada. Haga clic en una fila de ranura primero, luego haga clic en **● REC**.
- **El estado muestra Recording pero no se captura audio** — Verifique que el micrófono no esté silenciado a nivel del sistema operativo y que el dispositivo de entrada de audio esté enrutado correctamente a través de la radio.
- **Las teclas F no responden en el panel DVK** — La franja activa debe estar en un modo de voz para que los atajos de teclas F de DVK estén activos. Si la franja está en modo CW, los atajos de teclado de CWX están activos en su lugar.

## Relacionado

- [Digital Voice Keyer overview](overview.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Rename a slot](rename-a-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
