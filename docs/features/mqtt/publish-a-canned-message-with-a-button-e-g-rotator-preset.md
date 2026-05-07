# Publicar un mensaje predefinido con un botón (ej. ajuste predefinido del rotador)

Esta página explica cómo agregar un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker, por ejemplo, enviar un comando predefinido del rotador con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- Debe tener una conexión a un broker configurada. Consulte [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado indica "Connected") antes de que los botones de publicación puedan funcionar.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha.
2. Si aún no está conectado, complete los campos Host, Port, User, Pass y Topics, luego haga clic en Enable para ajustarlo a "On". Espere a que la etiqueta de estado indique "Connected".
3. Haga clic en Edit. El botón cambia a "Done" y comienza el modo de edición. Los botones de publicación existentes cambian de apariencia para indicar que son editables.
4. Haga clic en el mosaico `+` que aparece en la cuadrícula de botones. Se abre un cuadro de diálogo de edición.
5. En el cuadro de diálogo, ingrese la etiqueta del botón (el texto que aparecerá en el botón), el tema al que publicar y la carga útil a enviar. Confirme el cuadro de diálogo.
6. El nuevo botón aparece en la cuadrícula. Repita los pasos 4 y 5 para agregar más botones (hasta 12 en total).
7. Haga clic en Done para salir del modo de edición. Los botones vuelven a su apariencia normal.
8. Haga clic en cualquier botón de publicación para enviar inmediatamente su carga útil configurada al tema configurado. El botón solo está activo mientras esté conectado.

## Función de cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|---|
| Publish buttons | Botón pulsador | — | Hasta 12 botones | `MqttButtons` | Cada clic publica la carga útil configurada en el tema configurado. Solo activo mientras está conectado. |
| Edit / Done | Botón de alternancia | Edit | — | — | Entra o sale del modo de edición de botones. En modo de edición, al hacer clic en un botón se abre su cuadro de diálogo de edición; al hacer clic derecho en un botón se muestra una opción Remove; el mosaico `+` agrega un nuevo botón. |

## Consejos

- Para editar un botón existente, haga clic en Edit y luego haga clic en el botón que desea cambiar. Se abre el cuadro de diálogo de edición con la etiqueta, el tema y la carga útil actuales ya completados.
- Para eliminar un botón, haga clic en Edit, luego haga clic derecho en el botón y elija "Remove".
- Las definiciones de los botones se almacenan como JSON bajo `MqttButtons` y persisten tras reinicios.
- Al pasar el cursor sobre un botón en modo normal, se muestra un tooltip con el tema y la carga útil configurados, para que pueda confirmar lo que se enviará antes de hacer clic.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que Enable muestre "On" y que la etiqueta de estado indique "Connected". Si muestra un error, verifique la configuración de su broker y haga clic en Enable para reconectarse.
- **El mosaico `+` no aparece** — Ha alcanzado el límite de 12 botones. Elimine un botón existente para hacer espacio.
- **El botón falta después de reiniciar** — La configuración se guarda al confirmar el cuadro de diálogo de edición. Si AetherSDR se cerró forzosamente, es posible que la clave `MqttButtons` no se haya escrito. Vuelva a agregar el botón.

## Relacionado

- [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Agregar o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas del rotador/interruptor de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
