# Subir un archivo WAV a una ranura

Cargue un archivo WAV pregrabado desde su computadora en una de las ranuras del Digital Voice Keyer para reproducirlo al aire sin necesidad de grabarlo en vivo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK solo está disponible cuando hay una conexión activa con la radio.
- El panel DVK debe estar visible en la ventana principal. Aparece cuando DVK está habilitado o hay un modo de voz activo.
- Tenga el archivo WAV listo en su computadora.

## Pasos

1. Localice la fila de la ranura donde desea cargar el archivo (F1 a F8).
2. Haga clic derecho en cualquier lugar del marco de la fila de esa ranura.
3. En el menú contextual que aparece, seleccione la opción de subida.
4. En el diálogo de archivo que se abre, navegue hasta su archivo WAV y selecciónelo.
5. Confirme la selección. La etiqueta de duración de la ranura se actualizará de "Empty" a la duración del archivo cuando la transferencia finalice.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; haga clic derecho para abrir el menú contextual para renombrar o subir WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre asignado a la ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación, o "Empty" si la ranura no tiene contenido. | Empty |
| Barras de progreso de ranura | Muestra el progreso de reproducción o grabación en vivo. Ocultas cuando la ranura está inactiva. | — |

## Consejos

- Después de que finalice la subida, verifique que la etiqueta de duración de la ranura ya no muestre "Empty" antes de transmitir.
- Puede renombrar la ranura inmediatamente después de subir el archivo haciendo clic derecho nuevamente en la fila y seleccionando la opción de renombrar. Consulte [Renombrar una ranura](rename-a-slot.md).

## Solución de problemas

- **La etiqueta de duración de la ranura sigue mostrando "Empty" después de seleccionar un archivo** — Es posible que la transferencia a la radio haya fallado. Verifique que la conexión con la radio siga activa y luego intente la subida nuevamente.
- **El menú contextual no aparece** — Haga clic en otro lugar primero para deseleccionar cualquier control activo, luego haga clic derecho directamente en el marco de la fila de la ranura.

## Relacionado

- [Visión general del Digital Voice Keyer](overview.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Reproducir una ranura almacenada del voice keyer](play-a-stored-voice-keyer-slot.md)
- [Renombrar una ranura](rename-a-slot.md)
