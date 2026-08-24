# Conectarse a un broker MQTT de la estación

Esta página explica cómo abrir el applet MQTT y conectar AetherSDR a un broker MQTT de la estación para poder suscribirse a tópicos, ver mensajes entrantes, publicar cargas útiles predefinidas y supervisar las confirmaciones de publicación de mensajes.

## Antes de comenzar

- Su broker MQTT está en funcionamiento y es accesible desde el equipo que ejecuta AetherSDR.
- Usted conoce el nombre de host o la dirección IP del broker, el puerto y las credenciales (si las hay).
- AetherSDR fue compilado con soporte MQTT (`HAVE_MQTT`). Si el botón de bandeja MQTT no está presente, su compilación no incluye esta función.

## Pasos

1. Si el panel de applets no está visible, haga clic en `View > Applet Panel` para mostrarlo.
2. Haga clic en el botón de bandeja **MQTT** en la barra lateral derecha. Se abre el applet MQTT.
3. Haga clic en **Settings...** en el encabezado del applet MQTT. Se abre el diálogo MQTT Settings.
4. En la pestaña **Connection**, introduzca el nombre de host o la dirección IP del broker en el campo **Host**. El valor predeterminado es `localhost`.
5. En el campo **Port**, introduzca el puerto TCP del broker. El valor predeterminado es `1883`. Rango válido: 1–65535.
6. Si el broker requiere autenticación, introduzca sus credenciales en los campos **User** y **Pass**. Ambos son opcionales y pueden dejarse en blanco. La contraseña se almacena en el llavero del sistema.
7. En el campo **Topics**, introduzca una lista separada por comas de tópicos a los que suscribirse. Déjelo en blanco si solo necesita publicar. Para superponer también el valor de un tópico en el panadapter, prefíjelo con `*`. Ejemplo:
   ```
   *rotator/pos, *ant/selected, station/log
   ```
8. Si el broker requiere TLS, marque la casilla **TLS**. El campo de puerto cambia automáticamente de `1883` a `8883`. Si necesita un certificado CA personalizado, introduzca la ruta del archivo en el campo **CA cert** que aparece. Deje **CA cert** en blanco para usar el paquete CA del sistema.
9. Configure los botones de publicación en la pestaña **Publish Buttons** si lo desea.
10. Haga clic en **OK** para guardar la configuración y cerrar el diálogo.
11. Haga clic en **Enable** (que actualmente muestra "Off") para conectarse. La etiqueta del botón cambia a "On" y la configuración se guarda.
12. Observe la etiqueta de estado a la derecha del botón. Muestra "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Control             | Descripción                                                                                                                                             | Valor predeterminado                                                        |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Settings...**     | Abre el diálogo MQTT Settings (MqttSettingsDialog) para la configuración de la conexión al broker, suscripciones y botones de publicación.               | Nuevo en v26.5.3. Reemplaza los campos en línea Host/Port/User/Pass/TLS/Topics. |
| **Publish buttons** | Hasta 12 botones configurables; al hacer clic se publica la carga útil configurada en el tópico configurado.                                            | Configurados mediante la pestaña Publish Buttons del MqttSettingsDialog.   |
| **Message log**     | Muestra los mensajes recibidos como líneas `topic: value` y los mensajes publicados como líneas `TX topic: payload`. También procesa actualizaciones de alias de antena desde MQTT. | Limitado a 50 entradas.                                                    |
| **Enable**          | Conecta (On) o desconecta (Off); guarda toda la configuración al conectar. La contraseña se carga del llavero del sistema en el primer enable.           | Off                                                                        |
| **Status label**    | Muestra el estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, predeterminado en caso de error.                | Disconnected                                                               |

## Consejos

- La configuración se guarda en almacenamiento persistente solo cuando hace clic en **OK** en el diálogo MQTT Settings, no cuando hace clic en **Enable** para conectarse.
- El campo **CA cert** y su etiqueta están ocultos cuando **TLS** no está marcado. Marque **TLS** primero para que aparezca la fila.
- El **Message log** conserva los últimos 50 bloques de mensajes. Las entradas más antiguas se eliminan automáticamente. Tanto los mensajes recibidos como los publicados aparecen en el registro. Los mensajes publicados llevan el prefijo `TX` (por ejemplo, `TX topic: payload`).
- Los botones de publicación solo están activos mientras está conectado. Consulte [Add or remove custom publish buttons](../../features/mqtt/add-or-remove-custom-publish-buttons.md) para configurarlos.
- Si la contraseña del llavero del sistema aún no se ha cargado, la etiqueta de estado muestra "Waiting for keychain" hasta que se recupere la contraseña.
- Las contraseñas transferidas a AetherSDR mediante importación XML se mantienen en una bóveda de sesión en el primer uso. Si la contraseña aún no se ha escrito en el llavero, la credencial de sesión evita que la contraseña se almacene en texto plano en la configuración de la aplicación. En sistemas sin soporte de llavero, la contraseña se mantiene solo durante la sesión actual y nunca se persiste.

## Solución de problemas

- **La etiqueta de estado muestra un mensaje de error en lugar de "Connected"** — El broker rechazó la conexión o no es accesible. Verifique el **Host**, el **Port** y las credenciales. Si TLS está habilitado, confirme que el broker está escuchando en el puerto `8883` y que la ruta del certificado CA es correcta.
- **La etiqueta de estado muestra "Waiting for keychain"** — La contraseña aún no se ha cargado del llavero del sistema. Haga clic en **Enable** de nuevo o reinicie el applet.
- **El botón de bandeja MQTT está ausente** — AetherSDR fue compilado sin soporte MQTT. Necesita una compilación con la marca `HAVE_MQTT`.
- **El puerto no cambió al marcar TLS** — El cambio automático solo se activa si el valor actual del puerto es exactamente `1883` (cambiando a `8883`) o `8883` (cambiando a `1883`). Si había introducido un puerto personalizado, este no se modifica.
- **El campo Topics acepta entrada pero no aparecen mensajes** — Confirme que el broker está publicando en las cadenas de tópicos exactas introducidas. La coincidencia de tópicos MQTT distingue entre mayúsculas y minúsculas.

## Relacionado

- [MQTT overview](../../features/mqtt/overview.md)
- [Subscribe to rotator / antenna switch topics](../../features/mqtt/subscribe-to-rotator-antenna-switch-topics.md)
- [Overlay an MQTT value on the panadapter (prefix topic with *)](../../features/mqtt/overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publish a canned message with a button (e.g. rotator preset)](../../features/mqtt/publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Add or remove custom publish buttons](../../features/mqtt/add-or-remove-custom-publish-buttons.md)
- [Enable TLS with a custom CA certificate](../../features/mqtt/enable-tls-with-a-custom-ca-certificate.md)
