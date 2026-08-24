# Descripción general de la configuración de MQTT

El diálogo de Configuración de MQTT es la interfaz central de configuración para toda la funcionalidad de MQTT en AetherSDR. Permite conectarse a un broker MQTT, suscribirse a temas (con visualización opcional superpuesta en el panadapter), definir hasta 12 botones de publicación y habilitar o deshabilitar temas MQTT internos individuales de AetherSDR. Esta página describe el diálogo en su conjunto y señala instrucciones paso a paso para tareas específicas.

## Cómo funciona

El diálogo de Configuración de MQTT reemplaza al panel de configuración anterior dentro del applet. Está organizado en tres pestañas:

- **Broker** — Host del broker MQTT, puerto, nombre de usuario, contraseña, TLS y certificado CA.
- **Subscriptions** — Una tabla de temas a los que su radio está suscrita. Cada fila tiene un Topic editable y una casilla Display que muestra los datos del tema en la superposición del panadapter. Debajo de la tabla hay un grupo que lista los temas de suscripción MQTT internos de AetherSDR. Cada tema interno tiene una casilla Enable; los temas marcados como siempre activos aparecen atenuados y no se pueden deshabilitar.
- **Publish Buttons** — Una tabla que define hasta 12 botones. Cada fila tiene Label, Topic y Payload (todos editables). Estos botones aparecen en el applet de MQTT en la bandeja del Applet Panel. Debajo de la tabla hay un grupo que lista los temas de publicación MQTT internos de AetherSDR con casillas Enable.

El diálogo también incluye botones Ok, Apply y Cancel. Apply guarda toda la configuración (conexión, temas, definiciones de botones, contraseña y estados de habilitación de temas internos) sin cerrar el diálogo.

## Qué hace cada control

### Pestaña Broker

| Control | Etiqueta | Valor predeterminado | Rango | Comportamiento | Clave de configuración |
|---------|----------|----------------------|-------|----------------|-------------------------|
| Campo de texto | Host | `localhost` | — | Nombre de host o dirección IP del broker. | `MqttHost` |
| Cuadro de giro | Port | `1883` | 1–65535 | Puerto TCP del broker. Cambia automáticamente a 8883 cuando se activa TLS y viceversa. | `MqttPort` |
| Campo de texto | User | *(vacío)* | — | Nombre de usuario del broker (opcional). | `MqttUser` |
| Campo de texto (enmascarado) | Password | *(vacío)* | — | Contraseña del broker (opcional). Se almacena en el llavero del sistema cuando está disponible. En sistemas sin soporte de llavero, la contraseña es solo para la sesión: se mantiene en memoria durante la sesión actual y debe volver a ingresarse en el siguiente inicio. Una clave heredada de texto plano `MqttPass` en AppSettings se elimina una vez migrada. | — |
| Casilla de verificación | Use TLS | sin marcar | — | Habilita el cifrado TLS. Cambia automáticamente el puerto entre 1883 y 8883. Muestra/oculta la fila del certificado CA. | `MqttTls` |
| Campo de texto + botón Browse | CA cert | *(vacío)* | — | Ruta a un archivo de certificado CA. En blanco significa usar el paquete de CA del sistema. La fila solo es visible cuando Use TLS está marcada. | `MqttCaFile` |

### Pestaña Subscriptions

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Columnas de tabla | Topic, Display | Topic es un campo de texto editable. Display es una casilla de verificación; cuando está marcada, la carga útil del tema se dibuja en la superposición del panadapter. |
| Botón pulsador | Add | Inserta una nueva fila vacía. |
| Botón pulsador | Remove | Elimina todas las filas seleccionadas. |

El grupo **Internal AetherSDR Topics** lista los temas que se suscriben automáticamente cuando MQTT se conecta. Cada tema tiene una casilla Enable. Los temas marcados como siempre activos aparecen atenuados y no se pueden deshabilitar. Estos temas internos siempre se suscriben cuando MQTT se conecta y no se pueden eliminar; solo la casilla Enable puede activar o desactivar su procesamiento. Los siguientes temas de suscripción internos están disponibles:

| Tema | Descripción | Valor predeterminado | Deshabilitable por el usuario |
|------|-------------|----------------------|-------------------------------|
| `aethersdr/antenna_alias/+/name` | Nombre de antena (por puerto) | On | No (siempre activo) |
| `aethersdr/antenna_alias/bulk` | Nombres de antena (masivo) | On | No (siempre activo) |
| `aethersdr/cw/transmit` | Entrada de manipulador CW | On | Sí |
| `aethersdr/ax25/tx` | Transmisión AX.25 | On | Sí |

### Pestaña Publish Buttons

| Control | Etiqueta | Comportamiento |
|---------|----------|----------------|
| Columnas de tabla | Label, Topic, Payload | Las tres columnas son texto editable. Label es el texto del botón que se muestra en el applet de MQTT. |
| Botón pulsador | Add | Inserta una nueva fila vacía. Deshabilitado cuando la tabla ya tiene 12 filas. |
| Botón pulsador | Remove | Elimina todas las filas seleccionadas. |

El grupo **Internal AetherSDR Topics** lista los temas que se publican automáticamente cuando MQTT está conectado. Cada tema tiene una casilla Enable. Los siguientes temas de publicación internos están disponibles:

| Tema | Descripción | Valor predeterminado | Deshabilitable por el usuario |
|------|-------------|----------------------|-------------------------------|
| `aethersdr/cw/decode` | Texto decodificado CW | On | Sí |
| `aethersdr/radio/state` | Estado VFO / modo / TX de la radio | Off | Sí |
| `aethersdr/ax25/rx` | Tramas AX.25 recibidas | Off | Sí |

## Consejos

- Haga clic en Apply para guardar su configuración sin cerrar el diálogo. Esto es útil si desea probar la conexión de inmediato.
- El campo Password almacena las credenciales en el llavero del sistema cuando `HAVE_KEYCHAIN` está definido. Las contraseñas heredadas en texto plano en la clave `MqttPass` de AppSettings se migran en el primer guardado; la clave heredada se elimina después de una migración exitosa.
- En sistemas sin soporte de llavero, la contraseña de MQTT nunca se escribe en el almacén de configuración. Se mantiene en memoria solo para la sesión actual, por lo que debe volver a ingresarla después de reiniciar AetherSDR.
- Deshabilite los temas internos que no necesite para reducir el tráfico MQTT. Los temas marcados como "siempre activos" no se pueden deshabilitar porque son necesarios para la funcionalidad de alias de antena.
- Si utiliza scripts de retransmisión que reenvían `aethersdr/cw/decode` hacia `aethersdr/cw/transmit`, filtre por el espacio de nombres del tema (`aethersdr/...`) para evitar republicar la propia salida de AetherSDR de vuelta a sí mismo y crear un bucle de retroalimentación.

## Relacionado

- [Configurar la conexión al broker MQTT (host, puerto, credenciales, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [Suscribirse a temas MQTT y alternar la visualización en el panadapter](../mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Agregar o eliminar botones de publicación](add-or-remove-publish-buttons.md)
- Habilitar o deshabilitar temas MQTT internos
- [Configurar certificado CA para MQTT TLS](configure-ca-certificate-for-tls-mqtt.md)
- [Abrir la configuración de MQTT desde el applet de MQTT](open-mqtt-settings-from-the-mqtt-applet.md)
