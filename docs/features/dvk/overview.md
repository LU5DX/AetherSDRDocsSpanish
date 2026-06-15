# Descripción general del Keyer de Voz Digital

El Keyer de Voz Digital (DVK) le permite grabar, almacenar y reproducir hasta 8 ranuras de keyer de voz en una radio Flex conectada. Úselo para enviar audio pregrabado o grabado en vivo al aire sin activar manualmente el micrófono, o para previsualizar grabaciones localmente antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El panel DVK no está disponible sin una conexión activa a la radio.
- Debe estar activo un modo de voz, o DVK debe estar habilitado, para que el panel aparezca en la ventana principal.

## Cómo funciona

El panel DVK aparece en la ventana principal de AetherSDR cuando un modo de voz está activo. Muestra 8 ranuras dispuestas en una cuadrícula desplazable. Cada ranura muestra un botón de tecla F (F1 a F8), una etiqueta de nombre, una etiqueta de duración y una barra de progreso que se activa durante la grabación o reproducción.

Al hacer clic en un botón de tecla F se selecciona esa ranura y se inicia la reproducción si la ranura contiene una grabación. Al hacer clic nuevamente mientras se está reproduciendo, se detiene la reproducción. El mismo comportamiento está disponible desde el teclado usando las teclas F1 a F8. Los atajos de teclado se habilitan según el modo de la franja activa: cuando una franja en modo de voz está activa, los atajos de DVK están habilitados y los de CWX están deshabilitados, y viceversa. Esto asegura que los atajos funcionen independientemente de la visibilidad del panel y evita conflictos entre paneles. Al presionar Escape se detiene la operación que esté actualmente activa.

Los cuatro botones de transporte en la parte inferior del panel — ● REC, ■ STOP, ▶ PLAY y ◀ PREV — actúan sobre la ranura que esté seleccionada en ese momento. Un indicador de estado en la parte inferior del panel muestra el estado actual del DVK: Inactivo, Grabando o Reproduciendo.

Las ranuras pueden poblarse grabando directamente a través de la radio o subiendo un archivo WAV existente. Al hacer clic derecho en cualquier fila de ranura se abre un menú contextual para renombrar la ranura o subir un WAV. Al hacer doble clic en la etiqueta de nombre de la ranura también se abre la opción de renombrar en línea.

Si la radio rechaza un comando solicitado (por ejemplo, si se rechaza el inicio de una grabación), el panel muestra un mensaje de fallo en el área de estado. Los botones también se liberan visualmente de inmediato para que no permanezcan en un estado presionado. El mensaje de fallo muestra qué verbo (Grabación, Reproducción o Vista previa) falló, qué ranura estuvo involucrada y el mensaje de rechazo de la radio. Después de una breve visualización, el estado vuelve al estado actual de inactivo/grabando/reproduciendo.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona la ranura y alterna la reproducción al aire. Haga clic derecho en la fila para renombrar o subir un WAV. Los atajos de teclado F1-F8 funcionan según el modo de la franja activa, independientemente de la visibilidad del panel. | — |
| Etiquetas de nombre de ranura | Muestra el nombre asignado a cada ranura. | Grabación 1 … Grabación 8 |
| Etiquetas de duración de ranura | Muestra la longitud grabada de la ranura, o "Vacía" si la ranura no tiene contenido. | Vacía |
| Barras de progreso de ranura | Muestra el progreso en vivo de la reproducción o grabación. Ocultas cuando la ranura está inactiva. | — |
| ● REC | Inicia la grabación en la ranura seleccionada. El botón permanece resaltado mientras la grabación está en curso. Si la radio rechaza el comando de inicio, el botón se libera inmediatamente y aparece un mensaje de fallo en el área de estado. | — |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | — |
| ▶ PLAY | Reproduce la ranura seleccionada al aire. El botón permanece resaltado durante la reproducción. No tiene efecto si la ranura está vacía. | — |
| ◀ PREV | Previsualiza la ranura seleccionada a través del altavoz local sin transmitir. No tiene efecto si la ranura está vacía. | — |
| Edición de nombre | Campo de texto en línea para renombrar una ranura, activado a través del menú contextual o haciendo doble clic en la etiqueta de nombre. | — |
| Indicador de estado | Muestra el estado actual del DVK: Inactivo, Grabando o Reproduciendo. Si un comando de la radio falla, se muestra un mensaje de fallo temporalmente antes de volver al estado actual. | Inactivo |

## Consejos

- Presionar una tecla F mientras esa ranura ya se está reproduciendo detiene la reproducción, por lo que la misma tecla inicia y detiene una ranura.
- Presionar Escape cancela un renombrado activo sin guardar, o detiene la grabación, reproducción o vista previa actual si no hay un renombrado en curso.
- El panel DVK y el panel CWX comparten los mismos atajos de teclas F. Los atajos se habilitan o deshabilitan según el modo de la franja activa (el modo de voz habilita los atajos de DVK, el modo CW habilita los atajos de CWX), asegurando que solo un conjunto esté activo a la vez. A diferencia de versiones anteriores, esto funciona independientemente de la visibilidad del panel.
- El color de la barra de progreso indica la operación en curso: rojo para grabación, verde para reproducción y azul para vista previa.
- Si la radio rechaza un comando DVK, el área de estado muestra brevemente un mensaje de fallo con el número de ranura y el motivo. Los botones de transporte se liberan inmediatamente para que pueda reintentar la operación sin tener que cancelar un estado de botón atascado.

## Relacionado

- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Reproducir una ranura de keyer de voz almacenada](play-a-stored-voice-keyer-slot.md)
- [Previsualizar una ranura sin transmitir](preview-a-slot-without-transmitting.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
- [Renombrar una ranura](rename-a-slot.md)
- [Subir un archivo WAV a una ranura](upload-a-wav-file-into-a-slot.md)
