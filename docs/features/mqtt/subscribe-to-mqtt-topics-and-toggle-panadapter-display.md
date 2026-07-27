# Suscribirse a temas MQTT y activar la visualización en el panadapter

Agregue suscripciones a temas MQTT y controle si el último valor de cada tema se muestra como superposición en el panadapter. Esto le permite monitorear la telemetría de la estación (como la posición del rotor de antena, datos meteorológicos o el estado del amplificador) directamente en la pantalla del espectro.

## Antes de comenzar

- Debe tener un broker MQTT en funcionamiento accesible desde su equipo con AetherSDR.
- El applet MQTT debe estar visible (active el botón de la bandeja MQTT en la barra lateral derecha si está oculto).

## Pasos

1. Abra el cuadro de diálogo de Configuración MQTT: vaya a **Settings > MQTT...** o haga clic en **Settings...** en el encabezado del applet MQTT.
2. Haga clic en la pestaña **Subscriptions**.
3. Haga clic en **Add** para insertar una nueva fila en la tabla de temas.
4. Haga doble clic en la celda **Topic** y escriba la cadena completa del tema MQTT (por ejemplo, `rotator/azimuth`).
5. En la columna **Display**, marque la casilla para mostrar el último valor del tema como superposición en el panadapter. Déjela sin marcar para suscribirse sin mostrar el valor.
6. Haga clic en **Apply** para guardar la lista de suscripciones sin cerrar el diálogo, o en **Ok** para guardar y cerrar.
7. En el applet MQTT, haga clic en **Off** para cambiar a **On** y conectar con el broker.

## Función de cada control

| Control                 | Propósito                                                                                                                                                             | Valor predeterminado                             |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| Tabla de temas          | Lista de temas MQTT suscritos. Cada fila corresponde a un tema.                                                                                                       | (vacía)                                          |
| Casilla Display         | Al marcarla, el último valor recibido del tema aparece como superposición en el panadapter.                                                                            | Sin marcar                                       |
| Add                     | Inserta una nueva fila en blanco en la tabla de temas.                                                                                                                | —                                                |
| Remove                  | Elimina la(s) fila(s) seleccionada(s) de la tabla de temas.                                                                                                           | —                                                |
| Internal AetherSDR Topics | Lista de solo lectura con los temas suscritos automáticamente (por ejemplo, actualizaciones de alias de antena). No se pueden eliminar.                                 | Consulte la lista de solo lectura en el diálogo  |
| Settings...             | Abre el cuadro de diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.               | Nuevo en v26.5.3. Reemplaza los campos en línea Host/Port/User/Pass/TLS/Topics. |
| Publish buttons         | Al hacer clic, publica la carga útil configurada en el tema configurado mediante MqttClient::publish. Los botones se configuran en el cuadro de diálogo de Configuración MQTT. | Solo activos mientras está conectado. Se configuran mediante la pestaña Publish Buttons en MqttSettingsDialog. |
| Message log             | Muestra los mensajes recibidos como líneas 'topic: value'. También procesa actualizaciones de alias de antena desde MQTT.                                              | Limitado a 50 entradas.                          |
| Enable (Off/On)         | Conecta o desconecta del broker usando la configuración de MqttSettings. Emite connectRequested/disconnectRequested y guarda el estado de conexión habilitada.           | La contraseña se carga desde el llavero del sistema al activar por primera vez. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'. |
| Status label            | Muestra el estado de la conexión: verde "Connected", gris "Disconnected" o un mensaje de error con el color predeterminado.                                             | "Disconnected"                                   |

## Consejos

- La superposición del panadapter muestra el valor del mensaje recibido más recientemente para cada tema con Display habilitado. Las etiquetas de superposición se truncan para ajustarse, por lo que se recomienda mantener los nombres de los temas cortos.
- Un tema se suscribe inmediatamente al conectar con el broker (activando **On** en el applet). No es necesario reconectar después de cambiar las suscripciones; alterne **Off** y luego **On** para aplicar los cambios.
- Si la etiqueta de estado muestra "Waiting for keychain", la contraseña del llavero del sistema aún no se ha cargado. Alterne a Off y luego a On nuevamente para iniciar la recuperación del llavero.
- El registro de mensajes ahora también muestra los mensajes transmitidos con un prefijo "TX", lo que le ayuda a confirmar que los botones de publicación están funcionando.

## Relacionado

- [Overlay an MQTT value on the panadapter](overlay-an-mqtt-value-on-the-panadapter.md)
- [Configure MQTT broker connection (host, port, credentials, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
