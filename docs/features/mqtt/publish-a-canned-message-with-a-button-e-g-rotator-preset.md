# Publicar un mensaje predefinido con un botón (ej. preajuste de rotador)

Esta página muestra cómo añadir un botón de publicación al applet MQTT y usarlo para enviar un mensaje fijo a su broker — por ejemplo, enviar un comando de preajuste de rotador con un solo clic.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón MQTT de la barra lateral derecha para mostrarlo.
- Debe tener configurada una conexión con el broker. Consulte [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- El applet debe estar conectado (Enable muestra "On" y la etiqueta de estado indica "Connected") para que los botones de publicación puedan funcionar.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón MQTT de la barra lateral derecha.
2. Si aún no está conectado, haga clic en Settings... para abrir el diálogo de configuración MQTT (MQTT Settings). Configure los detalles de conexión al broker (Host, Port, User, Password), los temas de suscripción y los botones de publicación. Haga clic en OK para guardar.
3. Haga clic en Enable para establecerlo en "On". Espere a que la etiqueta de estado indique "Connected".
4. Haga clic en cualquier botón de publicación para enviar su payload configurado al tema configurado de forma inmediata. El botón solo está activo mientras esté conectado.

## Función de cada control

| Control          | Tipo                                                                                                                                                              | Valor predeterminado                                                                                                                |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Settings...      | Abre el diálogo MQTT Settings (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.                           | Nuevo en v26.5.3. Reemplaza los campos inline de Host/Port/User/Pass/TLS/Topics.                                                    |
| Botones de publicación | Al hacer clic, publica el payload configurado en el tema configurado mediante MqttClient::publish. Los botones se configuran en el diálogo MQTT Settings.          | Solo activo mientras está conectado. Configurado en la pestaña Publish Buttons del MqttSettingsDialog.                               |
| Registro de mensajes | Muestra los mensajes recibidos como líneas 'tema: valor'. También procesa las actualizaciones de alias de antena desde MQTT.                                       | Limitado a 50 entradas.                                                                                                             |
| Enable (Off/On)  | Conecta o desconecta del broker usando la configuración de MqttSettings. Emite connectRequested / disconnectRequested y guarda el estado de conexión habilitada. | La contraseña se carga desde el llavero del sistema al activar por primera vez. Si la contraseña del llavero aún no está cargada, muestra el estado 'Waiting for keychain'. |

## Indicadores

| Indicador       | Estados                                     | Significado                                                                                        |
|-----------------|----------------------------------------------|----------------------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, <mensaje de error> | Estado de la conexión con colores: verde cuando está conectado, gris cuando está desconectado, color predeterminado en caso de error. |

## Notas

- El applet MQTT ahora usa el gestor de temas de la aplicación para su apariencia visual. El texto de los botones, las etiquetas y el registro de mensajes siguen automáticamente los colores del tema actual en lugar de usar colores fijos.
- La contraseña se almacena en el llavero del sistema y se carga automáticamente cuando activa la conexión por primera vez. Si la contraseña del llavero aún no está cargada, el estado muestra "Waiting for keychain".
- La configuración de conexión al broker (host, puerto, credenciales, TLS y suscripciones) se realiza en el diálogo MQTT Settings (Settings > MQTT...) en lugar de en línea en el applet.
- Las definiciones de los botones de publicación se almacenan como JSON en `MqttButtons` y persisten entre reinicios.
- Al pasar el ratón sobre un botón en modo normal, se muestra un tooltip con el tema y payload configurados para que pueda confirmar lo que se enviará antes de hacer clic.
- A partir de v26.6.3, el registro de mensajes muestra tanto los mensajes recibidos como los publicados enviados. Los mensajes enviados aparecen con un prefijo "TX" (ej., "TX rotator/preset: 45") para distinguirlos de los mensajes entrantes.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que Enable muestre "On" y la etiqueta de estado indique "Connected". Si muestra un error, verifique la configuración del broker y haga clic en Enable para reconectar.
- **El botón desaparece después de reiniciar** — La configuración se guarda al confirmar el diálogo MQTT Settings. Si AetherSDR se cerró forzosamente, es posible que la clave `MqttButtons` no se haya escrito. Vuelva a configurar el botón.
- **El estado muestra "Waiting for keychain"** — El llavero del sistema aún no ha proporcionado la contraseña almacenada. Generalmente se resuelve automáticamente después de unos segundos. Si persiste, verifique la configuración del llavero del sistema.

## Relacionados

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Añadir o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas de rotador/antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Visión general de MQTT](overview.md)
