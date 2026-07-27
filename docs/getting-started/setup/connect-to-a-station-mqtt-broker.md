# Conectarse a un broker MQTT de estación

Esta página explica cómo abrir el applet MQTT y conectar AetherSDR a un broker MQTT de estación para suscribirse a temas, ver mensajes entrantes, publicar cargas útiles predefinidas y monitorear las confirmaciones de publicación de mensajes.

## Antes de comenzar

- Su broker MQTT está en ejecución y accesible desde la máquina donde se ejecuta AetherSDR.
- Conoce el nombre de host o dirección IP del broker, el puerto y las credenciales (si las hay).
- AetherSDR se compiló con soporte MQTT (`HAVE_MQTT`). Si el botón de la bandeja MQTT no está presente, su compilación no incluye esta funcionalidad.

## Pasos

1. Si el panel de applets no está visible, haga clic en `View > Applet Panel` para mostrarlo.
2. Haga clic en el botón de bandeja **MQTT** en la barra lateral derecha. Se abre el applet MQTT.
3. Haga clic en **Settings...** en el encabezado del applet MQTT. Se abre el diálogo de Configuración MQTT.
4. En la pestaña **Connection**, ingrese el nombre de host o dirección IP del broker en el campo **Host**. El valor predeterminado es `localhost`.
5. En el campo **Port**, ingrese el puerto TCP del broker. El valor predeterminado es `1883`. Rango válido: 1–65535.
6. Si el broker requiere autenticación, ingrese sus credenciales en los campos **User** y **Pass**. Ambos son opcionales y pueden dejarse en blanco. La contraseña se almacena en el llavero de claves del sistema.
7. En el campo **Topics**, ingrese una lista separada por comas de temas a los que suscribirse. Déjelo en blanco si solo necesita publicar. Para superponer el valor de un tema en el panadapter, prefíjelo con `*`. Ejemplo:
   ```
   *rotator/pos, *ant/selected, station/log
   ```
8. Si el broker requiere TLS, marque la casilla **TLS**. El campo de puerto cambia automáticamente de `1883` a `8883`. Si necesita un certificado CA personalizado, ingrese la ruta del archivo en el campo **CA cert** que aparece. Deje **CA cert** en blanco para usar el paquete CA del sistema.
9. Configure los botones de publicación en la pestaña **Publish Buttons** si lo desea.
10. Haga clic en **OK** para guardar la configuración y cerrar el diálogo.
11. Haga clic en **Enable** (que actualmente muestra "Off") para conectarse. La etiqueta del botón cambia a "On" y la configuración se guarda.
12. Observe la etiqueta de estado a la derecha del botón. Muestra "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Control             | Descripción                                                                                                                                                              | Valor predeterminado                                                |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|
| **Settings...**     | Abre el diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.                           | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Port/User/Pass/TLS/Topics. |
| **Publish buttons** | Hasta 12 botones configurables; al hacer clic se publica la carga útil configurada en el tema configurado.                                                               | Configurado mediante la pestaña Publish Buttons de MqttSettingsDialog. |
| **Message log**     | Muestra los mensajes recibidos como líneas `tema: valor` y los mensajes publicados como líneas `TX tema: carga_útil`. También procesa actualizaciones de alias de antena desde MQTT. | Limitado a 50 entradas.                                               |
| **Enable**          | Conecta (On) o desconecta (Off); guarda toda la configuración al conectar. La contraseña se carga desde el llavero de claves del sistema al habilitar por primera vez.     | Off                                                                   |
| **Status label**    | Muestra el estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, predeterminado en caso de error.                                 | Disconnected                                                          |
| Settings...         | Abre el diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación.                           | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Port/User/Pass/TLS/Topics. |

## Consejos

- La configuración se guarda en el almacenamiento persistente solo cuando hace clic en **OK** en el diálogo de Configuración MQTT, no cuando hace clic en **Enable** para conectarse.
- El campo **CA cert** y su etiqueta están ocultos cuando **TLS** no está marcado. Marque **TLS** primero para que aparezca la fila.
- El **Message log** conserva los últimos 50 bloques de mensajes. Las entradas más antiguas se eliminan automáticamente. Tanto los mensajes recibidos como los publicados aparecen en el registro. Los mensajes publicados tienen el prefijo `TX` (ej., `TX tema: carga_útil`).
- Los botones de publicación solo están activos mientras está conectado. Consulte [Añadir o eliminar botones de publicación personalizados](../../features/mqtt/add-or-remove-custom-publish-buttons.md) para configurarlos.
- Si la contraseña del llavero de claves del sistema aún no se ha cargado, la etiqueta de estado muestra "Waiting for keychain" hasta que se recupere la contraseña.

## Solución de problemas

- **La etiqueta de estado muestra un mensaje de error en lugar de "Connected"** — El broker rechazó la conexión o es inaccesible. Verifique el **Host**, el **Puerto** y las credenciales. Si TLS está habilitado, confirme que el broker esté escuchando en el puerto `8883` y que la ruta del certificado CA sea correcta.
- **La etiqueta de estado muestra "Waiting for keychain"** — La contraseña aún no se ha cargado desde el llavero de claves del sistema. Haga clic en **Enable** nuevamente o reinicie el applet.
- **El botón de bandeja MQTT está ausente** — AetherSDR se compiló sin soporte MQTT. Necesita una compilación realizada con la marca `HAVE_MQTT`.
- **El puerto no cambió cuando marqué TLS** — El cambio automático solo se activa si el valor actual del puerto es exactamente `1883` (cambia a `8883`) o `8883` (cambia a `1883`). Si ingresó un puerto personalizado, no se modifica.
- **El campo Topics acepta entrada pero no aparecen mensajes** — Confirme que el broker está publicando en las cadenas de tema exactas ingresadas. La coincidencia de temas MQTT distingue entre mayúsculas y minúsculas.

## Relacionado

- [Descripción general de MQTT](../../features/mqtt/overview.md)
- [Suscribirse a temas de rotador/interruptor de antena](../../features/mqtt/subscribe-to-rotator-antenna-switch-topics.md)
- [Superponer un valor MQTT en el panadapter (prefijar tema con *)](../../features/mqtt/overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Publicar un mensaje predefinido con un botón (ej., preset de rotador)](../../features/mqtt/publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Añadir o eliminar botones de publicación personalizados](../../features/mqtt/add-or-remove-custom-publish-buttons.md)
- [Habilitar TLS con un certificado CA personalizado](../../features/mqtt/enable-tls-with-a-custom-ca-certificate.md)
