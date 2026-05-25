# Suscribirse a temas MQTT y alternar la visualización del panadapter

Agregue suscripciones a temas MQTT y controle si el último valor de cada tema se muestra como superposición en el panadapter. Esto le permite monitorear la telemetría de la estación — como la posición del rotador de antena, datos meteorológicos o el estado del amplificador — directamente en la pantalla del espectro.

## Antes de comenzar

- Debe tener un broker MQTT funcional accesible desde su máquina con AetherSDR.
- El applet MQTT debe estar visible (alterne el botón de la bandeja MQTT en la barra lateral derecha si está oculto).

## Pasos

1. Abra el cuadro de diálogo MQTT Settings: vaya a **Settings > MQTT...** o haga clic en **Settings...** en el encabezado del applet MQTT.
2. Haga clic en la pestaña **Subscriptions**.
3. Haga clic en **Add** para insertar una nueva fila en la tabla de temas.
4. Haga doble clic en la celda **Topic** y escriba la cadena completa del tema MQTT (ej. `rotator/azimuth`).
5. En la columna **Display**, marque la casilla para mostrar el último valor del tema como superposición en el panadapter. Déjela sin marcar para suscribirse sin mostrar.
6. Haga clic en **Apply** para guardar la lista de suscripciones sin cerrar el cuadro de diálogo, u **Ok** para guardar y cerrar.
7. En el applet MQTT, haga clic en **Off** para alternar a **On** y conectarse al broker.

## Qué hace cada control

| Control | Propósito | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| Tabla de temas | Lista de temas MQTT suscritos. Cada fila es un tema. | (vacía) | Cualquier cadena de tema MQTT válida | `MqttSettings` (JSON anidado) |
| Casilla de verificación Display | Cuando está marcada, el último valor recibido del tema aparece como superposición en el panadapter. | Sin marcar | — | misma que arriba |
| Add | Inserta una nueva fila en blanco en la tabla de temas. | — | — | — |
| Remove | Elimina la(s) fila(s) seleccionada(s) de la tabla de temas. | — | — | — |
| Internal AetherSDR Topics | Lista de solo lectura de temas suscritos automáticamente (ej. actualizaciones de alias de antena). No se pueden eliminar. | Consulte la lista de solo lectura en el cuadro de diálogo | — | — |

## Consejos

- La superposición del panadapter muestra el valor del mensaje recibido más recientemente para cada tema con Display habilitado. Las etiquetas de superposición se truncan para ajustarse, por lo que mantenga los nombres de los temas cortos.
- Un tema se suscribe inmediatamente cuando se conecta al broker (alterne a **On** en el applet). No es necesario reconectarse después de cambiar las suscripciones — alterne a **Off** y luego a **On** para aplicar los cambios.

## Relacionado

- [Overlay an MQTT value on the panadapter](overlay-an-mqtt-value-on-the-panadapter.md)
- [Configure MQTT broker connection (host, port, credentials, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
