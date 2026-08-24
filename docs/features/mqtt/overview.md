# Descripción general de MQTT

El applet MQTT conecta AetherSDR con un broker MQTT de la estación para que pueda suscribirse a temas, ver los mensajes entrantes y salientes en un registro en vivo, superponer valores de temas en el panadapter y publicar mensajes predefinidos con botones definidos por el usuario. No se requiere conexión de radio.

## Antes de comenzar

- Debe tener un broker MQTT accesible en su red (por ejemplo, Mosquitto ejecutándose en `localhost`).
- Si el applet MQTT no está visible, habilítelo haciendo clic en el botón de bandeja MQTT en la barra lateral derecha. El applet está oculto por defecto.
- Si el botón de bandeja MQTT no está presente, su compilación de AetherSDR puede no incluir soporte MQTT (se requiere la compuerta de compilación `HAVE_MQTT`).

## Cómo funciona

Cuando hace clic en Enable (cambiándolo de Off a On), el applet carga la contraseña MQTT desde el llavero del sistema, guarda toda la configuración del broker y abre una conexión con el broker. Se suscribe a todos los temas configurados en el diálogo MQTT Settings. Los mensajes entrantes aparecen en el registro de mensajes como líneas `topic: value`; los mensajes publicados salientes aparecen como líneas `TX topic: value`. El registro conserva las últimas 50 líneas. Los temas con prefijo `*` en la lista de suscripciones además envían su último valor al panadapter como superposición. Los botones de publicación le permiten enviar un payload fijo a un tema fijo con un solo clic mientras está conectado.

Al hacer clic nuevamente en Enable (cambiándolo de On a Off), se desconecta inmediatamente y se eliminan las superposiciones del panadapter.

La configuración solo se guarda en disco cuando Enable pasa de Off a On.

## Qué hace cada control

| Control         | Predeterminado                                                                                                                                | Rango válido                                                                         |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Enable          | Off                                                                                                                                           | Off / On                                                                             |
| Settings...     | Abre el diálogo MQTT Settings (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.        | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Port/User/Pass/TLS/Topics.    |
| Publish buttons | Un clic publica el payload configurado en el tema configurado mediante `MqttClient::publish`. Los botones se configuran en el diálogo MQTT Settings. | Solo activos mientras está conectado. Se configuran en la pestaña Publish Buttons de MqttSettingsDialog. |
| Message log     | Muestra los mensajes recibidos como líneas `topic: value`. También procesa actualizaciones de alias de antena desde MQTT.                     | Limitado a 50 entradas.                                                               |

## Indicador de estado

La etiqueta de estado junto a Enable muestra el estado actual de la conexión:

- **Connected** — se muestra en verde cuando la conexión con el broker está establecida.
- **Disconnected** — se muestra en gris cuando no está conectado.
- **\<mensaje de error\>** — se muestra en el color predeterminado cuando ocurre un error de conexión; el texto describe el error.

## Consejos

- Los temas se comparan exactamente. Si un tema tiene una ruta profunda como `rotator/az/pos`, el registro de mensajes solo muestra el último segmento de la ruta (`pos`) como etiqueta, pero se usa la ruta completa para la comparación de superposición en el panadapter.
- No necesita una conexión de radio para usar MQTT. El applet opera independientemente del estado de conexión FlexRadio.
- Los botones de publicación están inactivos (los clics no tienen efecto) mientras está desconectado. Conéctese primero y luego use los botones.
- La contraseña MQTT se almacena en el llavero del sistema. Al habilitar por primera vez, el applet muestra "Waiting for keychain" hasta que se cargue la contraseña.
- Toda la configuración de conexión al broker (host, puerto, credenciales, TLS, suscripciones) se configura exclusivamente a través del diálogo MQTT Settings (Settings > MQTT...).
- El applet MQTT ahora usa colores conscientes del tema para todos los controles y etiquetas, adaptándose correctamente a los temas claros y oscuros.
- El registro de mensajes ahora muestra tanto mensajes entrantes como salientes. Los mensajes salientes aparecen con un prefijo `TX` (por ejemplo, `TX rotator/az/set: 180`) para distinguirlos de los mensajes entrantes.
- Si importa una configuración que contiene una contraseña MQTT, la contraseña se desvía al llavero del sistema durante la importación. En sistemas sin soporte de llavero, la contraseña se mantiene en una bóveda de sesión y se usa solo para la sesión actual para evitar dejarla en configuración de texto plano.

## Relacionado

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Subscribe to rotator / antenna switch topics](subscribe-to-rotator-antenna-switch-topics.md)
- [Overlay an MQTT value on the panadapter (prefix topic with *)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Add or remove custom publish buttons](add-or-remove-custom-publish-buttons.md)
- [Enable TLS with a custom CA certificate](enable-tls-with-a-custom-ca-certificate.md)
