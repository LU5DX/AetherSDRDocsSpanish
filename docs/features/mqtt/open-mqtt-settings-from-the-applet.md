# Applet MQTT

El applet MQTT integra AetherSDR con un broker MQTT de la estación: publique mensajes predefinidos con botones editables por el usuario, supervise los mensajes entrantes y superponga valores de temas en el panadapter.

## Abrir la configuración MQTT desde el applet

Abra el diálogo de Configuración MQTT desde el applet MQTT para configurar la conexión al broker, las suscripciones y los botones de publicación.

### Antes de comenzar

- El applet MQTT debe estar visible. Actívelo con el botón MQTT en la bandeja de la barra lateral derecha.
- La funcionalidad MQTT debe estar compilada (requiere la compilación `HAVE_MQTT`).

### Pasos

1. En el encabezado del applet MQTT, haga clic en **Settings...**.
2. Se abre el diálogo de Configuración MQTT.

## Qué hace cada control

| Control                | Comportamiento                                                                                                                                                                 | Notas                                                                                                                                 |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| Botón **Settings...** | Abre el diálogo de Configuración MQTT (`MqttSettingsDialog`) para la conexión al broker, suscripciones y configuración de botones de publicación.                                                 | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Puerto/Usuario/Contraseña/TLS/Temas.                                          |
| **Enable (Off/On)**    | Botón de alternancia que conecta o desconecta del broker usando la configuración de MqttSettings. Emite connectRequested/disconnectRequested y guarda el estado de conexión habilitada. | La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no está cargada, muestra el estado "Waiting for keychain". |
| **Botones de publicación**    | Hasta 12 botones pulsadores. Al hacer clic, publica la carga útil configurada en el tema configurado a través de MqttClient::publish.                                                                | Solo están activos mientras está conectado. Se configuran a través de la pestaña Publish Buttons del diálogo MqttSettingsDialog. Clave de ajuste: `MqttButtons`.                       |
| **Registro de mensajes**        | Muestra los mensajes recibidos como líneas "tema: valor" y los mensajes transmitidos como líneas "TX tema: valor". También procesa actualizaciones de alias de antena desde MQTT.                       | Limitado a 50 entradas. |

### Indicadores

| Indicador        | Estados                                                                 | Significado                                                          |
|-------------------|------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Etiqueta de estado** | "Disconnected" (gris), "Connected" (verde) o un mensaje de error (color predeterminado) | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, predeterminado en caso de error. |

## Detalles del registro de mensajes

El registro de mensajes muestra tanto los mensajes recibidos como los transmitidos:

- **Mensajes recibidos** aparecen como líneas `tema: valor`. Por ejemplo: `ant/A: 1`
- **Mensajes transmitidos** aparecen como líneas `TX tema: valor`. Por ejemplo: `TX rotator/preset: QTH`

El tema mostrado es el último segmento de la ruta completa del tema. Por ejemplo, si el tema completo es `flexradio/6804/ant/A`, el registro muestra solo `ant/A`.

El registro está limitado a las 50 entradas más recientes.

## Relacionado

- [Configure broker connection settings (host, port, credentials, TLS)](../../getting-started/setup/configure-broker-connection-settings-host-port-credentials-tls.md)
- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Enable TLS with a custom CA certificate](enable-tls-with-a-custom-ca-certificate.md)
- [Add or remove custom publish buttons](add-or-remove-custom-publish-buttons.md)
- [Subscribe to MQTT topics and toggle panadapter display](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Overlay an MQTT value on the panadapter](overlay-an-mqtt-value-on-the-panadapter.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
