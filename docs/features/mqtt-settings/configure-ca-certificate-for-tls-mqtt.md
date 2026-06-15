# Configurar el certificado CA para TLS MQTT

Proporcione un archivo de certificado CA personalizado al conectarse a un broker MQTT que utilice una Autoridad de Certificación autofirmada o privada. Cuando no se especifica un archivo de certificado CA, AetherSDR utiliza el paquete CA del sistema.

## Antes de comenzar

- Tiene un archivo de certificado CA en formato PEM en su sistema de archivos local.
- El cuadro de diálogo de Configuración MQTT está abierto (`Settings > MQTT...`).

## Pasos

1. En la pestaña **Broker**, marque **Use TLS**.
2. En el campo **CA cert**, ingrese la ruta completa del sistema de archivos a su archivo de certificado CA, o haga clic en **Browse...** para seleccionarlo.
3. Haga clic en **Apply** para guardar sin cerrar, o en **Ok** para guardar y cerrar.

## Función de cada control

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Use TLS** | Casilla de verificación que habilita el cifrado TLS. Al marcarla, cambia automáticamente el puerto de 1883 a 8883 (y viceversa al desmarcarla). | Sin marcar | `MqttTls` |
| **CA cert** | Campo de texto para la ruta del archivo de certificado CA. Visible solo cuando **Use TLS** está marcado. Déjelo en blanco para usar el paquete CA del sistema. El botón **Browse...** abre un cuadro de diálogo de selección de archivos. | En blanco | `MqttCaFile` |

## Pestaña Publish Buttons

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Internal AetherSDR Topics** | Grupo de solo lectura queenumera los temas publicados automáticamente cuando MQTT está conectado. Cada tema se puede activar o desactivar mediante una casilla de verificación. Los temas con una casilla atenuada están siempre activos y no se pueden deshabilitar. | Ver tabla a continuación | — |

### Temas de publicación internos

| Tema | Descripción | Bloqueable | Activado por defecto |
|---|---|---|---|
| `aethersdr/cw/decode` | Texto decodificado de CW | Sí | Activado |
| `aethersdr/radio/state` | Estado de VFO / modo / TX de la radio | Sí | Desactivado |
| `aethersdr/ax25/rx` | Tramas AX.25 recibidas | Sí | Desactivado |

## Pestaña Subscriptions

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Internal AetherSDR Topics** | Grupo de solo lectura que enumera los temas a los que se suscribe automáticamente cuando MQTT se conecta. Cada tema se puede activar o desactivar mediante una casilla de verificación. Los temas con una casilla atenuada están siempre activos y no se pueden deshabilitar. | Ver tabla a continuación | `mqtt_internal_<sanitized_topic>` |

### Temas de suscripción internos

| Tema | Descripción | Bloqueable | Activado por defecto |
|---|---|---|---|
| `aethersdr/antenna/alias/+` | Nombre de antena (por puerto) | No (siempre activo) | Activado |
| `aethersdr/antenna/alias` | Nombres de antena (masivos) | No (siempre activo) | Activado |
| `aethersdr/cw/transmit` | Entrada del manipulador CW | Sí | Activado |
| `aethersdr/ax25/tx` | Transmisión AX.25 | Sí | Activado |

Nota: La columna `defaultEnabled` muestra el estado inicial cuando se introdujo el bloqueo por tema en la versión v26.6.3. Para los temas listados como siempre activos (`Gateable = No`), la casilla de verificación está atenuada y no se puede modificar.

## Solución de problemas

- **La conexión falla con "certificate verify failed"** — La ruta del archivo de certificado CA es incorrecta o el certificado no coincide con el broker. Verifique la ruta del archivo y que el certificado sea la CA que firmó el certificado del broker.
- **El tema de publicación o suscripción no funciona** — Verifique la sección **Internal AetherSDR Topics** para asegurarse de que el tema deseado esté habilitado (casilla marcada). Los temas se pueden deshabilitar individualmente para reducir el tráfico de red.

## Relacionado

- [Configure MQTT broker connection (host, port, credentials, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [MQTT Settings overview](overview.md)
