# Cargar un archivo WAV en un slot

Cargue un archivo WAV pregrabado desde su computadora en uno de los slots del Digital Voice Keyer para reproducirlo en el aire sin necesidad de grabar en vivo.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El panel DVK solo está disponible cuando hay una conexión de radio activa.
- El panel DVK debe estar visible en la ventana principal. Aparece cuando el DVK está habilitado o hay un modo de voz activo.
- Tenga el archivo WAV listo en su computadora.

## Pasos

1. Localice la fila del slot en el que desea cargar el archivo (F1 a F8).
2. Haga clic derecho en cualquier parte del marco de esa fila.
3. En el menú contextual que aparece, seleccione la opción de carga.
4. En el cuadro de diálogo de archivo que se abre, navegue hasta su archivo WAV y selecciónelo.
5. Confirme la selección. La etiqueta de duración del slot cambia de "Empty" a la duración del archivo cuando la transferencia se completa.

## Qué hace cada control

| Control | Comportamiento | Valor predeterminado |
|---|---|---|
| Botones de slot F1 … F8 | Selecciona y reproduce ese slot; haga clic derecho para abrir el menú contextual y cambiar el nombre o cargar un WAV. | — |
| Etiquetas de nombre de slot | Muestra el nombre asignado al slot. | `Recording <n>` |
| Etiquetas de duración de slot | Muestra la duración de la grabación, o "Empty" si el slot no tiene contenido. | Empty |
| Barras de progreso de slot | Muestra el progreso en tiempo real de la reproducción o grabación. Se oculta cuando el slot está inactivo. | — |

## Consejos

- Una vez finalizada la carga, verifique que la etiqueta de duración del slot ya no muestre "Empty" antes de transmitir.
- Puede cambiar el nombre del slot inmediatamente después de la carga haciendo clic derecho en la fila nuevamente y seleccionando la opción de cambio de nombre. Consulte [Cambiar el nombre de un slot](rename-a-slot.md).

## Solución de problemas

- **La duración del slot sigue mostrando "Empty" después de seleccionar un archivo** — Es posible que la transferencia al radio haya fallado. Verifique que la conexión de radio siga activa y vuelva a intentar la carga.
- **El menú contextual no aparece** — Haga clic en otro lugar primero para deseleccionar cualquier control activo, luego haga clic derecho directamente sobre el marco de la fila del slot.

## Relacionados

- [Descripción general del Digital Voice Keyer](overview.md)
- [Grabar un nuevo slot de DVK](record-a-new-dvk-slot.md)
- [Reproducir un slot de voice keyer almacenado](play-a-stored-voice-keyer-slot.md)
- [Cambiar el nombre de un slot](rename-a-slot.md)
