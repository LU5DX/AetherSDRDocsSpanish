# Configurar los ajustes de MQTT

El diálogo de Ajustes de MQTT centraliza toda la configuración de MQTT: conexión al broker, suscripciones a temas y botones de publicación. Reemplaza al panel de ajustes dentro del applet de versiones anteriores.

## Antes de comenzar

- El diálogo de Ajustes de MQTT está abierto (`Settings > MQTT...`).

## Pestaña Broker

Configure los parámetros de conexión al broker.

1. En el campo **Host**, introduzca el nombre de host o la dirección IP del broker (valor predeterminado `localhost`).
2. En el campo **Port**, introduzca el puerto TCP del broker (valor predeterminado `1883`, rango 1–65535). El puerto cambia automáticamente entre 1883 y 8883 al alternar TLS.
3. Opcionalmente, introduzca un nombre de **User** para la autenticación en el broker.
4. Opcionalmente, introduzca una **Password** (enmascarada). La contraseña se almacena en el llavero del sistema. Si no hay llavero disponible, la contraseña se conserva solo en memoria durante la sesión actual y debe volver a introducirse en el siguiente inicio. Nunca se escribe en texto plano en el almacén de ajustes.
5. Marque **Use TLS** para habilitar el cifrado TLS. Esto cambia automáticamente el puerto entre 1883 y 8883.
6. Si TLS está habilitado, puede especificar opcionalmente una ruta de **CA cert**. Déjelo en blanco para usar el paquete de CA del sistema. Haga clic en **Browse...** para seleccionar un archivo.
7. Haga clic en **Apply** para guardar los ajustes sin cerrar, o en **Ok** para guardar y cerrar.

### Controles del broker

| Control | Descripción | Valor predeterminado | Clave de ajuste |
|---|---|---|---|
| **Host** | Nombre de host o dirección IP del broker. | `localhost` | `MqttHost` |
| **Port** | Puerto TCP del broker (1–65535). Cambia automáticamente entre 1883 y 8883 al alternar TLS. | `1883` | `MqttPort` |
| **User** | Nombre de usuario del broker (opcional). | en blanco | `MqttUser` |
| **Password** | Contraseña del broker (opcional, enmascarada). Se almacena en el llavero del sistema con migración de una sola vez desde los ajustes heredados en texto plano. Si el llavero no está disponible, se recurre a almacenamiento solo en memoria durante la sesión. | en blanco | — |
| **Use TLS** | Casilla que habilita el cifrado TLS. Cambia automáticamente el puerto entre 1883 y 8883. Muestra u oculta la fila de CA cert. | sin marcar | `MqttTls` |
| **CA cert** | Ruta a un archivo de certificado de CA. En blanco significa usar el paquete de CA del sistema. Solo visible cuando TLS está marcado. | en blanco | `MqttCaFile` |

## Pestaña Subscriptions

Gestione los temas suscritos.

1. En la pestaña **Subscriptions**, la tabla muestra los temas suscritos. Cada fila tiene:
   - **Topic**: cadena de tema de suscripción editable.
   - **Display**: casilla que controla si el tema aparece en la superposición del panadapter.
2. Haga clic en **Add** para añadir una nueva fila, o en **Remove** para eliminar la fila seleccionada.
3. El grupo **Internal AetherSDR Topics** muestra los temas suscritos automáticamente cuando MQTT se conecta. Estos temas no se pueden eliminar:

| Tema | Descripción | Admite activación | Activado por predeterminado |
|---|---|---|---|
| `aethersdr/antenna/alias/+` | Nombre de antena (por puerto) | No (siempre activo) | Activado |
| `aethersdr/antenna/alias` | Nombres de antena (masivo) | No (siempre activo) | Activado |
| `aethersdr/cw/transmit` | Entrada del manipulador CW | Sí | Activado |
| `aethersdr/ax25/tx` | Transmisión AX.25 | Sí | Activado |

Nota: La columna `defaultEnabled` muestra el estado inicial cuando se introdujo la activación por tema en la v26.6.3. Para los temas marcados como siempre activos (`Gateable = No`), la casilla aparece atenuada y no se puede cambiar.

## Pestaña Publish Buttons

Gestione hasta 12 botones de publicación.

1. En la pestaña **Publish Buttons**, la tabla muestra las definiciones de los botones. Cada fila tiene:
   - **Label**: texto de visualización del botón.
   - **Topic**: tema MQTT al que publicar.
   - **Payload**: texto de carga útil a publicar.
2. Haga clic en **Add** para añadir una nueva fila, o en **Remove** para eliminar la fila seleccionada. El botón **Add** está deshabilitado cuando hay 12 filas.
3. Las definiciones de los botones se comparten con el applet de MQTT.

## Solución de problemas

- **La conexión falla con "certificate verify failed"** — La ruta del archivo de certificado de CA es incorrecta o el certificado no coincide con el broker. Verifique la ruta del archivo y que el certificado sea la CA que firmó el certificado del broker.
- **La contraseña se pierde entre inicios** — Esto ocurre cuando el llavero del sistema no está disponible. La contraseña se mantiene en memoria solo durante la sesión actual y debe volver a introducirse en el siguiente inicio.
- **El tema de publicación o suscripción no funciona** — Verifique la pestaña **Subscriptions** para asegurarse de que el tema deseado esté presente y compruebe la casilla **Display** si espera salida en la superposición.

## Relacionado

- [Configurar la conexión al broker MQTT (host, puerto, credenciales, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [Descripción general de los ajustes de MQTT](overview.md)
