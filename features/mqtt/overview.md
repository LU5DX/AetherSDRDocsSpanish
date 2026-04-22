# Descripción general de MQTT

El applet de MQTT conecta AetherSDR a un bróker MQTT de la estación para que pueda suscribirse a tópicos, ver los mensajes entrantes en un registro en tiempo real, superponer valores de tópicos sobre el panadapter y publicar mensajes predefinidos mediante botones configurados por el usuario. No se requiere conexión de radio.

## Antes de comenzar

- Debe haber un bróker MQTT accesible en su red (por ejemplo, Mosquitto ejecutándose en `localhost`).
- Si el applet de MQTT no es visible, actívelo haciendo clic en el botón MQTT del panel lateral derecho. El applet está oculto de forma predeterminada.
- Si el botón MQTT del panel lateral no aparece, es posible que su versión de AetherSDR no incluya soporte para MQTT (se requiere la opción de compilación `HAVE_MQTT`).

## Cómo funciona

Cuando hace clic en Enable (cambiando de Off a On), el applet guarda todos los ajustes del bróker y abre una conexión con él. Se suscribe a todos los tópicos indicados en el campo Topics. Los mensajes entrantes aparecen en el registro de mensajes como líneas `topic: value`; el registro conserva las últimas 50 líneas. Los tópicos precedidos por `*` en el campo Topics también envían su último valor al panadapter como superposición. Los botones de publicación permiten enviar una carga útil fija a un tópico fijo con un solo clic mientras se está conectado.

Hacer clic en Enable nuevamente (cambiando de On a Off) desconecta de inmediato y elimina las superposiciones del panadapter.

Los ajustes se guardan en disco únicamente cuando Enable pasa de Off a On.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Host | `localhost` | Cualquier nombre de host o IP | `MqttHost` | Nombre de host o dirección IP del bróker. |
| Port | `1883` | 1–65535 | `MqttPort` | Puerto TCP del bróker. Cambia automáticamente entre `1883` y `8883` al activar o desactivar TLS. |
| User | _(vacío)_ | Cualquier cadena | `MqttUser` | Nombre de usuario del bróker. Opcional. |
| Pass | _(vacío)_ | Cualquier cadena | `MqttPass` | Contraseña del bróker. Opcional. Se muestra enmascarada. |
| Topics | _(vacío)_ | Lista separada por comas | `MqttTopics` | Tópicos a los que suscribirse. Anteponga `*` a un tópico para superponer también su valor en el panadapter. Ejemplo: `*rotator/pos, *ant/selected, station/log`. |
| TLS | Off | On / Off | `MqttTls` | Habilita el cifrado TLS. Al activarlo o desactivarlo, se muestra u oculta la fila del certificado CA y se cambia automáticamente el puerto entre `1883` y `8883`. |
| CA cert | _(vacío)_ | Ruta de archivo | `MqttCaFile` | Ruta al archivo de certificado CA. Déjelo en blanco para usar el paquete de CA del sistema. La fila solo es visible cuando TLS está activado. |
| Enable | Off | Off / On | _(no se persiste)_ | Conecta (Off → On) o desconecta (On → Off). El guardado de todos los ajustes en disco ocurre al conectar. |
| Publish buttons | _(ninguno)_ | Hasta 12 botones | `MqttButtons` | Cada botón publica una carga útil configurada en un tópico configurado. Solo activos mientras se está conectado. Se almacenan como JSON. |
| Edit / Done | Edit | Edit / Done | _(no se persiste)_ | Entra en el modo de edición de botones. En este modo, hacer clic en un botón abre su diálogo de edición, hacer clic derecho sobre un botón lo elimina, y una ficha `+` añade un nuevo botón (hasta 12). Haga clic en Done para salir del modo de edición. |
| Message log | _(vacío)_ | Últimas 50 líneas | _(no se persiste)_ | Muestra los mensajes recibidos como líneas `topic: value`. Solo lectura. |

## Indicador de estado

La etiqueta de estado junto a Enable muestra el estado actual de la conexión:

- **Connected** — se muestra en verde cuando la conexión con el bróker está establecida.
- **Disconnected** — se muestra en gris cuando no hay conexión.
- **\<error message\>** — se muestra en el color predeterminado cuando ocurre un error de conexión; el texto describe el error.

## Consejos

- Los tópicos se comparan de forma exacta. Si un tópico tiene una ruta profunda como `rotator/az/pos`, el registro de mensajes muestra solo el último segmento de la ruta (`pos`) como etiqueta, pero la ruta completa se utiliza para la coincidencia en la superposición del panadapter.
- No se necesita conexión de radio para usar MQTT. El applet opera de forma independiente al estado de la conexión con FlexRadio.
- Los botones de publicación están inactivos (los clics no tienen efecto) mientras se está desconectado. Conéctese primero y luego use los botones.

## Relacionado

- [Conectarse a un bróker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a tópicos de rotador o conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Superponer un valor MQTT en el panadapter (prefije el tópico con *)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publicar un mensaje predefinido con un botón (p. ej., posición preestablecida del rotador)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Agregar o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Habilitar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
