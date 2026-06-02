# Descripción general de MQTT

El applet MQTT conecta AetherSDR a un broker MQTT de la estación para que pueda suscribirse a temas, ver mensajes entrantes en un registro en vivo, superponer valores de temas en el panadapter y publicar mensajes predefinidos con botones personalizados. No se requiere conexión de radio.

## Antes de comenzar

- Un broker MQTT debe ser accesible en su red (por ejemplo, Mosquitto ejecutándose en `localhost`).
- Si el applet MQTT no está visible, actívelo haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha. El applet está oculto por defecto.
- Si el botón de la bandeja MQTT está ausente, es posible que su compilación de AetherSDR no incluya soporte MQTT (se requiere la puerta de compilación `HAVE_MQTT`).

## Cómo funciona

Al hacer clic en Enable (cambiándolo de Off a On), el applet carga la contraseña MQTT desde el llavero del sistema, guarda toda la configuración del broker y abre una conexión con el broker. Se suscribe a cada tema configurado en el cuadro de diálogo MQTT Settings. Los mensajes entrantes aparecen en el registro de mensajes como líneas `tema: valor`; el registro conserva las últimas 50 líneas. Los temas con el prefijo `*` en la lista de suscripciones además envían su último valor al panadapter como superposición. Los botones de publicación le permiten enviar una carga útil fija a un tema fijo con un solo clic mientras está conectado.

Al hacer clic nuevamente en Enable (cambiándolo de On a Off), se desconecta inmediatamente y se eliminan las superposiciones del panadapter.

La configuración se guarda en disco solo cuando Enable pasa de Off a On.

## Función de cada control

| Control         | Predeterminado                                                                                                                             | Rango válido                                                                         |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Enable          | Off                                                                                                                                        | Off / On                                                                             |
| Settings...     | Abre el cuadro de diálogo MQTT Settings (MqttSettingsDialog) para la configuración de conexión al broker, suscripciones y botones de publicación.                 | Nuevo en v26.5.3. Reemplaza los campos Host/Puerto/Usuario/Contraseña/TLS/Temas.     |
| Botones de publicación | Al hacer clic, publica la carga útil configurada en el tema configurado a través de MqttClient::publish. Los botones se configuran en el cuadro de diálogo MQTT Settings. | Solo activos mientras está conectado. Configurados mediante la pestaña Publish Buttons de MqttSettingsDialog. |
| Registro de mensajes | Muestra los mensajes recibidos como líneas 'tema: valor'. También procesa las actualizaciones de alias de antena desde MQTT.                | Limitado a 50 entradas.                                                              |

## Indicador de estado

La etiqueta de estado junto a Enable muestra el estado actual de la conexión:

- **Connected** — se muestra en verde cuando la conexión con el broker está establecida.
- **Disconnected** — se muestra en gris cuando no está conectado.
- **\<mensaje de error\>** — se muestra en el color predeterminado cuando ocurre un error de conexión; el texto describe el error.

## Consejos

- Los temas se comparan exactamente. Si un tema tiene una ruta profunda como `rotator/az/pos`, el registro de mensajes muestra solo el último segmento de la ruta (`pos`) como etiqueta, pero la ruta completa se usa para la coincidencia de superposición en el panadapter.
- No necesita una conexión de radio para usar MQTT. El applet opera independientemente del estado de la conexión FlexRadio.
- Los botones de publicación están inactivos (los clics no tienen efecto) mientras esté desconectado. Conéctese primero, luego use los botones.
- La contraseña MQTT se almacena en el llavero del sistema. Al activarlo por primera vez, el applet muestra "Waiting for keychain" hasta que se cargue la contraseña.
- Todos los ajustes de conexión al broker (host, puerto, credenciales, TLS, suscripciones) se configuran exclusivamente a través del cuadro de diálogo MQTT Settings (Settings > MQTT...).
- El applet MQTT ahora usa colores adaptables al tema para todos los controles y etiquetas, adaptándose correctamente a los temas claro y oscuro.

## Relacionado

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Subscribe to rotator / antenna switch topics](subscribe-to-rotator-antenna-switch-topics.md)
- [Overlay an MQTT value on the panadapter (prefix topic with *)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Add or remove custom publish buttons](add-or-remove-custom-publish-buttons.md)
- [Enable TLS with a custom CA certificate](enable-tls-with-a-custom-ca-certificate.md)
