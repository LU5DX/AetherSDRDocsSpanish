# Publicar un mensaje predefinido con un botón (p. ej., ajuste preestablecido del rotor)

Esta página muestra cómo agregar un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker, por ejemplo, enviar un comando preestablecido del rotor con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- Debe tener configurada una conexión a un broker. Consulte [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado dice "Connected") para que los botones de publicación funcionen.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha.
2. Si aún no está conectado, haga clic en Settings... para abrir el diálogo de configuración MQTT. Configure los detalles de conexión al broker (Host, Port, User, Password), temas de suscripción y botones de publicación. Haga clic en OK para guardar.
3. Haga clic en Enable para establecerlo en "On". Espere a que la etiqueta de estado indique "Connected".
4. Haga clic en cualquier botón de publicación para enviar inmediatamente su carga útil configurada a su tema configurado. El botón solo está activo mientras está conectado.

## Función de cada control

| Control          | Tipo                                                                                                                                           | Valor predeterminado                                                                |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Settings...      | Abre el diálogo de configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. | Nuevo en v26.5.3. Reemplaza los campos inline de Host/Port/User/Pass/TLS/Topics.    |
| Botones de publicación | Al hacer clic, publica la carga útil configurada en el tema configurado a través de MqttClient::publish. Los botones se configuran en el diálogo de configuración MQTT. | Solo activos mientras está conectado. Se configuran en la pestaña Publish Buttons de MqttSettingsDialog. |
| Registro de mensajes | Muestra los mensajes recibidos como líneas "tema: valor". También procesa actualizaciones de alias de antena provenientes de MQTT.             | Limitado a 50 entradas.                                                             |
| Enable (Off/On)  | Botón de alternancia para conectar o desconectar del broker usando la configuración de MqttSettingsDialog.                                    | Off. La contraseña se carga desde el llavero del sistema al habilitarlo por primera vez. |

## Indicadores

| Indicador      | Estados                                    | Significado                                                                                  |
|----------------|--------------------------------------------|----------------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, <mensaje de error>| Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, color predeterminado en caso de error. |

## Consejos

- La contraseña se almacena en el llavero del sistema y se carga automáticamente cuando habilita la conexión por primera vez. Si la contraseña del llavero aún no se ha cargado, el estado muestra "Waiting for keychain".
- La configuración de conexión al broker (host, puerto, credenciales, TLS y suscripciones) se configura en el diálogo de configuración MQTT (Settings > MQTT...), no directamente en el applet.
- Las definiciones de los botones de publicación se almacenan como JSON bajo `MqttButtons` y persisten entre reinicios.
- Al pasar el cursor sobre un botón en modo normal, se muestra una información sobre herramientas con el tema y la carga útil configurados, para que pueda confirmar lo que se enviará antes de hacer clic.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que Enable muestre "On" y que la etiqueta de estado indique "Connected". Si muestra un error, verifique la configuración de su broker y haga clic en Enable para reconectar.
- **El botón desaparece después de reiniciar** — La configuración se guarda al confirmar el diálogo de configuración MQTT. Si AetherSDR se cerró forzadamente, es posible que la clave `MqttButtons` no se haya escrito. Vuelva a configurar el botón.
- **El estado muestra "Waiting for keychain"** — El llavero del sistema aún no ha proporcionado la contraseña almacenada. Esto suele resolverse automáticamente después de unos segundos. Si persiste, verifique la configuración de su llavero del sistema.

## Relacionado

- [Conectarse a un broker MQTT de la estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Agregar o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas de rotor / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
