# Reproducir una ranura del teclado de voz digital almacenada

Use el panel Digital Voice Keyer para transmitir una grabación almacenada al aire. Al activar una ranura, se cierra la PTT del equipo y el audio se reproduce a través del slice de transmisión seleccionado.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. El panel DVK requiere una conexión de radio activa.
- La ranura de destino debe contener una grabación. Las ranuras que muestran "Empty" en la etiqueta de duración no pueden reproducirse.
- El equipo debe estar en un modo de voz (SSB, AM, FM) para que el panel DVK aparezca en la ventana principal.

## Pasos

1. Localice el panel Digital Voice Keyer en el área central de la ventana principal.
2. Identifique la ranura que desea reproducir. Verifique que su etiqueta de duración muestre un valor de tiempo y no "Empty".
3. Haga clic en la fila de la ranura para seleccionarla. La fila seleccionada se resalta con un borde azul.
4. Reproduzca la ranura mediante uno de estos métodos:
   - Haga clic en el botón **▶ PLAY** para reproducir la ranura actualmente seleccionada.
   - Haga clic directamente en el botón **F1** a **F8** de la ranura para seleccionarla y reproducirla en una sola acción.
   - Presione la tecla F correspondiente en su teclado (F1–F8) para seleccionar y reproducir esa ranura.
5. La barra de progreso de la ranura aparece y avanza durante la reproducción. El indicador de estado cambia de "Idle" a "Playing". El botón de tecla F de la ranura activa se resalta.
6. La reproducción se detiene automáticamente al finalizar la grabación. Para detenerla antes, haga clic en **■ STOP** o presione Escape.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de ranura **F1 … F8** | Selecciona y reproduce esa ranura; si la ranura ya está reproduciéndose, hacer clic de nuevo la detiene. | — |
| Etiquetas de nombre de ranura | Muestra el nombre de cada ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación o "Empty" si la ranura no tiene contenido. | `Empty` |
| Barras de progreso de ranura | Muestra el progreso de reproducción en tiempo real. Visible únicamente durante la reproducción activa. | Oculta |
| **▶ PLAY** | Reproduce la ranura seleccionada. No tiene efecto si la ranura está vacía. | — |
| **■ STOP** | Detiene la reproducción en curso. | — |

## Consejos

- Hacer clic en un botón **F1–F8** mientras esa ranura ya está reproduciéndose detiene la reproducción en lugar de reiniciarla.
- Presionar la tecla F correspondiente en el teclado equivale a hacer clic en el botón **F1–F8** en pantalla. Se admiten de F1 a F8.
- Para escuchar una ranura a través del altavoz local sin transmitir, use **◀ PREV** en lugar de **▶ PLAY**.

## Solución de problemas

- **▶ PLAY no hace nada** — La ranura seleccionada está vacía. La etiqueta de duración mostrará "Empty". Primero grabe audio o cargue un archivo WAV en la ranura.
- **La tecla F no tiene efecto** — El panel DVK debe tener el foco del teclado, o la ranura en esa posición está vacía.

## Relacionados

- [Descripción general del Digital Voice Keyer](overview.md)
- [Vista previa de una ranura sin transmitir](preview-a-slot-without-transmitting.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
- [Cargar un archivo WAV en una ranura](upload-a-wav-file-into-a-slot.md)
