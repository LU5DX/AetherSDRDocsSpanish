# Configurar la conexión al broker MQTT (host, puerto, credenciales, TLS)

Esta página explica cómo ingresar los detalles de conexión para su broker MQTT, de modo que AetherSDR pueda publicar el estado de la radio y suscribirse a tópicos.

## Antes de comenzar

- Necesita el nombre de host o la dirección IP de su broker MQTT.
- Necesita el puerto TCP del broker (1883 por defecto, o 8883 con TLS).
- Si el broker requiere autenticación, tenga listos el nombre de usuario y la contraseña.
- Si utiliza TLS con un certificado CA personalizado, tenga disponible la ruta del archivo del certificado.

## Pasos

1. Abra **Settings > MQTT...**. El cuadro de diálogo de configuración MQTT se abre en la pestaña **Broker**.
2. En **Host**, escriba el nombre de host o la dirección IP del broker (por defecto `localhost`).
3. En **Port**, establezca el puerto TCP (1883 por defecto, rango válido 1–65535).
4. Opcionalmente, ingrese un **User** y **Password** para la autenticación del broker.
5. Si el broker requiere TLS, marque **Use TLS**. El valor de **Port** cambia automáticamente de 1883 a 8883 (y vuelve al desmarcarlo).
6. Si utiliza un certificado CA personalizado, ingrese su ruta en **CA cert** o haga clic en **Browse...** para seleccionar el archivo. Déjelo en blanco para usar el paquete de CA del sistema.
7. Haga clic en **Apply** para guardar la configuración de conexión sin cerrar el cuadro de diálogo, o haga clic en **OK** para guardar y cerrar.

## Qué hace cada control

| Control | Valor por defecto | Rango válido | Clave de configuración | Comportamiento |
|---------|-------------------|--------------|------------------------|----------------|
| Host | `localhost` | cualquier hostname/IP | `MqttHost` (migrado a `MqttSettings`) | Nombre de host o dirección IP del broker |
| Port | `1883` | 1–65535 | `MqttPort` (migrado a `MqttSettings`) | Puerto TCP del broker; cambia automáticamente a 8883 cuando TLS está habilitado |
| User | (vacío) | cualquier texto | `MqttUser` (migrado a `MqttSettings`) | Nombre de usuario del broker (opcional) |
| Password | (vacío) | cualquier texto | almacenado en el llavero del sistema (qt6keychain) o en texto plano como alternativa | Contraseña del broker (opcional, enmascarada) |
| Use TLS | desmarcado | – | `MqttTls` (migrado a `MqttSettings`) | Habilita el cifrado TLS; muestra/oculta la fila del certificado CA |
| CA cert | (vacío) | ruta de archivo o vacío | `MqttCaFile` (migrado a `MqttSettings`) | Ruta a un archivo de certificado CA personalizado; vacío = paquete CA del sistema |

## Pestaña Subscriptions

La pestaña **Subscriptions** reemplaza el campo de texto de tópicos separados por comas de versiones anteriores. Contiene:

- **Tabla de tópicos**: Cada fila tiene un campo de texto editable para el tópico y una casilla **Display**. Cuando está marcada, los mensajes del tópico aparecen en la superposición del panadapter. Use los botones **Add** y **Remove** debajo de la tabla para administrar las filas.
- **Internal AetherSDR Topics**: Un cuadro de grupo de solo lectura que enumera los tópicos a los que AetherSDR se suscribe automáticamente cuando la conexión MQTT está activa. Estos tópicos no pueden ser eliminados por el usuario.

## Pestaña Publish Buttons

La pestaña **Publish Buttons** le permite definir hasta 12 botones de publicación. Cada fila en la tabla tiene tres campos de texto editables: **Label**, **Topic** y **Payload**. Use los botones **Add** y **Remove** debajo de la tabla para administrar las filas. El botón **Add** está deshabilitado cuando se alcanzan 12 filas.

La pestaña también incluye un cuadro de grupo **Internal AetherSDR Topics** que muestra los tópicos que AetherSDR publica automáticamente cuando la conexión MQTT está activa. Estos tópicos no son configurables por el usuario.

Tópicos internos de publicación actuales:
- `aethersdr/cw/decode`

## Consejos

- Si su broker no requiere contraseña, deje el campo **Password** vacío.
- Cuando **Use TLS** está marcado, AetherSDR cambia automáticamente el puerto a 8883. Si su broker usa un puerto TLS diferente, ajuste **Port** manualmente después de marcar TLS.
- La contraseña se almacena en el llavero del sistema cuando está disponible; de lo contrario, se almacena en texto plano en AppSettings.

## Relacionado

- [Configure CA certificate for TLS MQTT](../../features/mqtt-settings/configure-ca-certificate-for-tls-mqtt.md)
- [Subscribe to MQTT topics and toggle panadapter display](../../features/mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Add or remove publish buttons](../../features/mqtt-settings/add-or-remove-publish-buttons.md)
