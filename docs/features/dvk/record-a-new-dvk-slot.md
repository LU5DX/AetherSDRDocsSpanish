# Grabar una nueva ranura de DVK

Use el panel del Grabadora de Voz Digital (DVK) para grabar su voz en una de hasta 8 ranuras, que luego puede reproducir al aire con un solo clic o presionando una tecla de función (F).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK solo está disponible cuando hay una conexión activa con la radio.
- El panel DVK debe estar visible en la ventana principal. Si no se muestra, cambie a un modo de voz o active el DVK en la radio.
- Su micrófono debe estar configurado y funcionando a través de la ruta de audio de la radio.

## Pasos

1. En el panel DVK, haga clic en la fila de la ranura en la que desea grabar (F1 a F8). La fila seleccionada se resalta con un borde azul.
2. Haga clic en **● REC**. El botón se vuelve rojo y el indicador de estado cambia a **Recording**. La barra de progreso de la ranura aparece y avanza a medida que se captura el audio.
3. Hable su mensaje en el micrófono.
4. Haga clic en **■ STOP** cuando haya terminado. El indicador de estado vuelve a **Idle**, la barra de progreso desaparece y la etiqueta de duración de la ranura se actualiza de **Empty** para mostrar la duración grabada.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; haga clic derecho para renombrar o cargar un WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o **Empty** si la ranura no tiene audio. | Empty |
| Barras de progreso de ranura | Muestra el progreso de grabación o reproducción en vivo. Oculta cuando está inactiva. | — |
| **● REC** | Inicia la grabación en la ranura seleccionada. Se vuelve rojo mientras está activa. | — |
| **■ STOP** | Detiene la grabación o reproducción. | — |
| **▶ PLAY** | Reproduce la ranura seleccionada al aire. | — |
| **◀ PREV** | Previsualiza la ranura seleccionada a través del altavoz local sin transmitir. | — |

## Consejos

- La ranura 1 está seleccionada de forma predeterminada cuando se abre el panel DVK por primera vez. Si hace clic en **● REC** sin seleccionar otra ranura, la grabación se guarda en la ranura 1.
- Presionar Escape cancela la grabación con el mismo efecto que **■ STOP**.
- Puede renombrar una ranura después de grabar haciendo clic derecho en su fila y eligiendo renombrar en el menú contextual. La etiqueta de nombre de la ranura se puede editar en el lugar.
- Los atajos de teclas de función (F1–F8 y Escape) están activos siempre que la porción activa esté en un modo de voz. El panel DVK no necesita estar visible para que funcionen los atajos. Si cambia a un modo CW, los atajos de DVK se desactivan automáticamente y los atajos de teclado de CWX se activan, evitando conflictos.
- Los botones de teclas de función solo activan la reproducción si la ranura ya contiene una grabación. Una ranura que aún muestra **Empty** en la etiqueta de duración no se reproducirá cuando se presione su tecla de función.

## Solución de problemas

- **La etiqueta de duración permanece en Empty después de grabar** — Es posible que la radio no haya recibido audio. Verifique que la entrada de micrófono correcta esté seleccionada en `Settings > Radio Setup...` y que la radio no esté en un modo que desactive el micrófono.
- **● REC no hace nada al hacer clic** — No hay ninguna ranura seleccionada. Haga clic primero en una fila de ranura, luego haga clic en **● REC**.
- **El estado muestra Recording pero no se captura audio** — Verifique que el micrófono no esté silenciado a nivel del sistema operativo y que el dispositivo de entrada de audio esté enrutado correctamente a través de la radio.
- **Las teclas de función no responden en el panel DVK** — La porción activa debe estar en un modo de voz para que los atajos de teclas de función de DVK estén activos. Si la porción está en modo CW, los atajos de teclado de CWX están activos en su lugar.
- **La transferencia de WAV falla con "Transfer failed"** — Si falla la carga o descarga de un archivo WAV, la etiqueta de estado muestra un mensaje que comienza con "Transfer failed". Verifique que el archivo sea un WAV Mono válido de 16 bits con una frecuencia de muestreo de 8-48 kHz. Las interrupciones de red durante la transferencia también pueden causar este error.

## Relacionado

- [Digital Voice Keyer overview](overview.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Rename a slot](rename-a-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
