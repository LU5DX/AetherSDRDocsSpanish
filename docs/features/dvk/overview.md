# Descripción general del Pulsador de Voz Digital

El Pulsador de Voz Digital (DVK) permite grabar, almacenar y reproducir hasta 12 ranuras de pulsador de voz en una radio Flex conectada. Úselo para enviar audio pregrabado o grabado en vivo al aire sin necesidad de activar manualmente el micrófono, o para previsualizar las grabaciones localmente antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El panel DVK no está disponible sin una conexión de radio activa.
- Debe estar activo un modo de voz, o DVK debe estar habilitado, para que el panel aparezca en la ventana principal.

## Cómo funciona

El panel DVK aparece en la ventana principal de AetherSDR cuando un modo de voz está activo. Muestra 12 ranuras dispuestas en una cuadrícula desplazable. Cada ranura muestra un botón de tecla F (F1 a F12), una etiqueta de nombre, una etiqueta de duración y una barra de progreso que se activa durante la grabación o reproducción.

Al hacer clic en un botón de tecla F, se selecciona esa ranura y se inicia la reproducción si la ranura contiene una grabación. Al hacer clic nuevamente mientras se reproduce, se detiene la reproducción. El mismo comportamiento está disponible desde el teclado usando F1 a F12. Al presionar Escape se detiene la operación que esté activa en ese momento.

Los cuatro botones de transporte en la parte inferior del panel — ● REC, ■ STOP, ▶ PLAY y ◀ PREV — actúan sobre la ranura que esté seleccionada en ese momento. Un indicador de estado en la parte inferior del panel muestra el estado actual del DVK: Inactivo, Grabando o Reproduciendo.

Las ranuras se pueden llenar grabando directamente a través de la radio o subiendo un archivo WAV existente. Al hacer clic derecho en cualquier fila de ranura, se abre un menú contextual para renombrar la ranura o subir un WAV. Al hacer doble clic en la etiqueta de nombre de la ranura, también se abre el cambio de nombre en línea.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Botones de ranura F1 … F12 | Selecciona la ranura y alterna la reproducción al aire. Haga clic derecho en la fila para renombrar o subir un WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre asignado a cada ranura. | Grabación 1 … Grabación 12 |
| Etiquetas de duración de ranura | Muestra la duración grabada de la ranura, o "Vacía" si la ranura no tiene contenido. | Vacía |
| Barras de progreso de ranura | Muestra el progreso de reproducción o grabación en vivo. Oculta cuando la ranura está inactiva. | — |
| ● REC | Inicia la grabación en la ranura seleccionada. El botón permanece resaltado mientras la grabación está en curso. | — |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | — |
| ▶ PLAY | Reproduce la ranura seleccionada al aire. El botón permanece resaltado durante la reproducción. No tiene efecto si la ranura está vacía. | — |
| ◀ PREV | Previsualiza la ranura seleccionada a través del altavoz local sin transmitir. No tiene efecto si la ranura está vacía. | — |
| Editar nombre | Campo de texto en línea para renombrar una ranura, activado a través del menú contextual o haciendo doble clic en la etiqueta de nombre. | — |
| Indicador de estado | Muestra el estado actual del DVK: Inactivo, Grabando o Reproduciendo. | Inactivo |

## Consejos

- Presionar una tecla F mientras esa ranura ya se está reproduciendo detiene la reproducción, por lo que la misma tecla inicia y detiene una ranura.
- Presionar Escape cancela un cambio de nombre activo sin guardar, o detiene la grabación, reproducción o vista previa actual si no hay un cambio de nombre en curso.
- El color de la barra de progreso indica la operación en curso: rojo para grabación, verde para reproducción y azul para vista previa.

## Relacionado

- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Reproducir una ranura de pulsador de voz almacenada](play-a-stored-voice-keyer-slot.md)
- [Previsualizar una ranura sin transmitir](preview-a-slot-without-transmitting.md)
- [Detener una reproducción en curso](stop-a-playback-in-progress.md)
- [Renombrar una ranura](rename-a-slot.md)
- [Subir un archivo WAV a una ranura](upload-a-wav-file-into-a-slot.md)
