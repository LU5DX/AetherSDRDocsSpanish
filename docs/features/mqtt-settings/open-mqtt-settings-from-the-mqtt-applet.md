# Configurar Botones de Publicación MQTT

## Pasos

1. En el cuadro de diálogo Configuración MQTT, haga clic en la pestaña **Publish Buttons**.

   La pestaña Publish Buttons muestra una tabla con las columnas **Label**, **Topic** y **Payload**, además de un cuadro de grupo de solo lectura **Internal AetherSDR Topics**.

2. Para agregar un botón:
   - Haga clic en **Add** para insertar una nueva fila en blanco.
   - El botón Add está deshabilitado cuando existen 12 filas (máximo).
   - Ingrese una **Label** (texto del botón), **Topic** (tema MQTT para publicar) y **Payload** (mensaje a enviar).

3. Para eliminar un botón:
   - Haga clic en la fila que desea eliminar.
   - Haga clic en **Remove**.

4. Haga clic en **Apply** para guardar las definiciones de sus botones sin cerrar el diálogo, o haga clic en **OK** para guardar y cerrar.

## Qué muestra la sección Internal AetherSDR Topics

El cuadro de grupo **Internal AetherSDR Topics** enumera los temas que AetherSDR publica automáticamente cada vez que MQTT está conectado:

- `aethersdr/cw/decode`

Estos temas no son configurables por el usuario y no pueden eliminarse. Aparecen automáticamente en el broker cuando la característica correspondiente está activa.

## Número máximo de botones de publicación

Puede definir hasta **12 botones de publicación**. El botón Add está deshabilitado cuando existen 12 filas.

## Relacionado

- [Resumen de Configuración MQTT](overview.md)
- [Configurar la conexión del broker MQTT (host, puerto, credenciales, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [Suscribirse a temas MQTT y alternar visualización del panadapter](../mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Configurar certificado CA para MQTT TLS](configure-ca-certificate-for-tls-mqtt.md)
