# Resumen de MQTT

El applet de MQTT conecta AetherSDR con un broker MQTT de la estación para que pueda suscribirse a temas, ver los mensajes entrantes en un registro en vivo, superponer valores de temas en el panadapter y publicar mensajes predefinidos con botones personalizados. No se requiere conexión de radio.

## Antes de comenzar

- Un broker MQTT debe ser accesible en su red (por ejemplo, Mosquitto ejecutándose en `localhost`).
- Si el applet de MQTT no es visible, actívelo haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha. El applet está oculto por defecto.
- Si el botón de la bandeja MQTT no aparece, es posible que su compilación de AetherSDR no incluya soporte MQTT (se requiere la compuerta de compilación `HAVE_MQTT`).

## Cómo funciona

Al hacer clic en Enable (cambiándolo de Off a On), el applet guarda toda la configuración del broker y abre una conexión con el broker. Se suscribe a cada tema listado en el campo Topics. Los mensajes entrantes aparecen en el registro de mensajes como líneas `topic: value`; el registro conserva las últimas 50 líneas. Los temas con el prefijo `*` en el campo Topics además envían su último valor al panadapter como superposición. Los botones de publicación permiten enviar una carga útil fija a un tema fijo con un solo clic mientras está conectado.

Al hacer clic nuevamente en Enable (cambiándolo de On a Off), se desconecta inmediatamente y se eliminan todas las superposiciones del panadapter.

La configuración se guarda en el disco solo cuando Enable pasa de Off a On.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Host | `localhost` | Cualquier nombre de host o IP | `MqttHost` | Nombre de host o dirección IP del broker. |
| Port | `1883` | 1–65535 | `MqttPort` | Puerto TCP del broker. Cambia automáticamente entre `1883` y `8883` cuando se activa TLS. |
| User | _(vacío)_ | Cualquier cadena | `MqttUser` | Nombre de usuario del broker. Opcional. |
| Pass | _(vacío)_ | Cualquier cadena | `MqttPass` | Contraseña del broker. Opcional. Se muestra oculta. |
| Topics | _(vacío)_ | Lista separada por comas | `MqttTopics` | Temas a los que suscribirse. Anteponga `*` a un tema para también superponer su valor en el panadapter. Ejemplo: `*rotator/pos, *ant/selected, station/log`. |
| TLS | Off | On / Off | `MqttTls` | Activa el cifrado TLS. Al alternarlo, se muestra u oculta la fila del certificado CA y se cambia automáticamente el puerto entre `1883` y `8883`. |
| CA cert | _(vacío)_ | Ruta de archivo | `MqttCaFile` | Ruta a un archivo de certificado CA. Déjelo en blanco para usar el conjunto de CA del sistema. La fila solo es visible cuando TLS está marcado. |
| Enable | Off | Off / On | _(no persistida)_ | Conecta (Off → On) o desconecta (On → Off). Todas las configuraciones se guardan en el disco al conectar. |
| Publish buttons | _(ninguno)_ | Hasta 12 botones | `MqttButtons` | Cada botón publica una carga útil configurada en un tema configurado. Solo activo mientras está conectado. Se almacena como JSON. |
| Edit / Done | Edit | Edit / Done | _(no persistida)_ | Activa el modo de edición de botones. En modo de edición, al hacer clic en un botón se abre su diálogo de edición, al hacer clic derecho en un botón se elimina y un mosaico `+` agrega un nuevo botón (hasta 12). Haga clic en Done para salir del modo de edición. |
| Message log | _(vacío)_ | Últimas 50 líneas | _(no persistida)_ | Muestra los mensajes recibidos como líneas `topic: value`. Solo lectura. |

## Indicador de estado

La etiqueta de estado junto a Enable muestra el estado actual de la conexión:

- **Connected** — se muestra en verde cuando la conexión con el broker está establecida.
- **Disconnected** — se muestra en gris cuando no está conectado.
- **\<mensaje de error\>** — se muestra en el color predeterminado cuando ocurre un error de conexión; el texto describe el error.

## Consejos

- Los temas se comparan exactamente. Si un tema tiene una ruta profunda como `rotator/az/pos`, el registro de mensajes muestra solo el último segmento de la ruta (`pos`) como etiqueta, pero la ruta completa se usa para la coincidencia de superposición en el panadapter.
- No necesita una conexión de radio para usar MQTT. El applet opera independientemente del estado de la conexión FlexRadio.
- Los botones de publicación están inactivos (los clics no tienen efecto) mientras está desconectado. Conéctese primero, luego use los botones.

## Relacionados

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Subscribe to rotator / antenna switch topics](subscribe-to-rotator-antenna-switch-topics.md)
- [Overlay an MQTT value on the panadapter (prefix topic with *)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Add or remove custom publish buttons](add-or-remove-custom-publish-buttons.md)
- [Enable TLS with a custom CA certificate](enable-tls-with-a-custom-ca-certificate.md)
