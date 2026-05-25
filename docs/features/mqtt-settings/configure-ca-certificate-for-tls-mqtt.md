# Configurar certificado CA para TLS MQTT

Proporcione un archivo de certificado CA personalizado al conectarse a un broker MQTT que utiliza una Autoridad Certificadora (CA) autofirmada o privada. Cuando no se especifica ningún archivo de certificado CA, AetherSDR utiliza el paquete de CA del sistema.

## Antes de comenzar

- Tiene un archivo de certificado CA en formato PEM en su sistema de archivos local.
- El cuadro de diálogo MQTT Settings está abierto (`Settings > MQTT...`).

## Pasos

1. En la pestaña **Broker**, marque **Use TLS**.
2. En el campo **CA cert**, ingrese la ruta completa del sistema de archivos a su archivo de certificado CA, o haga clic en **Browse...** para seleccionarlo.
3. Haga clic en **Apply** para guardar sin cerrar, o en **Ok** para guardar y cerrar.

## Función de cada control

| Control | Descripción | Valor predeterminado | Clave de configuración |
|---|---|---|---|
| **Use TLS** | Casilla de verificación que habilita el cifrado TLS. Al marcarla, cambia automáticamente el puerto de 1883 a 8883 (y viceversa al desmarcarla). | sin marcar | `MqttTls` |
| **CA cert** | Campo de texto para la ruta del archivo de certificado CA. Visible solo cuando **Use TLS** está marcado. Déjelo en blanco para usar el paquete de CA del sistema. El botón **Browse...** abre un cuadro de diálogo de selección de archivos. | en blanco | `MqttCaFile` |

## Solución de problemas

- **La conexión falla con "certificate verify failed"** — La ruta del archivo de certificado CA es incorrecta o el certificado no coincide con el broker. Verifique la ruta del archivo y que el certificado sea la CA que firmó el certificado del broker.

## Relacionado

- [Configure MQTT broker connection (host, port, credentials, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [MQTT Settings overview](overview.md)
