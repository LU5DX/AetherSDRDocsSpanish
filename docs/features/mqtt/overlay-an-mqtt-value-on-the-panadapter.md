# Superponer un valor MQTT en el panadapter

Muestre el último valor de un tema MQTT suscrito directamente en el panadapter, para que pueda monitorear la telemetría de la estación (p. ej., temperatura de la antena, posición del rotor, datos meteorológicos) mientras opera.

## Antes de comenzar

- Conéctese a un broker MQTT de la estación y suscríbase al tema cuyo valor desea superponer. Consulte [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- La suscripción al tema debe tener habilitada la opción **Display on panadapter** en el diálogo de Configuración MQTT (`Settings > MQTT...`). Consulte [Suscribirse a temas MQTT y alternar la visualización en el panadapter](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md).

## Pasos

1. Abra la applet MQTT haciendo clic en el botón de bandeja **MQTT** en la barra lateral derecha.
2. Haga clic en el botón de alternancia **Enable (Off/On)** para conectarse al broker. El botón mostrará "On" y la etiqueta de estado se volverá verde cuando esté conectado.
3. Asegúrese de que el tema suscrito aparezca en el registro de mensajes. Una línea como `antennaTemp: 28.4` confirma que los datos están llegando.
4. La superposición del panadapter se actualiza automáticamente a medida que llegan los mensajes. Solo se superponen los temas que tienen marcada la opción **Display on panadapter** en su configuración de suscripción.

## Qué hace cada control

| Control                      | Comportamiento                                                                                                                                                                                                                                                                                                                                                                      | Clave de configuración                                                            |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| Alternancia **Enable (Off/On)** | Conecta o desconecta del broker usando la configuración de MqttSettings. Emite connectRequested/disconnectRequested y guarda el estado de conexión habilitada. La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'.                                           | —                                                                                 |
| Botón **Settings...**          | Abre el diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. Nuevo en v26.5.3. Reemplaza los campos integrados Host/Puerto/Usuario/Contraseña/TLS/Temas.                                                                                                                                          | —                                                                                 |
| Registro de mensajes          | Muestra los mensajes recibidos como líneas 'tema: valor'. También procesa actualizaciones de alias de antena desde MQTT.                                                                                                                                                                                                                                                            | Limitado a 50 entradas.                                                           |
| Botones de publicación        | Al hacer clic, publica la carga útil configurada en el tema configurado a través de MqttClient::publish. Los botones se configuran en el diálogo de Configuración MQTT.                                                                                                                                                                                                              | Solo activo mientras está conectado. Configurado en la pestaña Publish Buttons de MqttSettingsDialog. |
| **Settings...**               | Abre el diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.                                                                                                                                                                                                                                    | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Puerto/Usuario/Contraseña/TLS/Temas. |

## Indicador de estado

| Indicador       | Estados                                       | Significado                                                                |
|-----------------|-----------------------------------------------|----------------------------------------------------------------------------|
| Etiqueta de estado | Desconectado, Conectado, `<mensaje de error>` | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, color por defecto en caso de error. |

## Consejos

- Solo se superpone el **último valor** de cada tema habilitado para visualización. La superposición muestra el nombre corto del tema (último segmento) y el valor.
- Para limpiar la superposición, desconecte el cliente MQTT (alterne **Enable (Off/On)** a "Off").
- Los mensajes transmitidos aparecen en el registro de mensajes con un prefijo `TX`, mostrando el nombre corto del tema y los primeros 80 caracteres de la carga útil. Esto ayuda a confirmar que los botones de publicación funcionan correctamente.
- El registro de mensajes está limitado a 50 entradas. Las entradas más antiguas se eliminan automáticamente cuando se alcanza el límite.

## Solución de problemas

- **No aparece nada en el panadapter** — Verifique que la suscripción al tema tenga habilitada la opción **Display on panadapter** en `Settings > MQTT... > Subscriptions`. Compruebe que el registro de mensajes muestre que el tema está recibiendo valores.
- **Estado "Waiting for keychain"** — La contraseña MQTT está almacenada en el llavero de su sistema. Si no se ha cargado, la conexión se pospone. Ingrese la contraseña en el mensaje del llavero, o configure la conexión al broker sin contraseña.

## Relacionados

- [Suscribirse a temas MQTT y alternar la visualización en el panadapter](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
