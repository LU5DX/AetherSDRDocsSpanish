# Reproducir una ranura de grabación de voz guardada

Use el panel Digital Voice Keyer para transmitir una grabación almacenada al aire. Al activar una ranura, la radio se pone en transmisión y reproduce el audio a través del slice de transmisión seleccionado.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK requiere una conexión activa con la radio.
- La ranura de destino debe contener una grabación. Las ranuras que muestren "Empty" en la etiqueta de duración no pueden reproducirse.
- La radio debe estar en un modo de voz (SSB, AM, FM) para que el panel DVK aparezca en la ventana principal.

## Pasos

1. Localice el panel Digital Voice Keyer en el área central de la ventana principal.
2. Identifique la ranura que desea reproducir. Verifique que su etiqueta de duración muestre un valor de tiempo, no "Empty".
3. Haga clic en la fila de la ranura para seleccionarla. La fila seleccionada se resalta con un borde azul.
4. Reproduzca la ranura usando uno de estos métodos:
   - Haga clic en el botón **▶ PLAY** para reproducir la ranura seleccionada actualmente.
   - Haga clic directamente en el botón **F1** a **F8** de la ranura para seleccionarla y reproducirla en una sola acción.
   - Presione la tecla F correspondiente en su teclado (F1–F8) para seleccionar y reproducir esa ranura.
5. La barra de progreso de la ranura aparece y avanza durante la reproducción. El indicador de estado cambia de "Idle" a "Playing". El botón de tecla F de la ranura activa se resalta.
6. La reproducción se detiene automáticamente cuando termina la grabación. Para detenerla antes, haga clic en **■ STOP** o presione Escape.

## Función de cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| **F1 … F8** botones de ranura | Selecciona y reproduce esa ranura; si la ranura ya se está reproduciendo, al hacer clic nuevamente la detiene. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o "Empty" si la ranura no tiene contenido. | `Empty` |
| Barras de progreso de ranura | Muestra el progreso de la reproducción en vivo. Visible solo durante la reproducción activa. | Oculto |
| **▶ PLAY** | Reproduce la ranura seleccionada. No tiene efecto si la ranura está vacía. | — |
| **■ STOP** | Detiene la reproducción en curso. | — |
| **◀ PREV** | Previsualiza la ranura a través del altavoz local sin transmitir. | — |
| **● REC** | Inicia la grabación en la ranura seleccionada. | — |

## Consejos

- Hacer clic en un botón **F1–F8** mientras esa ranura ya se está reproduciendo detiene la reproducción en lugar de reiniciarla.
- Presionar la tecla F correspondiente en su teclado equivale a hacer clic en el botón **F1–F8** en pantalla. Se admiten F1 a F8.
- Para escuchar una ranura a través del altavoz local sin transmitir, use **◀ PREV** en lugar de **▶ PLAY**.
- Los atajos de teclado (F1–F8 y Escape) permanecen activos incluso cuando el panel DVK está oculto, siempre que el slice activo esté en un modo de voz (SSB, AM, FM). Cuando el slice activo cambia a modo CW, los atajos de teclas F del panel CWX se activan en su lugar. Esto garantiza que no haya conflictos de atajos.
- Si cambia al panel CWX mientras el panel DVK aún está visible, los atajos DVK permanecen activos solo si el slice está en un modo de voz. El panel CWX toma el control de los atajos de teclas F cuando el slice cambia a modo CW.

## Solución de problemas

- **▶ PLAY no hace nada** — La ranura seleccionada está vacía. La etiqueta de duración mostrará "Empty". Primero grabe audio o cargue un archivo WAV en la ranura.
- **La tecla F no tiene efecto** — Los atajos del panel DVK se habilitan según el modo del slice activo, no según la visibilidad del panel. Asegúrese de que el slice activo esté en un modo de voz (SSB, AM, FM). Si el slice está en modo CW, los atajos del panel CWX tienen prioridad.
- **Los atajos de teclado funcionan de manera inesperada** — Si tanto el panel DVK como el CWX están visibles, solo los atajos correspondientes al modo del slice activo están activos. Los atajos del otro panel están deshabilitados.

## Relacionados

- [Digital Voice Keyer overview](overview.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
