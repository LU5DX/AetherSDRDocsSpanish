# Reproducir una ranura de grabación de voz almacenada

Utilice el panel del keyer de voz digital (DVK) para transmitir una grabación almacenada al aire. Al activar una ranura, se pone en transmisión la radio y se reproduce el audio a través del segmento de transmisión seleccionado.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK requiere una conexión activa con la radio.
- La ranura de destino debe contener una grabación. Las ranuras que muestran "Empty" en la etiqueta de duración no se pueden reproducir.
- La radio debe estar en un modo de voz (SSB, AM, FM) para que el panel DVK aparezca en la ventana principal.

## Pasos

1. Localice el panel Digital Voice Keyer en el área central de la ventana principal.
2. Identifique la ranura que desea reproducir. Verifique que su etiqueta de duración muestre un valor de tiempo, no "Empty".
3. Haga clic en la fila de la ranura para seleccionarla. La fila seleccionada se resalta con el color de acento.
4. Reproduzca la ranura usando uno de estos métodos:
   - Haga clic en el botón **▶ PLAY** para reproducir la ranura seleccionada actualmente.
   - Haga clic directamente en el botón **F1** a **F8** de la ranura para seleccionarla y reproducirla en una sola acción.
   - Presione la tecla F correspondiente en su teclado (F1–F8) para seleccionar y reproducir esa ranura.
5. La barra de progreso de la ranura aparece y avanza durante la reproducción. El indicador de estado cambia de "Idle" a "Playing". El botón de tecla F de la ranura activa se resalta.
6. La reproducción se detiene automáticamente cuando la grabación termina. Para detenerla antes, haga clic en **■ STOP** o presione Escape.

## Función de cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| **F1 … F8** botones de ranura | Selecciona y reproduce esa ranura; si la ranura ya se está reproduciendo, hacer clic la detiene. Haga clic derecho para renombrar o subir un archivo WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la longitud de la grabación o "Empty" si la ranura no tiene contenido. | `Empty` |
| Barras de progreso de ranura | Muestra el progreso de reproducción o grabación en vivo. | Oculto |
| **▶ PLAY** | Reproduce la ranura seleccionada. No tiene efecto si la ranura está vacía. | — |
| **■ STOP** | Detiene la grabación o reproducción. | — |
| **◀ PREV** | Previsualiza la ranura a través del altavoz local sin transmitir. | — |
| **● REC** | Inicia la grabación en la ranura seleccionada. | — |
| **Rename edit** | Campo de texto en línea para renombrar una ranura, activado mediante el menú contextual de clic derecho. | — |

## Indicador de estado

El panel muestra una etiqueta de estado que cambia según la actividad actual:

| Estado | Significado |
|---|---|
| **Status: Idle** | No hay grabación ni reproducción en curso. |
| **Status: Recording** | Una ranura está grabando activamente. |
| **Status: Playing** | Una ranura se está reproduciendo activamente. |
| **Status: <verb> (slot <n>) failed — <message>** | La radio rechazó un comando de grabación (por ejemplo, la radio no estaba en un modo que admita grabación). El verbo indica la acción intentada (ej. "rec_start") y el mensaje explica el fallo. El estado vuelve a Idle después de un momento. |

## Consejos

- Hacer clic en un botón **F1–F8** mientras esa ranura ya se está reproduciendo detiene la reproducción en lugar de reiniciarla.
- Presionar la tecla F correspondiente en su teclado equivale a hacer clic en el botón **F1–F8** en pantalla. Se admiten F1 a F8.
- Para escuchar una ranura a través del altavoz local sin transmitir, use **◀ PREV** en lugar de **▶ PLAY**.
- Los atajos de teclado (F1–F8 y Escape) permanecen activos incluso cuando el panel DVK está oculto, siempre que el segmento activo esté en un modo de voz (SSB, AM, FM). Cuando el segmento activo cambia al modo CW, los atajos de tecla F del panel CWX se activan en su lugar. Esto garantiza que no haya conflictos de atajos.
- Si cambia al panel CWX mientras el panel DVK sigue visible, los atajos del DVK solo permanecen activos si el segmento está en un modo de voz. El panel CWX toma el control de los atajos de tecla F cuando el segmento cambia al modo CW.
- El panel utiliza los colores del tema visual actual, incluidos los bordes de las ranuras, el texto y el color de acento para los elementos seleccionados.

## Solución de problemas

- **▶ PLAY no hace nada** — La ranura seleccionada está vacía. La etiqueta de duración mostrará "Empty". Primero grabe audio o suba un archivo WAV a la ranura.
- **La tecla F no tiene efecto** — Los atajos del panel DVK se habilitan según el modo del segmento activo, no según la visibilidad del panel. Asegúrese de que el segmento activo esté en un modo de voz (SSB, AM, FM). Si el segmento está en modo CW, los atajos del panel CWX tienen prioridad.
- **Los atajos de teclado funcionan inesperadamente** — Si ambos paneles DVK y CWX están visibles, solo están activos los atajos correspondientes al modo del segmento activo. Los atajos del otro panel están desactivados.
- **El botón ● REC parece activarse pero la grabación no comienza** — Es posible que la radio haya rechazado el comando de grabación. La etiqueta de estado muestra brevemente un mensaje de fallo que explica el motivo (por ejemplo, la radio no estaba en un modo de voz). El botón vuelve a su estado normal automáticamente.

## Relacionado

- [Digital Voice Keyer overview](overview.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
