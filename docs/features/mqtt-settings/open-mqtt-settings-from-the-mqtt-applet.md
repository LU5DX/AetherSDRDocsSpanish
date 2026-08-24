# Configurar botones de publicación MQTT

## Pasos

1. En el diálogo de Configuración MQTT, haga clic en la pestaña **Publish Buttons**.

   La pestaña Publish Buttons muestra una tabla con las columnas **Label**, **Topic** y **Payload**.

2. Para agregar un botón:
   - Haga clic en **Add** para insertar una nueva fila vacía.
   - El botón Add está deshabilitado cuando existen 12 filas (máximo).
   - Ingrese un **Label** (texto del botón), un **Topic** (tema MQTT al que publicar) y un **Payload** (mensaje a enviar).

3. Para eliminar un botón:
   - Haga clic en la fila que desea eliminar.
   - Haga clic en **Remove**.

4. Haga clic en **Apply** para guardar sus definiciones de botones sin cerrar el diálogo, o haga clic en **OK** para guardar y cerrar.

## Pestaña Subscriptions

La pestaña **Subscriptions** contiene una tabla donde puede agregar y administrar suscripciones a temas MQTT:

- **Topic** (campo de texto editable): El tema MQTT al que suscribirse.
- **Display** (casilla de verificación): Cuando está marcada, habilita la visualización superpuesta del panadapter para ese tema.

Use los botones **Add** y **Remove** debajo de la tabla para administrar las suscripciones. El grupo **Internal AetherSDR Topics** muestra los temas que se suscriben automáticamente cuando MQTT se conecta y no pueden eliminarse.

## Qué muestra la sección Internal AetherSDR Topics

El grupo **Internal AetherSDR Topics** aparece tanto en la pestaña **Subscriptions** como en la pestaña **Publish Buttons**.

### En la pestaña Publish Buttons

El grupo **Internal AetherSDR Topics** lista los temas que AetherSDR publica automáticamente cuando MQTT está conectado. Cada tema tiene una casilla de verificación que le permite habilitarlo o deshabilitarlo individualmente. Los temas marcados como gateable (no atenuados) pueden alternarse; los temas no gateable están siempre activos y se muestran atenuados.

Los temas de publicación son:

| Tema | Descripción | Predeterminado | Gateable |
|------|-------------|----------------|----------|
| `aethersdr/cw/decode` | Texto decodificado de CW | On | Sí |
| `aethersdr/radio/state` | Estado de VFO / modo / TX de la radio | Off | Sí |
| `aethersdr/ax25/rx` | Tramas AX.25 recibidas | On | Sí |

### En la pestaña Subscriptions

Los temas de suscripción que se muestran en el grupo **Internal AetherSDR Topics** en la pestaña **Subscriptions** son:

| Tema | Descripción | Predeterminado | Gateable |
|------|-------------|----------------|----------|
| `aethersdr/antenna/alias/+` | Nombre de antena (por puerto) | On | No |
| `aethersdr/antenna/alias` | Nombres de antena (masivo) | On | No |
| `aethersdr/cw/transmit` | Entrada del keyer CW | Off | Sí |
| `aethersdr/ax25/tx` | Transmisión AX.25 | Off | Sí |

Cuando habilita o deshabilita un tema interno gateable, la configuración se almacena y tiene efecto la próxima vez que MQTT se conecte o reconecte.

## Número máximo de botones de publicación

Puede definir hasta **12 botones de publicación**. El botón Add está deshabilitado cuando existen 12 filas.

## Almacenamiento de contraseña

La contraseña MQTT se almacena en el llavero de su sistema. Si su sistema no admite almacenamiento en llavero, la contraseña se mantiene solo en memoria durante la sesión actual y debe volver a ingresarse la próxima vez que inicie AetherSDR. Una contraseña heredada en texto plano (de una versión anterior) se migra al llavero la primera vez que se utiliza y luego se elimina del almacén de configuración.

## Relacionado

- [Resumen de configuración MQTT](overview.md)
- [Configurar la conexión al broker MQTT (host, puerto, credenciales, TLS)](../../getting-started/setup/configure-mqtt-broker-connection-host-port-credentials-tls.md)
- [Suscribirse a temas MQTT y alternar la visualización del panadapter](../mqtt/subscribe-to-mqtt-topics-and-toggle-panadapter-display.md)
- [Configurar certificado CA para MQTT TLS](configure-ca-certificate-for-tls-mqtt.md)
