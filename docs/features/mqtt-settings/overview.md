# Resumen de la Configuración MQTT

El diálogo de Configuración MQTT es la interfaz central para toda la funcionalidad MQTT en AetherSDR. Permite conectarse a un broker MQTT, suscribirse a temas (con visualización opcional en la superposición del panadapter) y definir hasta 12 botones de publicación. Esta página describe el diálogo en su conjunto y remite a instrucciones paso a paso para tareas individuales.

## Cómo funciona

El diálogo de Configuración MQTT reemplaza el panel de configuración anterior dentro del applet. Está organizado en tres pestañas:

- **Broker** — host del broker MQTT, puerto, nombre de usuario, contraseña, TLS y certificado CA.
- **Subscriptions** — Una tabla de temas a los que su radio se suscribe. Cada fila tiene un Tema editable y una casilla de verificación Mostrar que muestra los datos del tema en la superposición del panadapter. Debajo de la tabla hay un cuadro de grupo de solo lectura que enumera los temas internos de AetherSDR que se suscriben automáticamente y no se pueden eliminar.
- **Publish Buttons** — Una tabla que define hasta 12 botones. Cada fila tiene Etiqueta, Tema y Carga útil (todos editables). Estos botones aparecen en el applet MQTT en la bandeja del Panel de Applets. Debajo de la tabla hay un cuadro de grupo de solo lectura que enumera los temas internos de AetherSDR que se publican automáticamente y no se pueden modificar.

El diálogo también incluye los botones Ok, Apply y Cancel. Apply guarda toda la configuración (conexión, temas, botones y contraseña) sin cerrar el diálogo.

## Función de cada control

### Pestaña Broker

| Control | Etiqueta | Valor predeterminado | Rango | Comportamiento | Clave de configuración |
|---------|----------|----------------------|-------|----------------|------------------------|
| Campo de texto | Host | `localhost` | — | Nombre de host o dirección IP del broker. | `MqttHost` |
| Cuadro giratorio | Port | `1883` | 1–65535 | Puerto TCP del broker. Cambia automáticamente a 8883 cuando se activa TLS y viceversa. | `MqttPort` |
| Campo de texto | User | *(vacío)* | — | Nombre de usuario del broker (opcional). | `MqttUser` |
| Campo de texto (enmascarado) | Password | *(vacío)* | — | Contraseña del broker (opcional). Se almacena en el llavero del sistema cuando está disponible; en caso contrario, se guarda como texto plano en la clave `MqttPass` de AppSettings. | — |
| Casilla de verificación | Use TLS | sin marcar | — | Habilita el cifrado TLS. Cambia automáticamente el puerto entre 1883 y 8883. Muestra/oculta la fila del certificado CA. | `MqttTls` |
| Campo de texto + botón Examinar | CA cert | *(vacío)* | — | Ruta a un archivo de certificado CA. En blanco significa usar el lote de CA del sistema. La fila solo es visible cuando Use TLS está marcada. | `MqttCaFile` |

### Pestaña Subscriptions

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Columnas de tabla | Topic, Display | Topic es un campo de texto editable. Display es una casilla de verificación; cuando está marcada, la carga útil del tema se dibuja en la superposición del panadapter. |
| Botón pulsador | Add | Inserta una nueva fila vacía. |
| Botón pulsador | Remove | Elimina todas las filas seleccionadas. |

El cuadro de grupo **Internal AetherSDR Topics** enumera los temas que se suscriben automáticamente cada vez que MQTT se conecta. Estos temas no pueden ser eliminados por el usuario.

### Pestaña Publish Buttons

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Columnas de tabla | Label, Topic, Payload | Las tres columnas son texto editable. Label es el texto del botón que se muestra en el applet MQTT. |
| Botón pulsador | Add | Inserta una nueva fila vacía. Deshabilitado cuando la tabla ya tiene 12 filas. |
| Botón pulsador | Remove | Elimina todas las filas seleccionadas. |

El cuadro de grupo **Internal AetherSDR Topics** enumera los temas que se publican automáticamente cuando MQTT está conectado. Estos temas no son configurables por el usuario. Actualmente se publican los siguientes temas:

- `aethersdr/cw/decode`

Este cuadro de grupo es parte de la pestaña Publish Buttons y muestra los temas en un área de texto de solo lectura que permite la selección de texto con el ratón.

## Consejos

- Haga clic en Apply para guardar su configuración sin cerrar el diálogo. Esto es útil si desea probar la conexión inmediatamente.
- El campo Password almacena las credenciales en el llavero del sistema cuando `HAVE_KEYCHAIN` está configurado. Las contraseñas heredadas en texto plano en la clave `MqttPass` de AppSettings se migran al primer guardado.

## Relacionado

- [Configure MQTT broker connection (host, port, credentials, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [Subscribe to MQTT topics and toggle panadapter display](../mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Add or remove publish buttons](add-or-remove-publish-buttons.md)
- [Configure CA certificate for TLS MQTT](configure-ca-certificate-for-tls-mqtt.md)
- [Open MQTT settings from the MQTT applet](open-mqtt-settings-from-the-mqtt-applet.md)
