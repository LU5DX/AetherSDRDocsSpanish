# Superponer un valor de MQTT en el panadapter

Muestre el último valor de un tema MQTT suscrito directamente en el panadapter, para que pueda monitorear la telemetría de la estación (p. ej., temperatura de la antena, posición del rotor, datos meteorológicos) mientras opera.

## Antes de empezar

- Conéctese a un broker MQTT de la estación y suscríbase al tema cuyo valor desea superponer. Consulte [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- La suscripción al tema debe tener habilitada la opción **Display on panadapter** en el diálogo MQTT Settings (`Settings > MQTT...`). Consulte [Suscribirse a temas MQTT y alternar la visualización en el panadapter](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md).

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de la bandeja **MQTT** en la barra lateral derecha.
2. Haga clic en el botón de alternancia **Off/On** para conectarse al broker. El botón muestra "On" y la etiqueta de estado se vuelve verde cuando está conectado.
3. Asegúrese de que el tema suscrito aparezca en el registro de mensajes. Una línea como `antennaTemp: 28.4` confirma que los datos están llegando.
4. La superposición del panadapter se actualiza automáticamente a medida que llegan los mensajes. Solo se superponen los temas que tienen marcada la opción **Display on panadapter** en su configuración de suscripción.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---------|---------------|------------------------|
| Alternancia **Off/On** | Conecta o desconecta del broker. Guarda el estado de la conexión. | — |
| Botón **Settings...** | Abre el diálogo MQTT Settings para la configuración del broker, suscripciones y botones de publicación. | — |
| Registro de mensajes | Muestra los últimos 50 mensajes recibidos como `tema: valor`. Habilita la superposición del panadapter para los temas con visualización habilitada. | — |
| Botones de publicación | Hasta 12 botones configurados en MQTT Settings. Cada uno publica su carga útil configurada en su tema configurado. | `MqttButtons` |

## Consejos

- Solo se superpone el **último valor** de cada tema con visualización habilitada. La superposición muestra el nombre corto del tema (último segmento) y el valor.
- Para borrar la superposición, desconecte el cliente MQTT (alterne **Off/On** a "Off").

## Solución de problemas

- **No aparece nada en el panadapter** — Verifique que la suscripción al tema tenga habilitada la opción **Display on panadapter** en `Settings > MQTT... > Subscriptions`. Compruebe que el registro de mensajes muestre el tema recibiendo valores.
- **Estado "Waiting for keychain"** — La contraseña de MQTT está almacenada en el llavero de su sistema. Si no se ha cargado, la conexión se difiere. Introduzca la contraseña en la solicitud del llavero, o configure la conexión del broker sin contraseña.

## Relacionados

- [Suscribirse a temas MQTT y alternar la visualización en el panadapter](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
