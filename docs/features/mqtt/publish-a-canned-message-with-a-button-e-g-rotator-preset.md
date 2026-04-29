# Publicar un mensaje predefinido con un botón (p. ej., preset de rotador)

Esta página muestra cómo agregar un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker — por ejemplo, enviar un comando de preset de rotador con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de bandeja MQTT en la barra lateral derecha para mostrarlo.
- Debe tener una conexión a un broker configurada. Consulte [Conectarse al broker MQTT de una estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado indica "Connected") antes de que los botones de publicación funcionen.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de bandeja MQTT en la barra lateral derecha.
2. Si aún no está conectado, complete Host, Port, User, Pass y Topics, luego haga clic en Enable para establecerlo en "On". Espere a que la etiqueta de estado indique "Connected".
3. Haga clic en Edit. El botón cambia a "Done" y comienza el modo de edición. Los botones de publicación existentes cambian de apariencia para indicar que son editables.
4. Haga clic en el mosaico `+` que aparece en la cuadrícula de botones. Se abre un diálogo de edición.
5. En el diálogo, ingrese la etiqueta del botón (el texto que aparecerá en el botón), el tema al que publicar y el payload a enviar. Confirme el diálogo.
6. El nuevo botón aparece en la cuadrícula. Repita los pasos 4–5 para agregar más botones (hasta 12 en total).
7. Haga clic en Done para salir del modo de edición. Los botones recuperan su apariencia normal.
8. Haga clic en cualquier botón de publicación para enviar su payload configurado al tema configurado de inmediato. El botón solo está activo mientras esté conectado.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Botones de publicación | Botón de pulsación | — | Hasta 12 botones | `MqttButtons` | Cada clic publica el payload configurado en el tema configurado. Solo activo mientras esté conectado. |
| Edit / Done | Botón de alternancia | Edit | — | — | Entra o sale del modo de edición de botones. En el modo de edición, hacer clic en un botón abre su diálogo de edición; hacer clic derecho en un botón muestra la opción Remove; el mosaico `+` agrega un nuevo botón. |

## Consejos

- Para editar un botón existente, haga clic en Edit y luego haga clic en el botón que desea cambiar. El diálogo de edición se abre con la etiqueta, el tema y el payload actuales prellenados.
- Para eliminar un botón, haga clic en Edit, luego haga clic derecho en el botón y elija "Remove".
- Las definiciones de botones se almacenan como JSON bajo `MqttButtons` y persisten entre reinicios.
- Al pasar el cursor sobre un botón en modo normal, se muestra un tooltip con el tema y el payload configurados, para que pueda confirmar qué se enviará antes de hacer clic.

## Solución de problemas

- **Hacer clic en un botón de publicación no hace nada** — El applet no está conectado. Verifique que Enable indique "On" y que la etiqueta de estado indique "Connected". Si muestra un error, compruebe la configuración de su broker y haga clic en Enable para reconectarse.
- **El mosaico `+` no aparece** — Ha alcanzado el límite de 12 botones. Elimine un botón existente para hacer espacio.
- **El botón falta después de reiniciar** — La configuración se guarda al confirmar el diálogo de edición. Si AetherSDR fue cerrado forzosamente, es posible que la clave `MqttButtons` no haya sido escrita. Vuelva a agregar el botón.

## Relacionado

- [Conectarse al broker MQTT de una estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Agregar o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas de rotador / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
