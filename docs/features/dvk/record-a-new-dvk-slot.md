# Grabar un nuevo espacio de DVK

Use el panel del Digital Voice Keyer para grabar su voz en uno de hasta 8 espacios, que luego podrá reproducir al aire con un solo clic o pulsando una tecla F.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel DVK solo está disponible cuando hay una conexión activa con el radio.
- El panel DVK debe estar visible en la ventana principal. Si no se muestra, cambie a un modo de voz o active DVK en el radio.
- Su micrófono debe estar configurado y funcionando a través de la ruta de audio del radio.

## Pasos

1. En el panel DVK, haga clic en la fila del espacio donde desea grabar (F1 a F8). La fila seleccionada se resalta con un borde azul.
2. Haga clic en **● REC**. El botón se vuelve rojo y el indicador de estado cambia a **Recording**. Aparece la barra de progreso del espacio y avanza a medida que se captura el audio.
3. Hable su mensaje en el micrófono.
4. Haga clic en **■ STOP** cuando haya terminado. El indicador de estado vuelve a **Idle**, la barra de progreso desaparece y la etiqueta de duración del espacio se actualiza de **Empty** para mostrar la duración grabada.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de espacio F1 … F8 | Selecciona y reproduce ese espacio; clic derecho para renombrar o subir un WAV. | — |
| Etiquetas de nombre del espacio | Muestra el nombre de cada espacio. | `Recording <n>` |
| Etiquetas de duración del espacio | Muestra la duración de la grabación o **Empty** si el espacio no tiene audio. | Empty |
| Barras de progreso del espacio | Muestra el progreso de grabación o reproducción en vivo. Oculto cuando está inactivo. | — |
| **● REC** | Inicia la grabación en el espacio seleccionado. Se vuelve rojo mientras está activo. | — |
| **■ STOP** | Detiene la grabación o reproducción. | — |
| **▶ PLAY** | Reproduce el espacio seleccionado al aire. | — |
| **◀ PREV** | Previsualiza el espacio seleccionado a través del altavoz local sin transmitir. | — |

## Consejos

- El espacio 1 está seleccionado por defecto cuando el panel DVK se abre por primera vez. Si hace clic en **● REC** sin seleccionar un espacio diferente, la grabación se guarda en el espacio 1.
- Presionar Escape cancela la grabación con el mismo efecto que **■ STOP**.
- Puede renombrar un espacio después de grabar haciendo clic derecho en su fila y eligiendo renombrar en el menú contextual. La etiqueta del nombre del espacio se puede editar en línea.
- Los atajos de teclas F (F1–F8 y Escape) están activos siempre que el slice activo esté en un modo de voz. El panel DVK no necesita estar visible para que los atajos funcionen. Si cambia a un modo CW, los atajos de DVK se desactivan automáticamente y los atajos de CWX se activan, evitando conflictos.
- Los botones de teclas F solo activan la reproducción si el espacio ya contiene una grabación. Un espacio que aún muestra **Empty** en la etiqueta de duración no se reproducirá cuando se presione su tecla F.

## Solución de problemas

- **La etiqueta de duración permanece Empty después de grabar** — Es posible que el radio no haya recibido audio. Verifique que la entrada de micrófono correcta esté seleccionada en `Settings > Radio Setup...` y que el radio no esté en un modo que desactive el micrófono.
- **● REC no hace nada al hacer clic** — No hay ningún espacio seleccionado. Haga clic primero en una fila de espacio y luego haga clic en **● REC**.
- **El botón ● REC se activa pero la grabación no comienza** — El radio rechazó el comando de inicio de grabación. La etiqueta de estado muestra brevemente un mensaje de fallo como "Status: rec_start (slot 2) failed — reason text" antes de volver a **Idle**. Esto puede ocurrir si el radio está ocupado, el espacio ya está en uso o la ruta de audio no está lista. Verifique que el radio esté en un modo de voz y que no esté grabando o reproduciendo otro espacio.
- **El estado muestra Recording pero no se captura audio** — Verifique que el micrófono no esté silenciado a nivel del sistema operativo y que el dispositivo de entrada de audio esté enrutado correctamente a través del radio.
- **Las teclas F no responden en el panel DVK** — El slice activo debe estar en un modo de voz para que los atajos de teclas F de DVK estén activos. Si el slice está en modo CW, los atajos de teclado de CWX están activos.
- **La transferencia de WAV falla con "Transfer failed"** — Si la carga o descarga de un archivo WAV falla, la etiqueta de estado muestra un mensaje que comienza con "Transfer failed". Verifique que el archivo sea un WAV Mono de 16 bits válido con una frecuencia de muestreo de 8-48 kHz. Las interrupciones de red durante la transferencia también pueden causar este error.

## Relacionado

- [Digital Voice Keyer overview](overview.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Rename a slot](rename-a-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
