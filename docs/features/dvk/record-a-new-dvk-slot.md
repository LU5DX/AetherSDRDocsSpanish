# Grabar un nuevo espacio de DVK

Use el panel del Keyer de Voz Digital para grabar su voz en uno de hasta 12 espacios, que luego podrá reproducir al aire con un solo clic o pulsando una tecla F.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel DVK solo está disponible cuando hay una conexión activa con el radio.
- El panel DVK debe estar visible en la ventana principal. Si no se muestra, cambie a un modo de voz o active el DVK en el radio.
- Su micrófono debe estar configurado y funcionando a través de la ruta de audio del radio.

## Pasos

1. En el panel DVK, haga clic en la fila del espacio donde desea grabar (F1 a F12). La fila seleccionada se resalta con un borde azul.
2. Haga clic en **● REC**. El botón se vuelve rojo y el indicador de estado cambia a **Recording**. Aparece la barra de progreso del espacio, que avanza a medida que se captura el audio.
3. Hable su mensaje al micrófono.
4. Haga clic en **■ STOP** cuando haya terminado. El indicador de estado vuelve a **Idle**, la barra de progreso desaparece y la etiqueta de duración del espacio cambia de **Empty** para mostrar la longitud grabada.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de espacio F1 … F12 | Selecciona y reproduce ese espacio; haga clic derecho para renombrar o subir un archivo WAV. | — |
| Etiquetas de nombre de espacio | Muestra el nombre de cada espacio. | `Recording <n>` |
| Etiquetas de duración de espacio | Muestra la longitud de la grabación o **Empty** si el espacio no tiene audio. | Empty |
| Barras de progreso de espacio | Muestra el progreso de grabación o reproducción en vivo. Ocultas cuando está inactivo. | — |
| **● REC** | Inicia la grabación en el espacio seleccionado. Se vuelve rojo mientras está activo. | — |
| **■ STOP** | Detiene la grabación o reproducción. | — |
| **▶ PLAY** | Reproduce el espacio seleccionado al aire. | — |
| **◀ PREV** | Previsualiza el espacio seleccionado a través del altavoz local sin transmitir. | — |

## Consejos

- El espacio 1 está seleccionado por defecto cuando el panel DVK se abre por primera vez. Si hace clic en **● REC** sin seleccionar un espacio diferente, la grabación se guardará en el espacio 1.
- Presionar Escape cancela la grabación con el mismo efecto que **■ STOP**.
- Puede renombrar un espacio después de grabarlo haciendo clic derecho en su fila y eligiendo renombrar en el menú contextual. La etiqueta de nombre del espacio se puede editar en línea.
- Los botones de tecla F solo activan la reproducción si el espacio ya contiene una grabación. Un espacio que todavía muestre **Empty** en la etiqueta de duración no se reproducirá cuando se presione su tecla F.

## Solución de problemas

- **La etiqueta de duración permanece Empty después de grabar** — Es posible que el radio no haya recibido audio. Verifique que la entrada de micrófono correcta esté seleccionada en `Settings > Radio Setup...` y que el radio no esté en un modo que desactive el micrófono.
- **Al hacer clic en ● REC no sucede nada** — No hay ningún espacio seleccionado. Haga clic primero en una fila de espacio, luego haga clic en **● REC**.
- **El estado muestra Recording pero no se captura audio** — Verifique que el micrófono no esté silenciado a nivel del sistema operativo y que el dispositivo de entrada de audio esté enrutado correctamente a través del radio.

## Relacionados

- [Digital Voice Keyer overview](overview.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Rename a slot](rename-a-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
