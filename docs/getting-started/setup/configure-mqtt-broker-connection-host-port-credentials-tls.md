# Configurar la conexión del broker MQTT (host, puerto, credenciales, TLS)

Esta página explica cómo introducir los datos de conexión de su broker MQTT para que AetherSDR pueda publicar el estado de la radio y suscribirse a temas.

## Antes de comenzar

- Necesita el nombre de host o la dirección IP de su broker MQTT.
- Necesita el puerto TCP del broker (1883 por defecto, o 8883 con TLS).
- Si el broker requiere autenticación, tenga el nombre de usuario y la contraseña listos.
- Si usa TLS con un certificado CA personalizado, tenga disponible la ruta del archivo de certificado.

## Pasos

1. Abra **Settings > MQTT...**. Se abre el diálogo MQTT Settings en la pestaña Broker.
2. En **Host**, escriba el nombre de host o la dirección IP del broker (por defecto `localhost`).
3. En **Port**, establezca el puerto TCP (1883 por defecto, rango válido 1–65535).
4. Opcionalmente, introduzca un **User** y **Password** para la autenticación del broker.
5. Si el broker requiere TLS, marque **Use TLS**. El valor de Port cambia automáticamente de 1883 a 8883 (y vuelve a 1883 al desmarcarlo).
6. Si usa un certificado CA personalizado, introduzca su ruta en **CA cert** o haga clic en **Browse...** para seleccionar el archivo. Déjelo en blanco para usar el paquete de CA del sistema.
7. Haga clic en **Apply** para guardar los ajustes de conexión sin cerrar el diálogo, o en **OK** para guardar y cerrar.

## Qué hace cada control

| Control | Valor por defecto | Rango válido | Clave de ajuste | Comportamiento |
|---------|-------------------|--------------|-----------------|----------------|
| Host | `localhost` | cualquier nombre de host/IP | `MqttHost` | Nombre de host o dirección IP del broker |
| Port | `1883` | 1–65535 | `MqttPort` | Puerto TCP del broker; cambia automáticamente a 8883 cuando TLS está habilitado |
| User | (vacío) | cualquier texto | `MqttUser` | Nombre de usuario del broker (opcional) |
| Password | (vacío) | cualquier texto | llavero del sistema (qt6keychain) con respaldo de texto sin cifrar heredado | Contraseña del broker (opcional, enmascarada) |
| Use TLS | desmarcado | – | `MqttTls` | Habilita el cifrado TLS; muestra/oculta la fila del certificado CA |
| CA cert | (vacío) | ruta de archivo o en blanco | `MqttCaFile` | Ruta a un archivo de certificado CA personalizado; en blanco = paquete de CA del sistema |

### Almacenamiento de la contraseña

La contraseña MQTT se almacena en el llavero del sistema (mediante qt6keychain) cuando está disponible. Cuando el llavero no está disponible, la contraseña se conserva solo en memoria durante la sesión actual y debe volver a introducirse en el siguiente inicio. No se escribe ninguna copia en texto sin cifrar en el almacén de ajustes. Una contraseña en texto sin cifrar heredada de versiones anteriores se migra al llavero (o al almacenamiento solo de sesión) en el primer uso y se elimina la clave de ajuste antigua.

## Pestaña Subscriptions

La pestaña **Subscriptions** reemplaza el campo de texto Topics separado por comas de versiones anteriores. Contiene:

- **Tabla de temas**: Cada fila tiene un campo de texto Topic editable y una casilla de verificación Display. Cuando está marcada, los mensajes del tema aparecen en la superposición del panadapter. Use los botones **Add** y **Remove** debajo de la tabla para gestionar las filas.
- **Temas internos de AetherSDR**: Un grupo de cuadros de solo lectura que enumera los temas a los que AetherSDR se suscribe automáticamente cuando la conexión MQTT está activa. Estos temas no se pueden eliminar por el usuario. Cada tema tiene una casilla de verificación para habilitarlo o deshabilitarlo. Los temas con comportamiento no regulable (temas de alias de antena) están siempre activos y aparecen atenuados. Los temas de suscripción internos disponibles son:

  | Tema | Descripción | Deshabilitable por el usuario |
  |------|-------------|-------------------------------|
  | `aethersdr/antenna/alias/+` | Nombre de antena (por puerto) | No |
  | `aethersdr/antenna/alias/bulk` | Nombres de antena (masivo) | No |
  | `aethersdr/cw/transmit` | Entrada del manipulador CW | Sí (desactivado por defecto) |
  | `aethersdr/ax25/tx` | Transmisión AX.25 | Sí (desactivado por defecto) |

  Desmarque la casilla junto a un tema regulable para evitar que AetherSDR se suscriba a él.

## Pestaña Publish Buttons

La pestaña **Publish Buttons** le permite definir hasta 12 botones de publicación. Cada fila de la tabla tiene tres campos de texto editables: **Label**, **Topic** y **Payload**. Use los botones **Add** y **Remove** debajo de la tabla para gestionar las filas. El botón Add se deshabilita cuando se alcanzan 12 filas. Las definiciones de botones se comparten con el applet MQTT.

La pestaña también incluye un grupo de cuadros **Internal AetherSDR Topics** que muestra los temas que AetherSDR publica automáticamente cuando la conexión MQTT está activa. Cada tema tiene una casilla de verificación para habilitarlo o deshabilitarlo. Los temas de publicación internos disponibles son:

| Tema | Descripción | Habilitado por defecto |
|------|-------------|------------------------|
| `aethersdr/cw/decode` | Texto decodificado en CW | Sí |
| `aethersdr/radio/state` | Estado de VFO / modo / TX de la radio | Sí |
| `aethersdr/ax25/rx` | Tramas AX.25 recibidas | Sí |

Desmarque la casilla junto a un tema para evitar que AetherSDR publique en él.

## Consejos

- Si su broker no requiere contraseña, deje el campo **Password** vacío.
- Cuando **Use TLS** está marcado, AetherSDR cambia automáticamente el puerto a 8883. Si su broker usa un puerto TLS diferente, ajuste **Port** manualmente después de marcar TLS.
- La contraseña se almacena en el llavero del sistema cuando está disponible; de lo contrario, se conserva solo durante la sesión actual y debe volver a introducirse en el siguiente inicio.
- Los scripts de retransmisión que reenvían `aethersdr/cw/decode` a `aethersdr/cw/transmit` deben filtrar por el espacio de nombres del tema (`aethersdr/...`) para evitar volver a publicar la salida propia de AetherSDR en sí misma y crear un bucle de retroalimentación.

## Relacionado

- [Configurar el certificado CA para TLS MQTT](../../features/mqtt-settings/configure-ca-certificate-for-tls-mqtt.md)
- [Suscribirse a temas MQTT y alternar la visualización en el panadapter](../../features/mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Añadir o eliminar botones de publicación](../../features/mqtt-settings/add-or-remove-publish-buttons.md)
