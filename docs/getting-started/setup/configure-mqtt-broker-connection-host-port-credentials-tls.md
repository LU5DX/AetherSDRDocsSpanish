# Configurar la conexión al broker MQTT (host, puerto, credenciales, TLS)

Esta página explica cómo ingresar los detalles de conexión para su broker MQTT, de modo que AetherSDR pueda publicar el estado de la radio y suscribirse a tópicos.

## Antes de comenzar

- Necesita el nombre de host o dirección IP de su broker MQTT.
- Necesita el puerto TCP del broker (por defecto 1883, o 8883 con TLS).
- Si el broker requiere autenticación, tenga listos el nombre de usuario y la contraseña.
- Si usa TLS con un certificado CA personalizado, tenga disponible la ruta del archivo del certificado.

## Pasos

1. Abra **Settings > MQTT...**. Se abre el cuadro de diálogo de configuración MQTT en la pestaña Broker.
2. En **Host**, escriba el nombre de host o dirección IP del broker (por defecto `localhost`).
3. En **Port**, configure el puerto TCP (por defecto 1883, rango válido 1–65535).
4. Opcionalmente, ingrese un **User** y **Password** para la autenticación del broker.
5. Si el broker requiere TLS, marque **Use TLS**. El valor de Port cambia automáticamente de 1883 a 8883 (y vuelve al desmarcar).
6. Si usa un certificado CA personalizado, ingrese su ruta en **CA cert** o haga clic en **Browse...** para seleccionar el archivo. Déjelo vacío para usar el conjunto de CA del sistema.
7. Haga clic en **Apply** para guardar los ajustes de conexión sin cerrar el cuadro de diálogo, o en **OK** para guardar y cerrar.

## Descripción de cada control

| Control | Valor por defecto | Rango válido | Clave de ajuste | Comportamiento |
|---------|-------------------|--------------|-----------------|----------------|
| Host | `localhost` | cualquier host/IP | `MqttHost` (migrado a `MqttSettings`) | Nombre de host o IP del broker |
| Port | `1883` | 1–65535 | `MqttPort` (migrado a `MqttSettings`) | Puerto TCP del broker; cambia automáticamente a 8883 cuando TLS está habilitado |
| User | (vacío) | cualquier texto | `MqttUser` (migrado a `MqttSettings`) | Nombre de usuario del broker (opcional) |
| Password | (vacío) | cualquier texto | almacenada en el llavero del sistema (qt6keychain) o como texto plano | Contraseña del broker (opcional, enmascarada) |
| Use TLS | desmarcado | – | `MqttTls` (migrado a `MqttSettings`) | Habilita el cifrado TLS; muestra/oculta la fila de certificado CA |
| CA cert | (vacío) | ruta de archivo o vacío | `MqttCaFile` (migrado a `MqttSettings`) | Ruta a un archivo de certificado CA personalizado; vacío = conjunto de CA del sistema |

## Pestaña Subscriptions

La pestaña **Subscriptions** reemplaza el campo de texto Topics separado por comas de versiones anteriores. Contiene:

- **Tabla de tópicos**: Cada fila tiene un campo de texto Topic editable y una casilla de verificación Display. Cuando está marcada, los mensajes del tópico aparecen en la superposición del panadapter. Use los botones **Add** y **Remove** debajo de la tabla para gestionar las filas.
- **Internal AetherSDR Topics**: Un cuadro de grupo de solo lectura que muestra los tópicos a los que AetherSDR se suscribe automáticamente cuando la conexión MQTT está activa. Cada tópico tiene una casilla de verificación para habilitarlo o deshabilitarlo. Los tópicos con comportamiento no deshabilitable (tópicos de alias de antena) están siempre activos y aparecen atenuados. Los tópicos de suscripción interna disponibles son:

  | Tópico | Descripción | Deshabilitable por el usuario |
  |--------|-------------|-------------------------------|
  | `aethersdr/antenna/alias/+` | Nombre de antena (por puerto) | No |
  | `aethersdr/antenna/alias/bulk` | Nombres de antena (masivo) | No |
  | `aethersdr/cw/transmit` | Entrada del manipulador CW | Sí (desactivado por defecto) |
  | `aethersdr/ax25/tx` | Transmisión AX.25 | Sí (desactivado por defecto) |

  Desmarque la casilla junto a un tópico deshabilitable para evitar que AetherSDR se suscriba a él.

## Pestaña Publish Buttons

La pestaña **Publish Buttons** le permite definir hasta 12 botones de publicación. Cada fila de la tabla tiene tres campos de texto editables: **Label**, **Topic** y **Payload**. Use los botones **Add** y **Remove** debajo de la tabla para gestionar las filas. El botón Add se deshabilita cuando se alcanzan 12 filas.

La pestaña también incluye un cuadro de grupo **Internal AetherSDR Topics** que muestra los tópicos que AetherSDR publica automáticamente cuando la conexión MQTT está activa. Cada tópico tiene una casilla de verificación para habilitarlo o deshabilitarlo. Los tópicos de publicación interna disponibles son:

| Tópico | Descripción | Habilitado por defecto |
|--------|-------------|------------------------|
| `aethersdr/cw/decode` | Texto descodificado en CW | Sí |
| `aethersdr/radio/state` | Estado VFO / modo / TX de la radio | Sí |
| `aethersdr/ax25/rx` | Tramas AX.25 recibidas | Sí |

Desmarque la casilla junto a un tópico para evitar que AetherSDR publique en él.

## Consejos

- Si su broker no requiere contraseña, deje el campo **Password** vacío.
- Cuando **Use TLS** está marcado, AetherSDR cambia automáticamente el puerto a 8883. Si su broker usa un puerto TLS diferente, ajuste **Port** manualmente después de marcar TLS.
- La contraseña se almacena en el llavero del sistema cuando está disponible; de lo contrario, se almacena como texto plano en AppSettings.
- Los scripts de relé que reenvían `aethersdr/cw/decode` hacia `aethersdr/cw/transmit` deben filtrar por el espacio de nombres del tópico (`aethersdr/...`) para evitar volver a publicar la salida de AetherSDR sobre sí misma y crear un bucle de realimentación.

## Relacionado

- [Configure CA certificate for TLS MQTT](../../features/mqtt-settings/configure-ca-certificate-for-tls-mqtt.md)
- [Subscribe to MQTT topics and toggle panadapter display](../../features/mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Add or remove publish buttons](../../features/mqtt-settings/add-or-remove-publish-buttons.md)
