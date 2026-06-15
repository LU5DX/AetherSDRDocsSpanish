# Configurar botones de publicación MQTT

## Pasos

1. En el cuadro de diálogo Configuración MQTT, haga clic en la pestaña **Publish Buttons**.

   La pestaña Publish Buttons muestra una tabla con las columnas **Label**, **Topic** y **Payload**, además de un cuadro de grupo de solo lectura **Internal AetherSDR Topics**.

2. Para añadir un botón:
   - Haga clic en **Add** para insertar una nueva fila en blanco.
   - El botón Add se deshabilita cuando existen 12 filas (máximo).
   - Ingrese una **Label** (texto del botón), **Topic** (tema MQTT para publicar) y **Payload** (mensaje a enviar).

3. Para eliminar un botón:
   - Haga clic en la fila que desea eliminar.
   - Haga clic en **Remove**.

4. Haga clic en **Apply** para guardar las definiciones de los botones sin cerrar el diálogo, o haga clic en **OK** para guardar y cerrar.

## Qué muestra la sección Internal AetherSDR Topics

El cuadro de grupo **Internal AetherSDR Topics** lista los temas que AetherSDR publica automáticamente siempre que MQTT esté conectado. Cada tema tiene una casilla de verificación que permite habilitarlo o deshabilitarlo individualmente. Los temas marcados como gateables (no atenuados) se pueden alternar; los temas no gateables siempre están activos y se muestran atenuados.

Los temas de publicación son:

| Topic | Descripción | Predeterminado | Gateable |
|-------|-------------|----------------|----------|
| `aethersdr/cw/decode` | Texto decodificado de CW | On | Sí |
| `aethersdr/radio/state` | Estado VFO/modo/TX de la radio | Off | Sí |
| `aethersdr/ax25/rx` | Tramas AX.25 recibidas | On | Sí |

Los temas de suscripción que se muestran en el cuadro de grupo **Internal AetherSDR Topics** en la pestaña **Subscriptions** son:

| Topic | Descripción | Predeterminado | Gateable |
|-------|-------------|----------------|----------|
| `aethersdr/antenna/alias/+` | Nombre de antena (por puerto) | On | No |
| `aethersdr/antenna/alias` | Nombres de antena (masivo) | On | No |
| `aethersdr/cw/transmit` | Entrada del manipulador CW | Off | Sí |
| `aethersdr/ax25/tx` | Transmisión AX.25 | Off | Sí |

Cuando habilita o deshabilita un tema interno gateable, la configuración se almacena y surte efecto la próxima vez que MQTT se conecte o reconecte.

## Número máximo de botones de publicación

Puede definir hasta **12 botones de publicación**. El botón Add está deshabilitado cuando existen 12 filas.

## Relacionado

- [Resumen de configuración MQTT](overview.md)
- [Configurar la conexión del broker MQTT (host, puerto, credenciales, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [Suscribirse a temas MQTT y alternar visualización del panadapter](../mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Configurar certificado CA para MQTT TLS](configure-ca-certificate-for-tls-mqtt.md)
