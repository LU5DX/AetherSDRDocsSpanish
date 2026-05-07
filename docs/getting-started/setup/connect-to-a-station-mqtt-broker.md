# Conectarse a un broker MQTT de estación

Esta página explica cómo abrir el applet MQTT y conectar AetherSDR a un broker MQTT de estación para suscribirse a tópicos, ver mensajes entrantes y publicar mensajes predefinidos.

## Antes de empezar

- Su broker MQTT está en ejecución y es accesible desde la máquina donde se ejecuta AetherSDR.
- Conoce el nombre de host o dirección IP del broker, el puerto y las credenciales (si las hay).
- AetherSDR fue compilado con soporte MQTT (`HAVE_MQTT`). Si el botón de la bandeja MQTT no está presente, su compilación no incluye esta funcionalidad.

## Pasos

1. Si el panel de applets no está visible, haga clic en `View > Applet Panel` para mostrarlo.
2. Haga clic en el botón **MQTT** de la bandeja en la barra lateral derecha. Se abre el applet MQTT.
3. En el campo **Host**, ingrese el nombre de host o dirección IP del broker. El valor predeterminado es `localhost`.
4. En el campo **Port**, ingrese el puerto TCP del broker. El valor predeterminado es `1883`. Rango válido: 1–65535.
5. Si el broker requiere autenticación, ingrese sus credenciales en los campos **User** y **Pass**. Ambos son opcionales y pueden dejarse en blanco.
6. En el campo **Topics**, ingrese una lista separada por comas de los tópicos a los que desea suscribirse. Déjelo en blanco si solo necesita publicar. Para superponer el valor de un tópico en el panadapter, prefíjelo con `*`. Ejemplo:
   ```
   *rotator/pos, *ant/selected, station/log
   ```
7. Si el broker requiere TLS, marque la casilla **TLS**. El campo de puerto cambia automáticamente de `1883` a `8883`. Si necesita un certificado CA personalizado, ingrese la ruta del archivo en el campo **CA cert** que aparece. Deje **CA cert** en blanco para usar el conjunto de CA del sistema.
8. Haga clic en **Enable** (actualmente muestra "Off") para conectar. El texto del botón cambia a "On" y todos los ajustes se guardan.
9. Observe la etiqueta de estado a la derecha del botón. Muestra "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Host** | Nombre de host o dirección IP del broker | `localhost` | Cualquier nombre de host o IP válido | `MqttHost` |
| **Port** | Puerto TCP del broker | `1883` | 1–65535 | `MqttPort` |
| **User** | Nombre de usuario del broker (opcional) | _(en blanco)_ | — | `MqttUser` |
| **Pass** | Contraseña del broker (opcional, enmascarada) | _(en blanco)_ | — | `MqttPass` |
| **Topics** | Lista de suscripción separada por comas; prefijar con `*` para superponer en el panadapter | _(en blanco)_ | — | `MqttTopics` |
| **TLS** | Habilita cifrado TLS; cambia automáticamente el puerto entre `1883` y `8883`; muestra/oculta la fila **CA cert** | Off | On / Off | `MqttTls` |
| **CA cert** | Ruta al archivo de certificado CA; en blanco usa el conjunto CA del sistema. Visible solo cuando TLS está marcado. | _(en blanco)_ | — | `MqttCaFile` |
| **Enable** | Conecta (On) o desconecta (Off); guarda todos los ajustes al conectar | Off | Off / On | — |
| **Message log** | Muestra los mensajes recibidos como líneas `topic: value` | — | Últimas 50 entradas | — |

## Consejos

- Los ajustes se guardan en almacenamiento persistente solo cuando hace clic en **Enable** para conectar, no cuando los escribe. Si edita los campos y cierra el applet sin conectar, los cambios se pierden.
- El campo **CA cert** y su etiqueta están ocultos cuando **TLS** no está marcado. Marque **TLS** primero para que aparezca la fila.
- El **Message log** conserva los últimos 50 bloques de mensajes. Las entradas más antiguas se eliminan automáticamente.
- Los botones de publicación solo están activos mientras está conectado. Consulte [Add or remove custom publish buttons](../../features/mqtt/add-or-remove-custom-publish-buttons.md) para configurarlos.

## Solución de problemas

- **La etiqueta de estado muestra un mensaje de error en lugar de "Connected"** — El broker rechazó la conexión o es inaccesible. Verifique el **Host**, **Port** y las credenciales. Si TLS está habilitado, confirme que el broker esté escuchando en el puerto `8883` y que la ruta del certificado CA sea correcta.
- **El botón de la bandeja MQTT no está presente** — AetherSDR fue compilado sin soporte MQTT. Necesita una compilación realizada con la bandera `HAVE_MQTT`.
- **El puerto no cambió al marcar TLS** — El cambio automático solo se activa si el valor actual del puerto es exactamente `1883` (cambiando a `8883`) o `8883` (cambiando a `1883`). Si había ingresado un puerto personalizado, este no se modifica.
- **El campo Topics acepta entrada pero no aparecen mensajes** — Confirme que el broker está publicando exactamente las cadenas de tópicos ingresadas. La coincidencia de tópicos MQTT distingue entre mayúsculas y minúsculas.

## Relacionados

- [MQTT overview](../../features/mqtt/overview.md)
- [Subscribe to rotator / antenna switch topics](../../features/mqtt/subscribe-to-rotator-antenna-switch-topics.md)
- [Overlay an MQTT value on the panadapter (prefix topic with *)](../../features/mqtt/overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publish a canned message with a button (e.g. rotator preset)](../../features/mqtt/publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Add or remove custom publish buttons](../../features/mqtt/add-or-remove-custom-publish-buttons.md)
- [Enable TLS with a custom CA certificate](../../features/mqtt/enable-tls-with-a-custom-ca-certificate.md)
