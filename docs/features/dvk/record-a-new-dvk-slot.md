# Grabar una nueva ranura de DVK

Utilice el panel del Digital Voice Keyer para grabar su voz en una de las hasta 8 ranuras, que luego podrá reproducir al aire con un solo clic o pulsando una tecla F.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El panel de DVK solo está disponible cuando hay una conexión activa con el equipo.
- El panel de DVK debe estar visible en la ventana principal. Si no se muestra, cambie a un modo de voz o habilite DVK en el equipo.
- Su micrófono debe estar configurado y funcionando a través de la ruta de audio del equipo.

## Pasos

1. En el panel de DVK, haga clic en la fila de la ranura en la que desea grabar (F1 a F8). La fila seleccionada se resalta con un borde azul.
2. Haga clic en **● REC**. El botón se vuelve rojo y el indicador de estado cambia a **Recording**. Aparece la barra de progreso de la ranura y avanza a medida que se captura el audio.
3. Hable su mensaje en el micrófono.
4. Haga clic en **■ STOP** cuando haya terminado. El indicador de estado vuelve a **Idle**, la barra de progreso desaparece y la etiqueta de duración de la ranura se actualiza de **Empty** a la longitud grabada.

## Función de cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; clic derecho para renombrar o subir un archivo WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la longitud de la grabación o **Empty** si la ranura no tiene audio. | Empty |
| Barras de progreso de ranura | Muestra el progreso en vivo de la grabación o reproducción. Ocultas cuando está inactivo. | — |
| **● REC** | Inicia la grabación en la ranura seleccionada. Se vuelve rojo mientras está activo. | — |
| **■ STOP** | Detiene la grabación o reproducción. | — |
| **▶ PLAY** | Reproduce la ranura seleccionada al aire. | — |
| **◀ PREV** | Previsualiza la ranura seleccionada por el altavoz local sin transmitir. | — |

## Consejos

- La ranura 1 está seleccionada por defecto cuando el panel de DVK se abre por primera vez. Si hace clic en **● REC** sin seleccionar una ranura diferente, la grabación se guarda en la ranura 1.
- Pulsar Escape cancela la grabación con el mismo efecto que **■ STOP**.
- Puede renombrar una ranura después de grabar haciendo clic derecho en su fila y eligiendo Rename en el menú contextual. La etiqueta del nombre de la ranura es editable en línea.
- Los atajos de teclas F (F1–F8 y Escape) solo están activos cuando el panel de DVK está visible. Si también utiliza el panel de CWX, sus atajos de teclas F se deshabilitan automáticamente mientras se muestra el panel de DVK, y viceversa, evitando conflictos.
- Los botones de teclas F solo activan la reproducción si la ranura ya contiene una grabación. Una ranura que aún muestra **Empty** en la etiqueta de duración no se reproducirá cuando se pulse su tecla F.

## Solución de problemas

- **La etiqueta de duración permanece en Empty después de grabar** — Es posible que el equipo no haya recibido audio. Verifique que la entrada de micrófono correcta esté seleccionada en `Settings > Radio Setup...` y que el equipo no esté en un modo que deshabilite el micrófono.
- **● REC no hace nada al hacer clic** — No hay ninguna ranura seleccionada. Haga clic en una fila de ranura primero, luego haga clic en **● REC**.
- **El estado muestra Recording pero no se captura audio** — Verifique que el micrófono no esté silenciado a nivel del sistema operativo y que el dispositivo de entrada de audio esté enrutado correctamente a través del equipo.
- **Las teclas F no responden en el panel de DVK** — El panel debe estar visible para que los atajos de teclas F estén activos. Si el panel está oculto u otro panel (como CWX) se muestra en su lugar, los atajos se deshabilitan automáticamente para evitar conflictos.

## Relacionado

- [Digital Voice Keyer overview](overview.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Rename a slot](rename-a-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
