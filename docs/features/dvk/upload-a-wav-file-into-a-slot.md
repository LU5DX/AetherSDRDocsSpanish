# Cargar un archivo WAV en una ranura

Cargue un archivo WAV pregrabado desde su computadora en una de las ranuras del Digital Voice Keyer para reproducirlo en el aire sin necesidad de grabar en vivo.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El panel DVK solo está disponible cuando hay una conexión de radio activa.
- El panel DVK debe estar visible en la ventana principal. Aparece cuando el DVK está habilitado o hay un modo de voz activo.
- Tenga el archivo WAV listo en su computadora.

## Pasos

1. Localice la fila de la ranura en la que desea cargar el archivo (F1 a F8).
2. Haga clic derecho en cualquier parte del marco de esa fila.
3. En el menú contextual que aparece, seleccione la opción de carga.
4. En el cuadro de diálogo de archivo que se abre, navegue hasta su archivo WAV y selecciónelo.
5. Confirme la selección. La etiqueta de duración de la ranura se actualiza de "Empty" a la duración del archivo cuando la transferencia finaliza.

## Qué hace cada control

| Control | Comportamiento | Predeterminado |
|---|---|---|
| Botones de ranura F1 … F8 | Selecciona y reproduce esa ranura; haga clic derecho para abrir el menú contextual y cambiar el nombre o cargar un WAV. | — |
| Etiquetas de nombre de ranura | Muestra el nombre asignado a la ranura. | `Recording <n>` |
| Etiquetas de duración de ranura | Muestra la duración de la grabación, o "Empty" si la ranura no tiene contenido. | Empty |
| Barras de progreso de ranura | Muestra el progreso de reproducción o grabación en tiempo real. Se ocultan cuando la ranura está inactiva. | — |

## Consejos

- Una vez finalizada la carga, verifique que la etiqueta de duración de la ranura ya no muestre "Empty" antes de transmitir.
- Puede cambiar el nombre de la ranura inmediatamente después de cargar el archivo haciendo clic derecho nuevamente en la fila y seleccionando la opción de cambio de nombre. Consulte [Cambiar el nombre de una ranura](rename-a-slot.md).

## Solución de problemas

- **La duración de la ranura sigue mostrando "Empty" después de seleccionar un archivo** — Es posible que la transferencia a la radio haya fallado. Verifique que la conexión de radio siga activa y vuelva a intentar la carga.
- **El menú contextual no aparece** — Haga clic en otro lugar primero para deseleccionar cualquier control activo y luego haga clic derecho directamente sobre el marco de la fila de la ranura.

## Relacionado

- [Descripción general del Digital Voice Keyer](overview.md)
- [Grabar una nueva ranura DVK](record-a-new-dvk-slot.md)
- [Reproducir una ranura del voice keyer almacenada](play-a-stored-voice-keyer-slot.md)
- [Cambiar el nombre de una ranura](rename-a-slot.md)
