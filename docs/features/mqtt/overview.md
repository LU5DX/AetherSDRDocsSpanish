# Resumen de MQTT

El applet MQTT conecta AetherSDR a un broker MQTT de la estación para que pueda suscribirse a tópicos, ver los mensajes entrantes en un registro en vivo, superponer valores de tópicos en el panadapter y publicar mensajes predefinidos con botones definidos por el usuario. No se requiere conexión de radio.

## Antes de comenzar

- Debe poder acceder a un broker MQTT en su red (por ejemplo, Mosquitto ejecutándose en `localhost`).
- Si el applet MQTT no está visible, actívelo haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha. El applet está oculto de forma predeterminada.
- Si el botón de la bandeja MQTT no aparece, es posible que su compilación de AetherSDR no incluya soporte MQTT (se requiere la puerta de compilación `HAVE_MQTT`).

## Cómo funciona

Al hacer clic en Enable (cambiándolo de Off a On), el applet carga la contraseña MQTT del llavero del sistema, guarda toda la configuración del broker y abre una conexión con el broker. Se suscribe a cada tópico configurado en el cuadro de diálogo MQTT Settings. Los mensajes entrantes aparecen en el registro de mensajes como líneas `tópico: valor`; el registro conserva las últimas 50 líneas. Los tópicos con el prefijo `*` en la lista de suscripción además envían su último valor al panadapter como superposición. Los botones de publicación le permiten enviar una carga útil fija a un tópico fijo con un solo clic mientras está conectado.

Al hacer clic nuevamente en Enable (cambiándolo de On a Off), se desconecta inmediatamente y se eliminan las superposiciones del panadapter.

La configuración se guarda en el disco solo cuando Enable pasa de Off a On.

## Qué hace cada control

| Control        | Valor predeterminado                                                                                                                         | Rango válido                                                                   |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| Enable         | Off                                                                                                                                           | Off / On                                                                       |
| Settings...    | Abre el cuadro de diálogo MQTT Settings (MqttSettingsDialog) para configurar la conexión al broker, las suscripciones y los botones de publicación. | Nuevo en v26.5.3. Reemplaza los campos Host/Puerto/Usuario/Contraseña/TLS/Tópicos en línea. |
| Botones de publicación | Al hacer clic, publica la carga útil configurada en el tópico configurado a través de MqttClient::publish. Los botones se configuran en el cuadro de diálogo MQTT Settings. | Solo activos mientras está conectado. Se configuran mediante la pestaña Publish Buttons de MqttSettingsDialog. |
| Registro de mensajes | Muestra los mensajes recibidos como líneas 'tópico: valor'. También procesa actualizaciones de alias de antena desde MQTT.                                              | Limitado a 50 entradas.                                                        |

## Indicador de estado

La etiqueta de estado junto a Enable muestra el estado actual de la conexión:

- **Connected** — se muestra en verde cuando la conexión con el broker está establecida.
- **Disconnected** — se muestra en gris cuando no está conectado.
- **\<mensaje de error\>** — se muestra en el color predeterminado cuando ocurre un error de conexión; el texto describe el error.

## Consejos

- Los tópicos se comparan exactamente. Si un tópico tiene una ruta profunda como `rotator/az/pos`, el registro de mensajes muestra solo el último segmento de la ruta (`pos`) como etiqueta, pero la ruta completa se utiliza para la coincidencia de superposición del panadapter.
- No necesita una conexión de radio para usar MQTT. El applet funciona independientemente del estado de la conexión FlexRadio.
- Los botones de publicación están inactivos (los clics no tienen efecto) mientras esté desconectado. Conéctese primero, luego use los botones.
- La contraseña MQTT se almacena en el llavero del sistema. Al habilitarlo por primera vez, el applet muestra "Waiting for keychain" hasta que se cargue la contraseña.
- Toda la configuración de conexión del broker (host, puerto, credenciales, TLS, suscripciones) se configura exclusivamente a través del cuadro de diálogo MQTT Settings (Settings > MQTT...).

## Relacionados

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Subscribe to rotator / antenna switch topics](subscribe-to-rotator-antenna-switch-topics.md)
- [Overlay an MQTT value on the panadapter (prefix topic with *)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Add or remove custom publish buttons](add-or-remove-custom-publish-buttons.md)
- [Enable TLS with a custom CA certificate](enable-tls-with-a-custom-ca-certificate.md)
