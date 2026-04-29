# Descripción general del Digital Voice Keyer

El Digital Voice Keyer (DVK) permite grabar, almacenar y reproducir hasta 12 ranuras de voz en una radio Flex conectada. Úselo para enviar audio pregrabado o grabado en vivo al aire sin accionar manualmente el micrófono, o para previsualizar grabaciones localmente antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El panel DVK no está disponible sin una conexión de radio activa.
- Debe estar activo un modo de voz, o el DVK debe estar habilitado, para que el panel aparezca en la ventana principal.

## Cómo funciona

El panel DVK aparece en la ventana principal de AetherSDR cuando hay un modo de voz activo. Muestra 12 ranuras organizadas en una cuadrícula desplazable. Cada ranura presenta un botón de tecla de función (F1 a F12), una etiqueta de nombre, una etiqueta de duración y una barra de progreso que se activa durante la grabación o la reproducción.

Al hacer clic en un botón de tecla de función se selecciona esa ranura y se inicia la reproducción si la ranura contiene una grabación. Volver a hacer clic mientras está reproduciéndose detiene la reproducción. El mismo comportamiento está disponible desde el teclado usando F1 a F12. Al presionar Escape se detiene la operación que esté activa en ese momento.

Los cuatro botones de transporte en la parte inferior del panel — ● REC, ■ STOP, ▶ PLAY y ◀ PREV — actúan sobre la ranura que esté seleccionada en ese momento. Un indicador de estado en la parte inferior del panel muestra el estado actual del DVK: Idle, Recording o Playing.

Las ranuras se pueden llenar grabando directamente a través de la radio o cargando un archivo WAV existente. Al hacer clic derecho en cualquier fila de ranura se abre un menú contextual para renombrar la ranura o cargar un WAV. Al hacer doble clic en la etiqueta de nombre de la ranura también se abre la edición en línea del nombre.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de ranura F1 … F12 | Selecciona la ranura y activa o desactiva la reproducción al aire. Haga clic derecho en la fila para renombrar o cargar un WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre asignado a cada ranura. | Recording 1 … Recording 12 |
| Etiquetas de duración de ranura | Muestra la duración grabada de la ranura, o "Empty" si la ranura no tiene contenido. | Empty |
| Barras de progreso de ranura | Muestra el progreso en tiempo real de la reproducción o la grabación. Ocultas cuando la ranura está inactiva. | — |
| ● REC | Inicia la grabación en la ranura seleccionada. El botón permanece resaltado mientras la grabación está en curso. | — |
| ■ STOP | Detiene cualquier grabación, reproducción o previsualización activa. | — |
| ▶ PLAY | Reproduce la ranura seleccionada al aire. El botón permanece resaltado durante la reproducción. No tiene efecto si la ranura está vacía. | — |
| ◀ PREV | Previsualiza la ranura seleccionada a través del altavoz local sin transmitir. No tiene efecto si la ranura está vacía. | — |
| Campo de renombre | Campo de texto en línea para renombrar una ranura; se activa a través del menú contextual o haciendo doble clic en la etiqueta de nombre. | — |
| Indicador de estado | Muestra el estado actual del DVK: Idle, Recording o Playing. | Idle |

## Consejos

- Presionar una tecla de función mientras esa ranura ya está reproduciéndose detiene la reproducción, de modo que la misma tecla tanto inicia como detiene una ranura.
- Presionar Escape cancela un renombre activo sin guardar, o detiene la grabación, reproducción o previsualización en curso si no hay ningún renombre en progreso.
- El color de la barra de progreso indica la operación en curso: rojo para grabación, verde para reproducción y azul para previsualización.

## Relacionado

- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Reproducir una ranura de voz almacenada](play-a-stored-voice-keyer-slot.md)
- [Previsualizar una ranura sin transmitir](preview-a-slot-without-transmitting.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
- [Renombrar una ranura](rename-a-slot.md)
- [Cargar un archivo WAV en una ranura](upload-a-wav-file-into-a-slot.md)
