# Publicar un mensaje predefinido con un botón (por ejemplo, posición preestablecida de rotador)

Esta página muestra cómo añadir un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker — por ejemplo, enviando un comando de posición preestablecida de rotador con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón MQTT del panel lateral derecho para mostrarlo.
- Debe tener una conexión a un broker configurada. Consulte [Conectar a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado indica "Connected") antes de que los botones de publicación funcionen.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón MQTT del panel lateral derecho.
2. Si aún no está conectado, complete Host, Port, User, Pass y Topics; luego haga clic en Enable para establecerlo en "On". Espere a que la etiqueta de estado indique "Connected".
3. Haga clic en Edit. El botón cambia a "Done" y comienza el modo de edición. Los botones de publicación existentes cambian de apariencia para indicar que son editables.
4. Haga clic en el mosaico `+` que aparece en la cuadrícula de botones. Se abre un diálogo de edición.
5. En el diálogo, introduzca la etiqueta del botón (el texto que aparecerá en el botón), el topic al que publicar y el payload que se enviará. Confirme el diálogo.
6. El nuevo botón aparece en la cuadrícula. Repita los pasos 4–5 para añadir más botones (hasta 12 en total).
7. Haga clic en Done para salir del modo de edición. Los botones vuelven a su apariencia normal.
8. Haga clic en cualquier botón de publicación para enviar inmediatamente su payload configurado al topic configurado. El botón solo está activo mientras haya conexión.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Botones de publicación | Botón momentáneo | — | Hasta 12 botones | `MqttButtons` | Cada clic publica el payload configurado en el topic configurado. Solo activo mientras haya conexión. |
| Edit / Done | Botón alternado | Edit | — | — | Entra o sale del modo de edición de botones. En el modo de edición, hacer clic en un botón abre su diálogo de edición; hacer clic derecho muestra la opción "Remove"; el mosaico `+` añade un nuevo botón. |

## Consejos

- Para editar un botón existente, haga clic en Edit y luego en el botón que desea cambiar. El diálogo de edición se abre con la etiqueta, el topic y el payload actuales precargados.
- Para eliminar un botón, haga clic en Edit, luego haga clic derecho sobre el botón y elija "Remove".
- Las definiciones de los botones se almacenan como JSON bajo `MqttButtons` y persisten entre reinicios.
- Al pasar el cursor sobre un botón en modo normal se muestra un tooltip con el topic y el payload configurados, de modo que puede confirmar lo que se enviará antes de hacer clic.

## Solución de problemas

- **Hacer clic en un botón de publicación no hace nada** — El applet no está conectado. Verifique que Enable indique "On" y que la etiqueta de estado indique "Connected". Si muestra un error, compruebe la configuración de su broker y haga clic en Enable para reconectarse.
- **El mosaico `+` no aparece** — Ha alcanzado el límite de 12 botones. Elimine un botón existente para liberar espacio.
- **Un botón no aparece tras reiniciar** — La configuración se guarda al confirmar el diálogo de edición. Si AetherSDR se cerró forzosamente, es posible que la clave `MqttButtons` no se haya escrito. Vuelva a añadir el botón.

## Relacionado

- [Conectar a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Añadir o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a topics de rotador / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
