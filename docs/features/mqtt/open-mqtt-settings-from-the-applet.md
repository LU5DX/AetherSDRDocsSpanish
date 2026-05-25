# Abrir los ajustes MQTT desde el applet

Abra el diálogo de Ajustes MQTT desde el applet MQTT para configurar la conexión al broker, las suscripciones y los ajustes de los botones de publicación.

## Antes de empezar

- El applet MQTT debe estar visible. Actívelo con el botón MQTT en la bandeja de la barra lateral derecha.
- La funcionalidad MQTT debe estar compilada (requiere la puerta de compilación `HAVE_MQTT`).

## Pasos

1. En el encabezado del applet MQTT, haga clic en **Settings...**.
2. Se abre el diálogo de Ajustes MQTT.

## Función de cada control

| Control | Comportamiento |
|---|---|
| Botón **Settings...** | Abre el diálogo de Ajustes MQTT (`MqttSettingsDialog`) para la conexión al broker, las suscripciones y la configuración de los botones de publicación. |

## Relacionado

- [Configurar los ajustes de conexión al broker (host, puerto, credenciales, TLS)](../../getting-started/setup/configure-broker-connection-settings-host-port-credentials-tls.md)
- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Habilitar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
- [Añadir o eliminar botones de publicación personalizados](add-or-remove-custom-publish-buttons.md)
- [Suscribirse a temas MQTT y alternar la visualización del panadapter](subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Superponer un valor MQTT en el panadapter](overlay-an-mqtt-value-on-the-panadapter.md)
- [Publicar un mensaje predefinido con un botón (p. ej., preajuste de rotor)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
