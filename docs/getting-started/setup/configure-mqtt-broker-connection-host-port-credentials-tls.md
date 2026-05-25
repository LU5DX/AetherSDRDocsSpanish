# Configurar la conexión con el broker MQTT (host, puerto, credenciales, TLS)

Esta página explica cómo ingresar los detalles de conexión para su broker MQTT, de modo que AetherSDR pueda publicar el estado de la radio y suscribirse a tópicos.

## Antes de comenzar

- Necesita el nombre de host o la dirección IP de su broker MQTT.
- Necesita el puerto TCP del broker (1883 por defecto, o 8883 con TLS).
- Si el broker requiere autenticación, tenga listos el nombre de usuario y la contraseña.
- Si usa TLS con un certificado CA personalizado, tenga disponible la ruta del archivo del certificado.

## Pasos

1. Abra **Settings > MQTT...**. Se abre el diálogo de configuración MQTT en la pestaña Broker.
2. En **Host**, escriba el nombre de host o la dirección IP del broker (por defecto `localhost`).
3. En **Port**, establezca el puerto TCP (1883 por defecto, rango válido 1–65535).
4. Opcionalmente, ingrese un **User** y **Password** para la autenticación del broker.
5. Si el broker requiere TLS, marque **Use TLS**. El valor de Port cambia automáticamente de 1883 a 8883 (y vuelve al desmarcarlo).
6. Si usa un certificado CA personalizado, ingrese su ruta en **CA cert** o haga clic en **Browse...** para seleccionar el archivo. Déjelo en blanco para usar el paquete de CA del sistema.
7. Haga clic en **Apply** para guardar la configuración de conexión sin cerrar el diálogo, o en **OK** para guardar y cerrar.

## Qué hace cada control

| Control | Valor predet. | Rango válido | Clave de ajuste | Comportamiento |
|---------|---------------|--------------|-----------------|----------------|
| Host | `localhost` | cualquier host/IP | `MqttHost` (migrado a `MqttSettings`) | Nombre de host o IP del broker |
| Port | `1883` | 1–65535 | `MqttPort` (migrado a `MqttSettings`) | Puerto TCP del broker; cambia automáticamente a 8883 cuando TLS está habilitado |
| User | (vacío) | cualquier texto | `MqttUser` (migrado a `MqttSettings`) | Nombre de usuario del broker (opcional) |
| Password | (vacío) | cualquier texto | almacenado en el llavero del sistema (qt6keychain) o en texto plano como alternativa | Contraseña del broker (opcional, enmascarada) |
| Use TLS | sin marcar | – | `MqttTls` (migrado a `MqttSettings`) | Habilita el cifrado TLS; muestra/oculta la fila del certificado CA |
| CA cert | (vacío) | ruta de archivo o blanco | `MqttCaFile` (migrado a `MqttSettings`) | Ruta a un archivo de certificado CA personalizado; blanco = paquete CA del sistema |

## Consejos

- Si su broker no requiere contraseña, deje vacío el campo **Password**.
- Cuando **Use TLS** está marcado, AetherSDR cambia automáticamente el puerto a 8883. Si su broker usa un puerto TLS diferente, ajuste **Port** manualmente después de marcar TLS.
- La contraseña se almacena en el llavero del sistema cuando está disponible; de lo contrario, se almacena como texto plano en AppSettings.

## Relacionado

- [Configure CA certificate for TLS MQTT](../../features/mqtt-settings/configure-ca-certificate-for-tls-mqtt.md)
- [Subscribe to MQTT topics and toggle panadapter display](../../features/mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Add or remove publish buttons](../../features/mqtt-settings/add-or-remove-publish-buttons.md)
