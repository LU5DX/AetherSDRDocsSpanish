# Superponer un valor MQTT en el panadapter

Muestre el último valor de un tema MQTT suscrito directamente en el panadapter, para poder supervisar la telemetría de la estación (por ejemplo, temperatura de la antena, posición del rotor, datos meteorológicos) mientras opera.

## Antes de comenzar

- Conéctese a un broker MQTT de la estación y suscríbase al tema cuyo valor desea superponer. Consulte [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- La suscripción al tema debe tener habilitada la opción **Display on panadapter** en el cuadro de diálogo MQTT Settings (`Settings > MQTT...`). Consulte [Suscribirse a temas MQTT y alternar la visualización en panadapter](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md).

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de bandeja **MQTT** en la barra lateral derecha.
2. Haga clic en el botón de alternancia **Enable (Off/On)** para conectarse al broker. El botón muestra "On" y la etiqueta de estado se vuelve verde cuando está conectado.
3. Asegúrese de que el tema suscrito aparezca en el registro de mensajes. Una línea como `antennaTemp: 28.4` confirma que los datos están llegando.
4. La superposición del panadapter se actualiza automáticamente a medida que llegan los mensajes. Solo se superponen los temas que tienen marcada la opción **Display on panadapter** en su configuración de suscripción.

## Función de cada control

| Control                    | Comportamiento                                                                                                                                                                                                                                                                                                       | Clave de configuración |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
| Alternancia **Enable (Off/On)** | Conecta o desconecta del broker usando la configuración de MqttSettings. Emite connectRequested/disconnectRequested y guarda el estado de conexión habilitada. La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'. | —                      |
| Botón **Settings...**     | Abre el cuadro de diálogo MQTT Settings (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. Nuevo en v26.5.3. Reemplaza los campos Host/Port/User/Pass/TLS/Topics integrados.                                                                                   | —                      |
| Registro de mensajes       | Muestra los mensajes recibidos como líneas `topic: value`. También muestra los mensajes transmitidos como líneas `TX topic: payload`. Procesa las actualizaciones de alias de antena desde MQTT.                                                                                                                      | Limitado a 50 entradas. |
| Botones de publicación     | Al hacer clic, publica el payload configurado en el tema configurado a través de MqttClient::publish. Los botones se configuran en el cuadro de diálogo MQTT Settings. Solo están activos mientras está conectado. Se configuran a través de la pestaña Publish Buttons de MqttSettingsDialog.                     | `MqttButtons`          |

## Indicador de estado

| Indicador    | Estados                                      | Significado                                                               |
|--------------|----------------------------------------------|---------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, `<mensaje de error>` | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, predeterminado en caso de error. |

## Consejos

- Solo se superpone el **último valor** de cada tema habilitado para visualización. La superposición muestra el nombre corto del tema (último segmento) y el valor.
- Para borrar la superposición, desconecte el cliente MQTT (alterne **Enable (Off/On)** a "Off").
- Los mensajes transmitidos aparecen en el registro de mensajes con un prefijo `TX`, mostrando el nombre corto del tema y los primeros 80 caracteres del payload. Esto ayuda a confirmar que los botones de publicación funcionan correctamente.
- El registro de mensajes tiene un límite de 50 entradas. Las entradas más antiguas se eliminan automáticamente cuando se alcanza el límite.

## Solución de problemas

- **No aparece nada en el panadapter** — Verifique que la suscripción al tema tenga habilitada la opción **Display on panadapter** en `Settings > MQTT... > Subscriptions`. Compruebe que el registro de mensajes muestre que el tema está recibiendo valores.
- **Estado "Waiting for keychain"** — La contraseña MQTT está almacenada en el llavero del sistema. Si no se ha cargado, la conexión se pospone. Ingrese la contraseña en la solicitud del llavero, o configure la conexión al broker sin contraseña.

## Relacionados

- [Suscribirse a temas MQTT y alternar la visualización en panadapter](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
