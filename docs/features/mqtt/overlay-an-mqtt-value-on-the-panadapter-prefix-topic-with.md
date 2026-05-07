# Superponer un valor MQTT en el panadapter (prefijar el tema con *)

Cuando un tema suscrito tiene el prefijo `*` en el campo Topics, AetherSDR superpone el valor más reciente de ese tema directamente en la pantalla del panadapter. Esto le permite monitorear datos en vivo, como la posición del rotor o la selección de antena, sin tener que cambiar la vista de RF.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón MQTT de la barra lateral derecha para mostrarlo.
- Necesita un broker MQTT accesible que publique el tema que desea mostrar. Consulte [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md) si el broker aún no está configurado.
- Si el applet está actualmente conectado (Enable muestra "On"), haga clic en Enable para desconectarse antes de editar la lista de temas.

## Pasos

1. Abra el applet MQTT haciendo clic en el botón MQTT de la barra lateral derecha.
2. En el campo Topics, ingrese cada tema al que desea suscribirse como una lista separada por comas. Prefije cualquier tema con `*` para superponer también su valor en el panadapter. Por ejemplo:

    ```
    *rotator/pos, *ant/selected, station/log
    ```

    Los temas sin `*` solo se registran en el registro de mensajes. Los temas con el prefijo `*` se registran y se superponen en el panadapter.

3. Verifique que los campos Host, Port, User y Pass sean correctos para su broker.
4. Haga clic en Enable.
5. La etiqueta del botón cambia a "On" y la etiqueta de estado muestra "Connected" en verde. Los valores entrantes para los temas con prefijo `*` aparecen en el panadapter. Todos los mensajes recibidos aparecen en el registro de mensajes como líneas `tema: valor`.

## Función de cada control

| Control | Predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Host | `localhost` | Cualquier nombre de host o IP | `MqttHost` | Nombre de host o dirección IP del broker. Se guarda al hacer clic en Enable. |
| Port | `1883` | 1–65535 | `MqttPort` | Puerto TCP del broker. Cambia automáticamente entre 1883 y 8883 cuando se activa/desactiva TLS. |
| User | _(vacío)_ | Cualquier cadena | `MqttUser` | Nombre de usuario del broker. Opcional. |
| Pass | _(vacío)_ | Cualquier cadena | `MqttPass` | Contraseña del broker. Se muestra enmascarada. Opcional. |
| Topics | _(vacío)_ | Lista separada por comas | `MqttTopics` | Temas a los que suscribirse. Prefije con `*` para superponer el valor en el panadapter. |
| TLS | Off | On / Off | `MqttTls` | Habilita el cifrado TLS. Muestra la fila del certificado CA y cambia automáticamente el puerto entre 1883 y 8883. |
| CA cert | _(vacío)_ | Ruta de archivo | `MqttCaFile` | Ruta a un archivo de certificado CA. En blanco usa el paquete de CA del sistema. Visible solo cuando TLS está marcado. |
| Enable | Off | Off / On | _(ninguna)_ | Conecta o desconecta el broker. Guarda toda la configuración al conectar. |
| Message log | — | Últimas 50 entradas | _(ninguna)_ | Muestra los mensajes recibidos como líneas `tema: valor`. |

## Consejos

- Solo el segmento final de la ruta del tema se muestra en la superposición del panadapter. Por ejemplo, `rotator/pos` se muestra como `pos: <valor>`. Use nombres de temas cuyo último segmento sea autoexplicativo si se suscribe a varios temas a la vez.
- La superposición se actualiza cada vez que llega un mensaje nuevo al tema. No hay promediado ni suavizado; se muestra el valor bruto de la carga útil (hasta 80 caracteres).
- Eliminar el prefijo `*` de un tema y hacer clic en Enable nuevamente detiene la superposición de ese tema sin cancelar completamente la suscripción. El valor continúa apareciendo en el registro de mensajes.
- Todos los ajustes se guardan en el almacenamiento persistente solo cuando se hace clic en Enable para conectar. Editar los campos y salir del applet sin hacer clic en Enable descarta los cambios.

## Solución de problemas

- **El estado muestra "Connected" pero no aparece ninguna superposición en el panadapter** — Confirme que la cadena del tema en Topics coincida exactamente con lo que el broker está publicando, incluyendo mayúsculas/minúsculas y los separadores de ruta. La coincidencia de temas MQTT distingue entre mayúsculas y minúsculas.
- **El estado muestra un mensaje de error en lugar de "Connected"** — El broker rechazó la conexión. Verifique Host, Port, User y Pass. Si TLS está habilitado, verifique la ruta del certificado CA o déjela en blanco para usar el paquete de CA del sistema.
- **La superposición desaparece después de una desconexión** — Cuando la conexión se pierde, AetherSDR borra la superposición del panadapter. Vuelva a conectar haciendo clic en Enable para restaurarla.

## Relacionado

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a temas de rotor / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Habilitar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
- [Descripción general de MQTT](overview.md)
