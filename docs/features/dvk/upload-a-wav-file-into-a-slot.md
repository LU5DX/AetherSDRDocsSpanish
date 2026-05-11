# Cargar un archivo WAV en una ranura

Cargue un archivo WAV pregrabado desde su computadora a una de las ranuras del teclado de voz digital (DVK) para poder reproducirlo al aire sin necesidad de grabar en vivo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK solo está disponible cuando hay una conexión activa con la radio.
- El panel DVK debe estar visible en la ventana principal. Aparece cuando DVK está habilitado o hay un modo de voz activo.
- Tenga el archivo WAV listo en su computadora.

## Pasos

1. Ubique la fila de la ranura donde desea cargar el archivo (F1 a F8).
2. Haga clic derecho en cualquier lugar del marco de la fila de esa ranura.
3. En el menú contextual que aparece, seleccione la opción de carga.
4. En el cuadro de diálogo de archivos que se abre, navegue hasta su archivo WAV y selecciónelo.
5. Confirme la selección. La etiqueta de duración de la ranura se actualizará de "Empty" a la duración del archivo cuando se complete la transferencia.

## Funcionamiento de cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; clic derecho abre el menú contextual para renombrar o cargar WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre asignado a la ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación, o "Empty" si la ranura no tiene contenido. | Empty |
| Barras de progreso de ranura | Muestran el progreso de reproducción o grabación en vivo. Ocultas cuando la ranura está inactiva. | — |
| ● REC | Inicia la grabación en la ranura seleccionada. | — |
| ■ STOP | Detiene la grabación o reproducción. | — |
| ▶ PLAY | Reproduce la ranura seleccionada. | — |
| ◀ PREV | Previsualiza la ranura a través del altavoz local. | — |
| Edición de nombre | Cambio de nombre en línea de una ranura activado mediante el menú contextual. | — |

## Atajos de teclado

El panel DVK registra los siguientes atajos de teclado, que solo están activos mientras el panel está visible. Esto evita conflictos con otros paneles que también usan F1–F12 (por ejemplo, el panel CWX).

| Tecla | Acción |
|---|---|
| F1 … F12 | Selecciona y reproduce la ranura correspondiente (F1 selecciona la ranura 1, F2 la ranura 2, etc.). La ranura debe contener una grabación. |
| Escape | Cancela una operación de cambio de nombre activa. Si no hay un cambio de nombre en curso, detiene cualquier grabación o reproducción de DVK. |

## Consejos

- Después de que finalice la carga, verifique que la etiqueta de duración de la ranura ya no muestre "Empty" antes de transmitir.
- Puede renombrar la ranura inmediatamente después de cargar haciendo clic derecho en la fila nuevamente y seleccionando la opción de cambio de nombre. Consulte [Renombrar una ranura](rename-a-slot.md).
- Use los atajos de teclado (F1–F8) para seleccionar y reproducir rápidamente mensajes almacenados al aire. La tecla Escape proporciona una forma conveniente de detener la operación.

## Solución de problemas

- **La duración de la ranura aún muestra "Empty" después de seleccionar un archivo** — La transferencia a la radio pudo haber fallado. Verifique que la conexión con la radio siga activa y luego intente la carga nuevamente.
- **El menú contextual no aparece** — Haga clic en otro lugar primero para desseleccionar cualquier control activo, luego haga clic derecho directamente en el marco de la fila de la ranura.
- **Los atajos de teclado (F1–F8, Escape) no funcionan** — Asegúrese de que el panel DVK esté visible. Los atajos están deshabilitados cuando el panel está oculto para evitar conflictos con otros paneles.

## Relacionados

- [Descripción general del teclado de voz digital](overview.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Reproducir una ranura del teclado de voz almacenada](play-a-stored-voice-keyer-slot.md)
- [Renombrar una ranura](rename-a-slot.md)
