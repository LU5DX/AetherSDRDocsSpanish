# Descripción general del Digital Voice Keyer

El Digital Voice Keyer (DVK) le permite grabar, almacenar y reproducir hasta 12 espacios de grabación de voz en una radio Flex conectada. Úselo para enviar audio pregrabado o grabado en vivo al aire sin necesidad de activar manualmente el micrófono, o para previsualizar las grabaciones localmente antes de transmitir.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex. El panel DVK no está disponible sin una conexión activa a la radio.
- Debe estar activo un modo de voz, o DVK debe estar habilitado, para que el panel aparezca en la ventana principal.

## Cómo funciona

El panel DVK aparece en la ventana principal de AetherSDR cuando hay un modo de voz activo. Muestra 12 espacios organizados en una cuadrícula desplazable. Cada espacio muestra un botón de tecla F (F1 a F12), una etiqueta de nombre, una etiqueta de duración y una barra de progreso que se activa durante la grabación o reproducción.

Al hacer clic en un botón de tecla F, se selecciona ese espacio y se inicia la reproducción si el espacio contiene una grabación. Al hacer clic nuevamente mientras se reproduce, se detiene la reproducción. El mismo comportamiento está disponible desde el teclado usando F1 a F12, pero solo mientras el panel DVK esté visible. Los atajos de teclado están desactivados cuando el panel DVK está oculto para evitar conflictos con otros paneles que usan las mismas teclas F (como el panel CWX). Al presionar Escape se detiene la operación que esté activa en ese momento.

Los cuatro botones de transporte en la parte inferior del panel — ● REC, ■ STOP, ▶ PLAY y ◀ PREV — actúan sobre el espacio que esté seleccionado actualmente. Un indicador de estado en la parte inferior del panel muestra el estado actual del DVK: Idle, Recording o Playing.

Los espacios se pueden llenar grabando directamente a través de la radio o subiendo un archivo WAV existente. Al hacer clic derecho en cualquier fila de espacio, se abre un menú contextual para renombrar el espacio o subir un WAV. Al hacer doble clic en la etiqueta de nombre del espacio también se abre la opción de renombrar en línea.

## Función de cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de espacio F1 … F8 | Selecciona el espacio y alterna la reproducción al aire. Haga clic derecho en la fila para renombrar o subir un WAV. Los atajos de teclado F1-F12 solo funcionan mientras el panel DVK está visible. | — |
| Etiquetas de nombre de espacio | Muestra el nombre asignado a cada espacio. | Recording 1 … Recording 12 |
| Etiquetas de duración de espacio | Muestra la duración grabada del espacio, o "Empty" si el espacio no tiene contenido. | Empty |
| Barras de progreso de espacio | Muestra el progreso en vivo de la reproducción o grabación. Ocultas cuando el espacio está inactivo. | — |
| ● REC | Inicia la grabación en el espacio seleccionado. El botón permanece resaltado mientras la grabación está en curso. | — |
| ■ STOP | Detiene cualquier grabación, reproducción o vista previa activa. | — |
| ▶ PLAY | Reproduce el espacio seleccionado al aire. El botón permanece resaltado durante la reproducción. No tiene efecto si el espacio está vacío. | — |
| ◀ PREV | Previsualiza el espacio seleccionado a través del altavoz local sin transmitir. No tiene efecto si el espacio está vacío. | — |
| Edición de nombre | Campo de texto en línea para renombrar un espacio, activado mediante el menú contextual o haciendo doble clic en la etiqueta de nombre. | — |
| Indicador de estado | Muestra el estado actual del DVK: Idle, Recording o Playing. | Idle |

## Consejos

- Presionar una tecla F mientras ese espacio ya se está reproduciendo detiene la reproducción, por lo que la misma tecla inicia y detiene un espacio.
- Presionar Escape cancela un cambio de nombre activo sin guardar, o detiene la grabación, reproducción o vista previa actual si no hay un cambio de nombre en curso.
- El panel DVK y el panel CWX comparten los mismos atajos de teclas F, pero solo un panel puede estar visible a la vez. Los atajos de teclado se habilitan automáticamente cuando se muestra el panel DVK y se deshabilitan cuando está oculto, lo que garantiza que no haya conflictos.
- El color de la barra de progreso indica la operación en curso: rojo para grabación, verde para reproducción y azul para vista previa.

## Relacionados

- [Record a new DVK slot](record-a-new-dvk-slot.md)
- [Play a stored voice-keyer slot](play-a-stored-voice-keyer-slot.md)
- [Preview a slot without transmitting](preview-a-slot-without-transmitting.md)
- [Stop a playback in progress](stop-a-playback-in-progress.md)
- [Rename a slot](rename-a-slot.md)
- [Upload a WAV file into a slot](upload-a-wav-file-into-a-slot.md)
