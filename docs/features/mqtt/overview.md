# Descripción general de MQTT

El applet de MQTT conecta AetherSDR a un broker MQTT de estación para que pueda suscribirse a topics, ver los mensajes entrantes en un registro en tiempo real, superponer valores de topics en el panadapter y publicar mensajes predefinidos mediante botones configurados por el usuario. No se requiere conexión de radio.

## Antes de comenzar

- Un broker MQTT debe ser accesible en su red (por ejemplo, Mosquitto ejecutándose en `localhost`).
- Si el applet de MQTT no es visible, actívelo haciendo clic en el botón de bandeja MQTT de la barra lateral derecha. El applet está oculto por defecto.
- Si el botón de bandeja MQTT no aparece, es posible que su compilación de AetherSDR no incluya soporte para MQTT (se requiere la opción de compilación `HAVE_MQTT`).

## Cómo funciona

Al hacer clic en Enable (cambiando el estado de Off a On), el applet guarda todos los ajustes del broker y abre una conexión con él. Se suscribe a todos los topics indicados en el campo Topics. Los mensajes entrantes aparecen en el registro de mensajes como líneas `topic: value`; el registro conserva las últimas 50 líneas. Los topics con el prefijo `*` en el campo Topics también envían su último valor al panadapter como superposición. Los botones de publicación permiten enviar un payload fijo a un topic fijo con un solo clic mientras se está conectado.

Al hacer clic en Enable nuevamente (cambiando el estado de On a Off), la conexión se interrumpe de inmediato y se eliminan las superposiciones del panadapter.

Los ajustes se guardan en disco únicamente cuando Enable pasa de Off a On.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Host | `localhost` | Cualquier nombre de host o IP | `MqttHost` | Nombre de host o dirección IP del broker. |
| Port | `1883` | 1–65535 | `MqttPort` | Puerto TCP del broker. Cambia automáticamente entre `1883` y `8883` al activar o desactivar TLS. |
| User | _(vacío)_ | Cualquier cadena | `MqttUser` | Nombre de usuario del broker. Opcional. |
| Pass | _(vacío)_ | Cualquier cadena | `MqttPass` | Contraseña del broker. Opcional. Se muestra enmascarada. |
| Topics | _(vacío)_ | Lista separada por comas | `MqttTopics` | Topics a los que suscribirse. Agregue el prefijo `*` a un topic para superponer también su valor en el panadapter. Ejemplo: `*rotator/pos, *ant/selected, station/log`. |
| TLS | Off | On / Off | `MqttTls` | Activa el cifrado TLS. Al activarlo o desactivarlo, se muestra u oculta la fila del certificado CA y el Port cambia automáticamente entre `1883` y `8883`. |
| CA cert | _(vacío)_ | Ruta de archivo | `MqttCaFile` | Ruta a un archivo de certificado CA. Déjelo en blanco para usar el paquete CA del sistema. La fila solo es visible cuando TLS está activado. |
| Enable | Off | Off / On | _(no se persiste)_ | Conecta (Off → On) o desconecta (On → Off). El guardado de todos los ajustes en disco ocurre al conectarse. |
| Publish buttons | _(ninguno)_ | Hasta 12 botones | `MqttButtons` | Cada botón publica un payload configurado en un topic configurado. Solo está activo mientras está conectado. Se almacena como JSON. |
| Edit / Done | Edit | Edit / Done | _(no se persiste)_ | Entra en el modo de edición de botones. En este modo, hacer clic en un botón abre su diálogo de edición, hacer clic derecho sobre un botón lo elimina y un mosaico `+` permite agregar un nuevo botón (hasta 12). Haga clic en Done para salir del modo de edición. |
| Message log | _(vacío)_ | Últimas 50 líneas | _(no se persiste)_ | Muestra los mensajes recibidos como líneas `topic: value`. Solo lectura. |

## Indicador de estado

La etiqueta de estado junto a Enable muestra el estado actual de la conexión:

- **Connected** — se muestra en verde cuando la conexión con el broker está establecida.
- **Disconnected** — se muestra en gris cuando no hay conexión.
- **\<error message\>** — se muestra con el color predeterminado cuando ocurre un error de conexión; el texto describe el error.

## Consejos

- Los topics se comparan de forma exacta. Si un topic tiene una ruta profunda como `rotator/az/pos`, el registro de mensajes muestra solo el último segmento de la ruta (`pos`) como etiqueta, pero la ruta completa se utiliza para la coincidencia de superposiciones en el panadapter.
- No se necesita conexión de radio para usar MQTT. El applet opera de forma independiente del estado de conexión con el FlexRadio.
- Los botones de publicación están inactivos (los clics no tienen efecto) mientras no hay conexión. Conéctese primero y luego use los botones.

## Relacionado

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a topics de rotator / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Superponer un valor MQTT en el panadapter (agregar prefijo * al topic)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publicar un mensaje predefinido con un botón (p. ej., posición preestablecida del rotator)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Agregar o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Activar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
