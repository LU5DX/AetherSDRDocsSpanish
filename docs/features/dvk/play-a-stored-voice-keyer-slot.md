# Reproducir una ranura guardada del grabador de voz digital

Utilice el panel del Grabador de Voz Digital (DVK) para transmitir una grabación almacenada en el aire. Al activar una ranura, la radio se pone en transmisión y reproduce el audio a través del slice de transmisión seleccionado.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK requiere una conexión activa con la radio.
- La ranura de destino debe contener una grabación. Las ranuras que muestran "Empty" (Vacío) en la etiqueta de duración no se pueden reproducir.
- La radio debe estar en un modo de voz (SSB, AM, FM) para que el panel DVK aparezca en la ventana principal.

## Pasos

1. Localice el panel Digital Voice Keyer en el área central de la ventana principal.
2. Identifique la ranura que desea reproducir. Verifique que su etiqueta de duración muestre un valor de tiempo, no "Empty".
3. Haga clic en la fila de la ranura para seleccionarla. La fila seleccionada se resalta con un borde azul.
4. Reproduzca la ranura usando uno de estos métodos:
   - Haga clic en el botón **▶ PLAY** para reproducir la ranura seleccionada actualmente.
   - Haga clic directamente en el botón **F1** a **F8** de la ranura para seleccionarla y reproducirla en una sola acción.
   - Presione la tecla F correspondiente en su teclado (F1–F8) para seleccionar y reproducir esa ranura.
5. La barra de progreso de la ranura aparece y avanza durante la reproducción. El indicador de estado cambia de "Idle" (Inactivo) a "Playing" (Reproduciendo). El botón de la tecla F de la ranura activa se resalta.
6. La reproducción se detiene automáticamente cuando termina la grabación. Para detenerla antes, haga clic en **■ STOP** o presione Escape.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| **F1 … F8** botones de ranura | Selecciona y reproduce esa ranura; si la ranura ya se está reproduciendo, al hacer clic nuevamente se detiene. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o "Empty" si la ranura no tiene contenido. | `Empty` |
| Barras de progreso de ranura | Muestra el progreso de la reproducción en vivo. Visible solo durante la reproducción activa. | Oculto |
| **▶ PLAY** | Reproduce la ranura seleccionada. No tiene efecto si la ranura está vacía. | — |
| **■ STOP** | Detiene la reproducción en curso. | — |
| **◀ PREV** | Previsualiza la ranura a través del altavoz local sin transmitir. | — |
| **● REC** | Inicia la grabación en la ranura seleccionada. | — |

## Consejos

- Hacer clic en un botón **F1–F8** mientras esa ranura ya se está reproduciendo detiene la reproducción en lugar de reiniciarla.
- Presionar la tecla F correspondiente en su teclado es equivalente a hacer clic en el botón **F1–F8** en pantalla. Se admiten las teclas F1 a F8.
- Para escuchar una ranura a través de su altavoz local sin transmitir, use **◀ PREV** en lugar de **▶ PLAY**.
- Los atajos de teclado (F1–F8 y Escape) están activos solo mientras el panel DVK está visible. Si cambia al panel CWX en la misma área de división, el panel CWX toma el control de los mismos atajos de tecla F. Ocultar el panel DVK desactiva automáticamente sus atajos para evitar conflictos.

## Solución de problemas

- **▶ PLAY no hace nada** — La ranura seleccionada está vacía. La etiqueta de duración mostrará "Empty". Grabe audio o cargue un archivo WAV en la ranura primero.
- **La tecla F no tiene efecto** — El panel DVK debe estar visible en la ventana principal. Si el panel CWX se muestra en su lugar, sus atajos de tecla F tienen prioridad. Asegúrese de que el panel DVK sea el panel activo en el área de división.

## Relacionado

- [Digital Voice Keyer overview](overview.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
