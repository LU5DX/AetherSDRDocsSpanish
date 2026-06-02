# Reproducir una ranura de grabación de voz guardada

Use el panel de grabación de voz digital (Digital Voice Keyer) para transmitir una grabación almacenada al aire. Al activar una ranura, se pone en marcha el equipo y reproduce el audio a través de la rebanada de transmisión seleccionada.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El panel DVK requiere una conexión activa con el equipo.
- La ranura destino debe contener una grabación. Las ranuras que muestran "Empty" en la etiqueta de duración no se pueden reproducir.
- El equipo debe estar en un modo de voz (SSB, AM, FM) para que el panel DVK aparezca en la ventana principal.

## Pasos

1. Localice el panel Digital Voice Keyer en el área central de la ventana principal.
2. Identifique la ranura que desea reproducir. Verifique que su etiqueta de duración muestre un valor de tiempo, no "Empty".
3. Haga clic en la fila de la ranura para seleccionarla. La fila seleccionada se resalta con el color de acento.
4. Reproduzca la ranura usando uno de estos métodos:
   - Haga clic en el botón **▶ PLAY** para reproducir la ranura seleccionada actualmente.
   - Haga clic directamente en el botón **F1** a **F8** de la ranura para seleccionarla y reproducirla en una sola acción.
   - Presione la tecla F correspondiente en su teclado (F1–F8) para seleccionar y reproducir esa ranura.
5. La barra de progreso de la ranura aparece y avanza durante la reproducción. El indicador de estado cambia de "Idle" a "Playing". El botón de tecla F de la ranura activa se resalta.
6. La reproducción se detiene automáticamente cuando termina la grabación. Para detenerla antes, haga clic en **■ STOP** o presione Escape.

## Funciones de cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| **F1 … F8** botones de ranura | Selecciona y reproduce esa ranura; si la ranura ya se está reproduciendo, volver a hacer clic la detiene. Clic derecho para renombrar o subir un archivo WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o "Empty" si la ranura no tiene contenido. | `Empty` |
| Barras de progreso de ranura | Muestra el progreso de reproducción o grabación en vivo. | Oculto |
| **▶ PLAY** | Reproduce la ranura seleccionada. No tiene efecto si la ranura está vacía. | — |
| **■ STOP** | Detiene la grabación o reproducción. | — |
| **◀ PREV** | Previsualiza la ranura a través del altavoz local sin transmitir. | — |
| **● REC** | Inicia la grabación en la ranura seleccionada. | — |
| **Editar nombre** | Campo de texto en línea para renombrar una ranura, activado mediante el menú contextual de clic derecho. | — |

## Indicador de estado

El panel muestra una etiqueta de estado que cambia según la actividad actual:

| Estado | Significado |
|---|---|
| **Status: Idle** | No hay grabación ni reproducción en curso. |
| **Status: Recording** | Una ranura está grabando activamente. |
| **Status: Playing** | Una ranura se está reproduciendo activamente. |

## Consejos

- Hacer clic en un botón **F1–F8** mientras esa ranura ya se está reproduciendo detiene la reproducción en lugar de reiniciarla.
- Presionar la tecla F correspondiente en su teclado equivale a hacer clic en el botón **F1–F8** en pantalla. Se admiten las teclas F1 a F8.
- Para escuchar una ranura a través de su altavoz local sin transmitir, use **◀ PREV** en lugar de **▶ PLAY**.
- Los atajos de teclado (F1–F8 y Escape) permanecen activos incluso cuando el panel DVK está oculto, siempre que la rebanada activa esté en un modo de voz (SSB, AM, FM). Cuando la rebanada activa cambia a modo CW, los atajos de tecla F del panel CWX se activan en su lugar. Esto garantiza que no haya conflictos de atajos.
- Si cambia al panel CWX mientras el panel DVK sigue visible, los atajos del DVK permanecen activos solo si la rebanada está en un modo de voz. El panel CWX toma el control de los atajos de tecla F cuando la rebanada cambia a modo CW.
- El panel usa el tema visual actual para los colores, incluidos los bordes de las ranuras, el texto y el color de acento para los elementos seleccionados.

## Solución de problemas

- **▶ PLAY no hace nada** — La ranura seleccionada está vacía. La etiqueta de duración mostrará "Empty". Grabe audio o suba un archivo WAV a la ranura primero.
- **Presionar una tecla F no tiene efecto** — Los atajos del panel DVK se habilitan según el modo de la rebanada activa, no según la visibilidad del panel. Asegúrese de que la rebanada activa esté en un modo de voz (SSB, AM, FM). Si la rebanada está en modo CW, los atajos del panel CWX tienen prioridad.
- **Los atajos de teclado funcionan de forma inesperada** — Si el panel DVK y el panel CWX están visibles, solo están activos los atajos correspondientes al modo de la rebanada activa. Los atajos del otro panel están deshabilitados.

## Relacionados

- [Resumen del grabador de voz digital (Digital Voice Keyer)](overview.md)
- [Previsualizar una ranura sin transmitir](preview-a-slot-without-transmitting.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
- [Subir un archivo WAV a una ranura](upload-a-wav-file-into-a-slot.md)
