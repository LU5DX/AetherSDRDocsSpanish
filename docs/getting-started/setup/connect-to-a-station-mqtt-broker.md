# Conectarse a un broker MQTT de estación

Esta página explica cómo abrir el applet de MQTT y conectar AetherSDR a un broker MQTT de estación para suscribirse a topics, ver los mensajes entrantes y publicar payloads predefinidos.

## Antes de comenzar

- El broker MQTT está en ejecución y es accesible desde la máquina donde corre AetherSDR.
- Conoce el nombre de host o la dirección IP del broker, el puerto y las credenciales (si las hay).
- AetherSDR fue compilado con soporte para MQTT (`HAVE_MQTT`). Si el botón de bandeja de MQTT no aparece, su compilación no incluye esta función.

## Pasos

1. Si el panel de applets no es visible, haga clic en `View > Applet Panel` para mostrarlo.
2. Haga clic en el botón de bandeja **MQTT** en la barra lateral derecha. El applet de MQTT se abre.
3. En el campo **Host**, ingrese el nombre de host o la dirección IP del broker. El valor predeterminado es `localhost`.
4. En el campo **Port**, ingrese el puerto TCP del broker. El valor predeterminado es `1883`. Rango válido: 1–65535.
5. Si el broker requiere autenticación, ingrese sus credenciales en los campos **User** y **Pass**. Ambos son opcionales y pueden dejarse en blanco.
6. En el campo **Topics**, ingrese una lista de topics separados por comas a los que suscribirse. Déjelo en blanco si solo necesita publicar. Para superponer también el valor de un topic en el panadapter (visor panorámico de espectro), antepóngale `*`. Ejemplo:
   ```
   *rotator/pos, *ant/selected, station/log
   ```
7. Si el broker requiere TLS, marque la casilla **TLS**. El campo de puerto cambia automáticamente de `1883` a `8883`. Si necesita un certificado CA personalizado, ingrese la ruta del archivo en el campo **CA cert** que aparece. Deje **CA cert** en blanco para usar el paquete de CA del sistema.
8. Haga clic en **Enable** (que actualmente muestra "Off") para conectarse. La etiqueta del botón cambia a "On" y todos los ajustes se guardan.
9. Observe la etiqueta de estado a la derecha del botón. Muestra "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Host** | Nombre de host o dirección IP del broker | `localhost` | Cualquier nombre de host o IP válido | `MqttHost` |
| **Port** | Puerto TCP del broker | `1883` | 1–65535 | `MqttPort` |
| **User** | Nombre de usuario del broker (opcional) | _(en blanco)_ | — | `MqttUser` |
| **Pass** | Contraseña del broker (opcional, enmascarada) | _(en blanco)_ | — | `MqttPass` |
| **Topics** | Lista de suscripciones separadas por comas; anteponga `*` para superponer en el panadapter | _(en blanco)_ | — | `MqttTopics` |
| **TLS** | Activa el cifrado TLS; cambia automáticamente el puerto entre `1883` y `8883`; muestra u oculta la fila **CA cert** | Off | On / Off | `MqttTls` |
| **CA cert** | Ruta al archivo de certificado CA; si se deja en blanco, se usa el paquete CA del sistema. Solo visible cuando TLS está marcado. | _(en blanco)_ | — | `MqttCaFile` |
| **Enable** | Conecta (On) o desconecta (Off); guarda todos los ajustes al conectar | Off | Off / On | — |
| **Message log** | Muestra los mensajes recibidos como líneas `topic: value` | — | Últimas 50 entradas | — |

## Consejos

- Los ajustes se guardan en almacenamiento persistente únicamente cuando se hace clic en **Enable** para conectar, no al escribirlos. Si edita los campos y cierra el applet sin conectarse, los cambios se perderán.
- El campo **CA cert** y su etiqueta están ocultos cuando **TLS** no está marcado. Marque **TLS** primero para que aparezca la fila.
- El **Message log** conserva los últimos 50 bloques de mensajes. Las entradas más antiguas se eliminan automáticamente.
- Los botones de publicación solo están activos mientras se está conectado. Consulte [Agregar o eliminar botones de publicación personalizados](../../features/mqtt/add-or-remove-custom-publish-buttons.md) para configurarlos.

## Solución de problemas

- **La etiqueta de estado muestra un mensaje de error en lugar de "Connected"** — El broker rechazó la conexión o no es accesible. Verifique el **Host**, el **Port** y las credenciales. Si TLS está activado, confirme que el broker está escuchando en el puerto `8883` y que la ruta del certificado CA es correcta.
- **El botón de bandeja de MQTT no aparece** — AetherSDR fue compilado sin soporte para MQTT. Se necesita una compilación con el indicador `HAVE_MQTT`.
- **El puerto no cambió al marcar TLS** — El cambio automático solo se activa si el valor actual del puerto es exactamente `1883` (cambia a `8883`) o `8883` (cambia a `1883`). Si había ingresado un puerto personalizado, este no se modifica.
- **El campo Topics acepta la entrada pero no aparecen mensajes** — Confirme que el broker está publicando en las cadenas de topics exactas ingresadas. La coincidencia de topics en MQTT distingue entre mayúsculas y minúsculas.

## Relacionados

- [Descripción general de MQTT](../../features/mqtt/overview.md)
- [Suscribirse a topics de rotator / conmutador de antena](../../features/mqtt/subscribe-to-rotator-antenna-switch-topics.md)
- [Superponer un valor MQTT en el panadapter (anteponer * al topic)](../../features/mqtt/overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publicar un mensaje predefinido con un botón (p. ej., preset de rotator)](../../features/mqtt/publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Agregar o eliminar botones de publicación personalizados](../../features/mqtt/add-or-remove-custom-publish-buttons.md)
- [Activar TLS con un certificado CA personalizado](../../features/mqtt/enable-tls-with-a-custom-ca-certificate.md)
