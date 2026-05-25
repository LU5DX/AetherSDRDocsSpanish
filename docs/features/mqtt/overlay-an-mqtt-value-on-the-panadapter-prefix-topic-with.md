# Superponer un valor MQTT en el panadapter (prefijar el tema con *)

Cuando un tema suscrito tiene el prefijo `*` en el campo Topics, AetherSDR superpone el valor más reciente de ese tema directamente en la visualización del panadapter. Esto le permite monitorear datos en vivo, como la posición del rotor o la selección de antena, sin tener que cambiar la vista de RF.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- Necesita un broker MQTT accesible que publique el tema que desea mostrar. Consulte [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md) si el broker aún no está configurado.
- Si el applet está actualmente conectado (Enable muestra "On"), haga clic en Enable para desconectarse antes de editar la configuración.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha.
2. Haga clic en **Settings...** para abrir el diálogo MQTT Settings.
3. En la pestaña **Subscriptions**, ingrese cada tema al que desee suscribirse como una lista separada por comas. Agregue el prefijo `*` a cualquier tema para superponer también su valor en el panadapter. Por ejemplo:

    ```
    *rotator/pos, *ant/selected, station/log
    ```

    Los temas sin `*` solo se registran en el registro de mensajes. Los temas con el prefijo `*` se registran y se superponen en el panadapter.

4. En la pestaña **Connection**, verifique que los campos Host, Port, User y Pass sean correctos para su broker. Configure TLS si es necesario.
5. Haga clic en **Save** para cerrar el diálogo.
6. Haga clic en **Enable** en el applet.
7. La etiqueta del botón cambia a "On" y la etiqueta de estado muestra "Connected" en verde. Los valores entrantes para los temas con prefijo `*` aparecen en el panadapter. Todos los mensajes recibidos aparecen en el registro de mensajes como líneas `tema: valor`.

## Función de cada control

| Control          | Valor predeterminado                                                                                                       | Rango válido                                                              |
|------------------|----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Enable           | Off                                                                                                                        | Off / On                                                                  |
| Settings...      | Abre el diálogo MQTT Settings (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. | Nuevo en v26.5.3. Reemplaza los campos integrados Host/Port/User/Pass/TLS/Topics. |
| Publish buttons  | Haga clic para publicar la carga útil configurada en el tema configurado. Se configura en la pestaña Publish Buttons del diálogo MQTT Settings. | Hasta 12 botones. Solo activos mientras está conectado.                   |
| Message log      | Muestra los mensajes recibidos como líneas 'tema: valor'. También procesa las actualizaciones de alias de antena desde MQTT. | Limitado a 50 entradas.                                                   |

## Indicadores

| Indicador     | Estados                                                     | Significado                                                |
|---------------|-------------------------------------------------------------|------------------------------------------------------------|
| Status label  | Disconnected / Connected / <mensaje de error>                | Verde cuando está conectado, gris cuando está desconectado, predeterminado en error. |

## Consejos

- Solo se muestra el segmento final de la ruta del tema en la superposición del panadapter. Por ejemplo, `rotator/pos` se muestra como `pos: <valor>`. Use nombres de tema cuyo último segmento sea autoexplicativo si se suscribe a varios temas a la vez.
- La superposición se actualiza cada vez que llega un nuevo mensaje al tema. No hay promediado ni suavizado; se muestra el valor bruto de la carga útil (hasta 80 caracteres).
- Al eliminar el prefijo `*` de un tema y hacer clic nuevamente en Enable, se detiene la superposición para ese tema sin anular la suscripción por completo. El valor continúa apareciendo en el registro de mensajes.
- La contraseña se almacena en el llavero del sistema. Al habilitar por primera vez, si la contraseña del llavero aún no se ha cargado, el estado muestra "Waiting for keychain".

## Solución de problemas

- **El estado muestra "Connected" pero no aparece ninguna superposición en el panadapter** — Verifique que la cadena del tema en Topics coincida exactamente con lo que publica el broker, incluyendo mayúsculas/minúsculas y separadores de ruta. La coincidencia de temas MQTP distingue entre mayúsculas y minúsculas.
- **El estado muestra un mensaje de error en lugar de "Connected"** — El broker rechazó la conexión. Verifique los campos Host, Port, User y Pass en el diálogo MQTT Settings. Si TLS está habilitado, verifique la ruta del certificado CA o déjela en blanco para usar el conjunto de CA del sistema.
- **La superposición desaparece después de una desconexión** — Cuando la conexión se pierde, AetherSDR borra la superposición del panadapter. Reconéctese haciendo clic en Enable para restaurarla.
- **El estado muestra "Waiting for keychain"** — La contraseña no se ha recuperado del llavero del sistema aún. Espere un momento o asegúrese de que el llavero esté desbloqueado.

## Relacionados

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Subscribe to rotator / antenna switch topics](subscribe-to-rotator-antenna-switch-topics.md)
- [Enable TLS with a custom CA certificate](enable-tls-with-a-custom-ca-certificate.md)
- [MQTT overview](overview.md)
