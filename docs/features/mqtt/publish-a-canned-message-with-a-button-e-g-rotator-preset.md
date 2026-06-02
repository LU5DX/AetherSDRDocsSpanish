# Publicar un mensaje predefinido con un botón (ej. preajuste de rotor)

Esta página muestra cómo agregar un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker — por ejemplo, enviar un comando de preajuste de rotor con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- Debe tener configurada una conexión al broker. Consulte [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado dice "Connected") para que los botones de publicación funcionen.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha.
2. Si aún no está conectado, haga clic en Settings... para abrir el diálogo de Configuración MQTT. Configure los detalles de conexión al broker (Host, Port, User, Password), temas de suscripción y botones de publicación. Haga clic en OK para guardar.
3. Haga clic en Enable para establecerlo en "On". Espere hasta que la etiqueta de estado muestre "Connected".
4. Haga clic en cualquier botón de publicación para enviar inmediatamente su carga útil configurada al tema configurado. El botón solo está activo mientras está conectado.

## Qué hace cada control

| Control         | Tipo                                                                                                                                                          | Valor predeterminado                                                                                                                  |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| Settings...     | Abre el diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.                 | Nuevo en v26.5.3. Reemplaza los campos inline de Host/Port/User/Pass/TLS/Topics.                                                      |
| Botones de publicación | Haga clic para publicar la carga útil configurada en el tema configurado mediante MqttClient::publish. Los botones se configuran en el diálogo de Configuración MQTT. | Solo activo mientras está conectado. Configurados mediante la pestaña Publish Buttons del MqttSettingsDialog.                          |
| Registro de mensajes | Muestra los mensajes recibidos como líneas 'tema: valor'. También procesa actualizaciones de alias de antena desde MQTT.                                       | Limitado a 50 entradas.                                                                                                                |
| Enable (Off/On) | Conecta o desconecta del broker usando la configuración de MqttSettings. Emite connectRequested/disconnectRequested y guarda el estado habilitado de la conexión. | La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'. |

## Indicadores

| Indicador    | Estados                                    | Significado                                                                                       |
|--------------|-------------------------------------------|---------------------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, <mensaje de error> | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, color predeterminado en caso de error. |

## Notas

- El applet MQTT ahora utiliza el gestor de temas de la aplicación para su apariencia visual. El texto de los botones, las etiquetas y el registro de mensajes siguen automáticamente los colores del tema actual en lugar de usar colores fijos.
- La contraseña se almacena en el llavero del sistema y se carga automáticamente cuando habilita la conexión por primera vez. Si la contraseña del llavero aún no se ha cargado, el estado muestra "Waiting for keychain".
- La configuración de conexión al broker (host, puerto, credenciales, TLS y suscripciones) se configura en el diálogo de Configuración MQTT (Settings > MQTT...) en lugar de inline en el applet.
- Las definiciones de botones publicados se almacenan como JSON bajo la clave `MqttButtons` y persisten entre reinicios.
- Al pasar el cursor sobre un botón en modo normal, se muestra un tooltip con el tema y la carga útil configurados, para que pueda confirmar lo que se enviará antes de hacer clic.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que Enable muestre "On" y la etiqueta de estado muestre "Connected". Si muestra un error, verifique la configuración de su broker y haga clic en Enable para reconectar.
- **El botón falta después de reiniciar** — La configuración se guarda cuando confirma el diálogo de Configuración MQTT. Si AetherSDR se cerró forzosamente, es posible que la clave `MqttButtons` no se haya escrito. Vuelva a configurar el botón.
- **El estado muestra "Waiting for keychain"** — El llavero del sistema aún no ha proporcionado la contraseña almacenada. Esto generalmente se resuelve automáticamente después de unos segundos. Si persiste, verifique la configuración de su llavero del sistema.

## Relacionado

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Agregar o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas de rotor / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
