# Descripción general de la configuración MQTT

El cuadro de diálogo de configuración MQTT es la interfaz central de configuración para todas las funciones MQTT en AetherSDR. Permite conectarse a un broker MQTT, suscribirse a temas (con visualización opcional en la superposición del panadapter), definir hasta 12 botones de publicación y habilitar o deshabilitar temas MQTT internos individuales de AetherSDR. Esta página describe el diálogo en su conjunto y señala las instrucciones paso a paso para tareas individuales.

## Cómo funciona

El cuadro de diálogo de configuración MQTT reemplaza el panel de configuración anterior dentro del applet. Está organizado en tres pestañas:

- **Broker** — Host del broker MQTT, puerto, nombre de usuario, contraseña, TLS y certificado CA.
- **Subscriptions** — Una tabla de temas a los que su radio se suscribe. Cada fila tiene un Tema editable y una casilla de verificación Mostrar que muestra los datos del tema en la superposición del panadapter. Debajo de la tabla hay un cuadro de grupo que enumera los temas de suscripción internos de AetherSDR. Cada tema interno tiene una casilla de verificación Habilitar; los temas etiquetados como siempre activos aparecen atenuados y no se pueden deshabilitar.
- **Publish Buttons** — Una tabla que define hasta 12 botones. Cada fila tiene Etiqueta, Tema y Carga útil (todos editables). Estos botones aparecen en el applet MQTT en la bandeja del Panel de Applets. Debajo de la tabla hay un cuadro de grupo que enumera los temas de publicación internos de AetherSDR con casillas de verificación Habilitar.

El diálogo también incluye botones Aceptar, Aplicar y Cancelar. Aplicar guarda toda la configuración (conexión, temas, definiciones de botones, contraseña y estados de habilitación de temas internos) sin cerrar el diálogo.

## Qué hace cada control

### Pestaña Broker

| Control | Etiqueta | Valor predeterminado | Rango | Comportamiento | Clave de configuración |
|---------|----------|----------------------|-------|----------------|------------------------|
| Campo de texto | Host | `localhost` | — | Nombre de host o dirección IP del broker. | `MqttHost` |
| Cuadro de giro | Port | `1883` | 1–65535 | Puerto TCP del broker. Cambia automáticamente a 8883 cuando se activa TLS y viceversa. | `MqttPort` |
| Campo de texto | User | *(vacío)* | — | Nombre de usuario del broker (opcional). | `MqttUser` |
| Campo de texto (enmascarado) | Password | *(vacío)* | — | Contraseña del broker (opcional). Se almacena en el llavero del sistema cuando está disponible; de lo contrario, recurre a la clave de texto plano `MqttPass` en AppSettings. | — |
| Casilla de verificación | Use TLS | desmarcada | — | Habilita el cifrado TLS. Cambia automáticamente el puerto entre 1883 y 8883. Muestra u oculta la fila del certificado CA. | `MqttTls` |
| Campo de texto + botón Examinar | CA cert | *(vacío)* | — | Ruta a un archivo de certificado CA. En blanco significa usar el paquete CA del sistema. La fila solo es visible cuando Use TLS está marcada. | `MqttCaFile` |

### Pestaña Subscriptions

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Columnas de tabla | Topic, Display | Topic es un campo de texto editable. Display es una casilla de verificación; cuando está marcada, la carga útil del tema se dibuja en la superposición del panadapter. |
| Botón pulsador | Add | Inserta una nueva fila vacía. |
| Botón pulsador | Remove | Elimina todas las filas seleccionadas. |

El cuadro de grupo **Internal AetherSDR Topics** enumera los temas a los que se suscribe automáticamente cuando MQTT se conecta. Cada tema tiene una casilla de verificación Habilitar. Los temas etiquetados como siempre activos se muestran atenuados y no se pueden deshabilitar. Los siguientes temas de suscripción internos están disponibles:

| Tema | Descripción | Predeterminado | Deshabilitable por el usuario |
|------|-------------|----------------|-------------------------------|
| `aethersdr/antenna_alias/+/name` | Nombre de antena (por puerto) | Activado | No (siempre activo) |
| `aethersdr/antenna_alias/bulk` | Nombres de antena (masivo) | Activado | No (siempre activo) |
| `aethersdr/cw/transmit` | Entrada del keyer CW | Activado | Sí |
| `aethersdr/ax25/tx` | Transmisión AX.25 | Activado | Sí |

### Pestaña Publish Buttons

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Columnas de tabla | Label, Topic, Payload | Las tres columnas son texto editable. Label es el texto del botón que se muestra en el applet MQTT. |
| Botón pulsador | Add | Inserta una nueva fila vacía. Deshabilitado cuando la tabla ya tiene 12 filas. |
| Botón pulsador | Remove | Elimina todas las filas seleccionadas. |

El cuadro de grupo **Internal AetherSDR Topics** enumera los temas que se publican automáticamente cuando MQTT está conectado. Cada tema tiene una casilla de verificación Habilitar. Los siguientes temas de publicación internos están disponibles:

| Tema | Descripción | Predeterminado | Deshabilitable por el usuario |
|------|-------------|----------------|-------------------------------|
| `aethersdr/cw/decode` | Texto decodificado CW | Activado | Sí |
| `aethersdr/radio/state` | Estado VFO / modo / TX de la radio | Desactivado | Sí |
| `aethersdr/ax25/rx` | Tramas recibidas AX.25 | Desactivado | Sí |

## Consejos

- Haga clic en Aplicar para guardar la configuración sin cerrar el diálogo. Esto es útil si desea probar la conexión de inmediato.
- El campo de contraseña almacena las credenciales en el llavero del sistema cuando `HAVE_KEYCHAIN` está configurado. Las contraseñas de texto plano heredadas en la clave `MqttPass` de AppSettings se migran al primer guardado.
- Deshabilite los temas internos que no necesite para reducir el tráfico MQTT. Los temas etiquetados como "siempre activos" no se pueden deshabilitar porque son necesarios para la funcionalidad de alias de antena.
- Si utiliza scripts de retransmisión que reenvían `aethersdr/cw/decode` a `aethersdr/cw/transmit`, filtre en el espacio de nombres del tema (`aethersdr/...`) para evitar volver a publicar la propia salida de AetherSDR en sí mismo y crear un bucle de retroalimentación.

## Relacionado

- [Configure MQTT broker connection (host, port, credentials, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [Subscribe to MQTT topics and toggle panadapter display](../mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Add or remove publish buttons](add-or-remove-publish-buttons.md)
- [Enable or disable internal MQTT topics](enable-or-disable-internal-mqtt-topics.md)
- [Configure CA certificate for TLS MQTT](configure-ca-certificate-for-tls-mqtt.md)
- [Open MQTT settings from the MQTT applet](open-mqtt-settings-from-the-mqtt-applet.md)
