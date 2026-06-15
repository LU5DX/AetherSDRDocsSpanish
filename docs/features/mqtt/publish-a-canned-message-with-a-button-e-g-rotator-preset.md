# Publicar un mensaje predefinido con un botón (ej. preajuste de rotador)

Esta página muestra cómo agregar un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker — por ejemplo, enviar un comando de preajuste de rotador con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- Debe tener configurada una conexión a un broker. Consulte [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado dice "Connected") para que los botones de publicación se activen.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha.
2. Si aún no está conectado, haga clic en Settings... para abrir el diálogo MQTT Settings. Configure los detalles de conexión al broker (Host, Port, User, Password), los temas de suscripción y los botones de publicación. Haga clic en OK para guardar.
3. Haga clic en Enable para establecerlo en "On". Espere a que la etiqueta de estado muestre "Connected".
4. Haga clic en cualquier botón de publicación para enviar su carga útil configurada a su tema configurado de inmediato. El botón solo está activo mientras está conectado.

## Función de cada control

| Control         | Tipo                                                                                                                                                       | Predeterminado                                                                                                                         |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| Settings...     | Abre el diálogo MQTT Settings (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.                    | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Port/User/Pass/TLS/Topics.                                                      |
| Botones de publicación | Al hacer clic, publica la carga útil configurada en el tema configurado mediante MqttClient::publish. Los botones se configuran en el diálogo MQTT Settings. | Solo activos mientras está conectado. Configurados mediante la pestaña Publish Buttons de MqttSettingsDialog.                           |
| Registro de mensajes | Muestra los mensajes recibidos y enviados. Los mensajes entrantes se muestran como 'tema: valor'. Los mensajes salientes publicados se muestran con el prefijo 'TX'. Límite de 50 entradas. | Límite de 50 entradas. Nuevo en v26.6.3: muestra los mensajes enviados como 'TX tema: carga útil'.                                      |
| Enable (Off/On) | Conecta o desconecta del broker usando la configuración de MqttSettings. Emite connectRequested / disconnectRequested y guarda el estado habilitado de conexión. | La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no está cargada, muestra el estado 'Waiting for keychain'. |

## Indicadores

| Indicador    | Estados                                    | Significado                                                                                   |
|--------------|--------------------------------------------|-----------------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, <mensaje de error> | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, color predeterminado en caso de error. |

## Notas

- El applet MQTT ahora usa el gestor de temas de la aplicación para su apariencia visual. El texto de los botones, las etiquetas y el registro de mensajes siguen automáticamente los colores del tema actual en lugar de usar colores fijos.
- La contraseña se almacena en el llavero del sistema y se carga automáticamente cuando habilita la conexión por primera vez. Si la contraseña del llavero aún no está cargada, el estado muestra "Waiting for keychain".
- Los ajustes de conexión al broker (host, puerto, credenciales, TLS y suscripciones) se configuran en el diálogo MQTT Settings (Settings > MQTT...) en lugar de hacerlo directamente en el applet.
- Las definiciones de los botones de publicación se almacenan como JSON bajo la clave `MqttButtons` y persisten entre reinicios.
- Al pasar el cursor sobre un botón en modo normal, se muestra una información sobre herramientas con el tema y la carga útil configurados, para que pueda confirmar lo que se enviará antes de hacer clic.
- A partir de v26.6.3, el registro de mensajes muestra tanto los mensajes recibidos como los enviados publicados. Los mensajes enviados aparecen con el prefijo "TX" (ej., "TX rotator/preset: 45") para distinguirlos de los mensajes entrantes.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que Enable muestre "On" y la etiqueta de estado muestre "Connected". Si muestra un error, verifique la configuración de su broker y haga clic en Enable para reconectar.
- **El botón falta después de un reinicio** — La configuración se guarda cuando confirma el diálogo MQTT Settings. Si AetherSDR se cerró forzosamente, es posible que la clave `MqttButtons` no se haya escrito. Reconfigure el botón.
- **El estado muestra "Waiting for keychain"** — El llavero del sistema aún no ha proporcionado la contraseña almacenada. Esto suele resolverse automáticamente después de unos segundos. Si persiste, verifique la configuración de su llavero del sistema.

## Relacionados

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Agregar o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas de rotador / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
