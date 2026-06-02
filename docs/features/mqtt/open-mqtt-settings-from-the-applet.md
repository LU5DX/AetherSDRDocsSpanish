# Abrir los ajustes MQTT desde el applet

Abra el diálogo de Ajustes MQTT desde el applet MQTT para configurar la conexión al broker, las suscripciones y los botones de publicación.

## Antes de comenzar

- El applet MQTT debe estar visible. Actívelo con el botón de la bandeja MQTT en la barra lateral derecha.
- La función MQTT debe estar compilada (requiere la compuerta de compilación `HAVE_MQTT`).

## Pasos

1. En el encabezado del applet MQTT, haga clic en **Settings...**.
2. Se abre el diálogo de Ajustes MQTT.

## Función de cada control

| Control               | Comportamiento                                                                                                                   | Notas                                                                     |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Botón **Settings...** | Abre el diálogo de Ajustes MQTT (`MqttSettingsDialog`) para la conexión al broker, suscripciones y configuración de botones de publicación. | Nuevo en v26.5.3. Sustituye los campos en línea de Host/Puerto/Usuario/Contraseña/TLS/Temas. |
| **Enable (Off/On)**   | Botón de alternancia que conecta o desconecta del broker usando los ajustes de MqttSettings. Emite connectRequested / disconnectRequested y guarda el estado de conexión habilitada. | La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no está cargada, muestra el estado 'Waiting for keychain'. |
| **Botones de publicación** | Hasta 12 botones. Al hacer clic, publica la carga útil configurada en el tema configurado mediante MqttClient::publish.         | Solo activos mientras está conectado. Se configuran en la pestaña Publish Buttons del diálogo MqttSettingsDialog. Clave de ajuste: `MqttButtons`. |
| **Registro de mensajes** | Muestra los mensajes recibidos como líneas "tema: valor". También procesa actualizaciones de alias de antena desde MQTT.        | Limitado a 50 entradas.                                                     |

## Indicadores

| Indicador           | Estados                                                                    | Significado                                                          |
|----------------------|----------------------------------------------------------------------------|----------------------------------------------------------------------|
| **Etiqueta de estado** | "Disconnected" (gris), "Connected" (verde) o un mensaje de error (color predeterminado) | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, color predeterminado en caso de error. |

## Relacionado

- [Configure broker connection settings (host, port, credentials, TLS)](../../getting-started/setup/configure-broker-connection-settings-host-port-credentials-tls.md)
- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Enable TLS with a custom CA certificate](enable-tls-with-a-custom-ca-certificate.md)
- [Add or remove custom publish buttons](add-or-remove-custom-publish-buttons.md)
- [Subscribe to MQTT topics and toggle panadapter display](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Overlay an MQTT value on the panadapter](overlay-an-mqtt-value-on-the-panadapter.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
