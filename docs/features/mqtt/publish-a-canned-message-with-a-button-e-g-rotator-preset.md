# Publicar un mensaje predefinido con un botón (p. ej., ajuste de rotor)

Esta página muestra cómo añadir un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker, por ejemplo, enviar un comando de ajuste de rotor con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de bandeja MQTT en la barra lateral derecha para mostrarlo.
- Debe tener configurada una conexión con un broker. Consulte [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado dice "Connected") antes de que los botones de publicación se activen.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de bandeja MQTT en la barra lateral derecha.
2. Si aún no está conectado, haga clic en Settings... para abrir el diálogo de Ajustes MQTT. Configure los detalles de conexión del broker (Host, Port, User, Password), los temas de suscripción y los botones de publicación. Haga clic en OK para guardar.
3. Haga clic en Enable para configurarlo en "On". Espere a que la etiqueta de estado muestre "Connected".
4. Haga clic en cualquier botón de publicación para enviar su carga útil configurada al tema configurado de inmediato. El botón solo está activo mientras esté conectado.

## Función de cada control

| Control        | Tipo                                                                                                                                                      | Valor predeterminado                                                                                                                          |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| Settings...    | Abre el diálogo de Ajustes MQTT (MqttSettingsDialog) para la conexión al broker, las suscripciones y la configuración de los botones de publicación.       | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Port/User/Pass/TLS/Topics.                                                             |
| Botones de publicación | Haga clic para publicar la carga útil configurada en el tema configurado mediante MqttClient::publish. Los botones se configuran en el diálogo de Ajustes MQTT. | Solo activos mientras esté conectado. Configurados mediante la pestaña Publish Buttons de MqttSettingsDialog.                                 |
| Registro de mensajes | Muestra los mensajes recibidos como líneas 'tema: valor'. También procesa las actualizaciones de alias de antena desde MQTT.                              | Limitado a 50 entradas.                                                                                                                        |
| Enable (Off/On) | Conecta o desconecta del broker usando los ajustes de MqttSettings. Emite connectRequested / disconnectRequested y guarda el estado habilitado de la conexión. | La contraseña se carga desde el llavero del sistema al primer Enable. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'. |

## Indicadores

| Indicador    | Estados                                    | Significado                                                                                       |
|--------------|--------------------------------------------|---------------------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, <mensaje de error> | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, predeterminado en caso de error. |

## Notas

- El applet MQTT ahora utiliza el gestor de temas de la aplicación para su apariencia visual. El texto de los botones, las etiquetas y el registro de mensajes siguen automáticamente los colores del tema actual en lugar de usar colores fijos.
- La contraseña se almacena en el llavero del sistema y se carga automáticamente cuando habilita la conexión por primera vez. Si la contraseña del llavero aún no se ha cargado, el estado muestra "Waiting for keychain".
- Los ajustes de conexión al broker (host, puerto, credenciales, TLS y suscripciones) se configuran en el diálogo de Ajustes MQTT (Settings > MQTT...) en lugar de hacerlo directamente en el applet.
- Las definiciones de los botones de publicación se guardan como JSON bajo `MqttButtons` y persisten al reiniciar.
- Al pasar el cursor sobre un botón en modo normal, se muestra una información sobre herramientas con el tema y la carga útil configurados, de modo que pueda confirmar lo que se enviará antes de hacer clic.
- A partir de v26.6.3, el registro de mensajes muestra tanto los mensajes recibidos como los publicados enviados. Los mensajes enviados aparecen con el prefijo "TX" (p. ej., "TX rotator/preset: 45") para distinguirlos de los mensajes entrantes.
- Si el llavero del sistema no está disponible, la contraseña MQTT se mantiene solo durante la sesión actual de AetherSDR. No se escribe en los ajustes de la aplicación en texto plano; si cierra y reinicia AetherSDR, deberá volver a introducir la contraseña.

## Solución de problemas

- **Al hacer clic en un botón de publicación no ocurre nada** — El applet no está conectado. Compruebe que Enable muestre "On" y que la etiqueta de estado muestre "Connected". Si muestra un error, verifique los ajustes del broker y haga clic en Enable para reconectarse.
- **El botón falta después de reiniciar** — Los ajustes se guardan al confirmar el diálogo de Ajustes MQTT. Si AetherSDR se cerró forzosamente, es posible que la clave `MqttButtons` no se haya escrito. Vuelva a configurar el botón.
- **El estado muestra "Waiting for keychain"** — El llavero del sistema aún no ha proporcionado la contraseña almacenada. Esto suele resolverse automáticamente después de unos segundos. Si persiste, verifique la configuración del llavero de su sistema.
- **La contraseña no se recuerda tras reiniciar (sin llavero)** — En sistemas sin soporte de llavero, la contraseña MQTT se mantiene solo durante la sesión actual. Vuelva a introducir la contraseña cada vez que inicie AetherSDR.

## Relacionado

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Añadir o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas de rotor / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
