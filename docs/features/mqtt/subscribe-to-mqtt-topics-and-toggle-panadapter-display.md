# Suscribirse a temas MQTT y alternar la visualización en el panadapter

Agregue suscripciones a temas MQTT y controle si el último valor de cada tema se muestra como una superposición en el panadapter. Esto le permite monitorear la telemetría de la estación — como la posición del rotador de antena, datos meteorológicos o el estado del amplificador — directamente en la pantalla del espectro.

## Antes de comenzar

- Debe tener un broker MQTT funcional accesible desde su equipo con AetherSDR.
- El applet MQTT debe estar visible (alterne el botón de la bandeja MQTT en la barra lateral derecha si está oculto).

## Pasos

1. Abra el diálogo de configuración MQTT: vaya a **Settings > MQTT...** o haga clic en **Settings...** en el encabezado del applet MQTT.
2. Haga clic en la pestaña **Subscriptions**.
3. Haga clic en **Add** para insertar una nueva fila en la tabla de temas.
4. Haga doble clic en la celda **Topic** y escriba la cadena completa del tema MQTT (ej. `rotator/azimuth`).
5. En la columna **Display**, marque la casilla para mostrar el último valor del tema como una superposición en el panadapter. Déjela sin marcar para suscribirse sin mostrar el valor.
6. Haga clic en **Apply** para guardar la lista de suscripciones sin cerrar el diálogo, o en **Ok** para guardar y cerrar.
7. En el applet MQTT, haga clic en **Off** para cambiarlo a **On** y conectarse al broker.

## Función de cada control

| Control                   | Propósito                                                                                                                   | Valor predeterminado                                                       |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| Tabla de temas            | Lista de temas MQTT suscritos. Cada fila es un tema.                                                                        | (vacía)                                                                    |
| Casilla de verificación Display | Cuando está marcada, el último valor recibido del tema aparece como superposición en el panadapter.                         | Sin marcar                                                                 |
| Add                       | Inserta una nueva fila en blanco en la tabla de temas.                                                                      | —                                                                          |
| Remove                    | Elimina la(s) fila(s) seleccionada(s) de la tabla de temas.                                                                 | —                                                                          |
| Internal AetherSDR Topics | Lista de solo lectura de temas suscritos automáticamente (ej. actualizaciones de alias de antena). No se pueden eliminar.   | Vea la lista de solo lectura en el diálogo                                 |
| Settings...               | Abre el diálogo de configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. | Nuevo en v26.5.3. Reemplaza los campos inline de Host/Puerto/Usuario/Contraseña/TLS/Temas. |
| Publish buttons           | Hasta 12 botones configurables que publican una carga útil en un tema al hacer clic. Se configuran en el diálogo de configuración MQTT. | (ninguno)                                                                  |
| Message log               | Muestra los mensajes recibidos como líneas `tema: valor`, limitado a las últimas 50 entradas.                              | (vacío)                                                                    |
| Enable (Off/On)           | Botón de alternancia para conectar o desconectar del broker. La contraseña se carga desde el llavero del sistema al activarlo por primera vez. | Off                                                                        |
| Status label              | Muestra el estado de la conexión: verde "Connected", gris "Disconnected" o mensaje de error en color predeterminado.         | "Disconnected"                                                             |

## Consejos

- La superposición del panadapter muestra el valor del mensaje recibido más recientemente para cada tema con Display habilitado. Las etiquetas de superposición se truncan para ajustarse, por lo que mantenga los nombres de los temas cortos.
- Un tema se suscribe inmediatamente cuando se conecta al broker (alterne a **On** en el applet). No es necesario reconectarse después de cambiar las suscripciones; alterne a **Off** y luego a **On** para aplicar los cambios.
- Si la etiqueta de estado muestra "Waiting for keychain", la contraseña del llavero del sistema aún no se ha cargado. Alterne a Off y luego a On nuevamente para activar la recuperación del llavero.

## Relacionado

- [Overlay an MQTT value on the panadapter](overlay-an-mqtt-value-on-the-panadapter.md)
- [Configure MQTT broker connection (host, port, credentials, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
