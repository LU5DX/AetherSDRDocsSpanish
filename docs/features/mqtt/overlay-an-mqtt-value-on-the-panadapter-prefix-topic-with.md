# Superponer un valor MQTT en el panadapter (prefije el tópico con \*)

Cuando un tópico suscrito se prefija con `*` en el campo Topics, AetherSDR superpone el valor más reciente de ese tópico directamente en la pantalla del panadapter. Esto permite monitorear datos en tiempo real, como la posición del rotador o la selección de antena, sin abandonar la vista de RF.

## Antes de comenzar

- El applet de MQTT debe estar visible. Si no lo está, haga clic en el botón MQTT del área de bandeja en la barra lateral derecha para mostrarlo.
- Necesita un broker MQTT accesible que publique el tópico que desea visualizar. Consulte [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md) si el broker aún no está configurado.
- Si el applet está actualmente conectado (Enable muestra "On"), haga clic en Enable para desconectarse antes de editar la lista de tópicos.

## Pasos

1. Abra el applet de MQTT haciendo clic en el botón MQTT del área de bandeja en la barra lateral derecha.
2. En el campo Topics, introduzca cada tópico al que desea suscribirse como una lista separada por comas. Prefije cualquier tópico con `*` para superponer también su valor en el panadapter. Por ejemplo:

    ```
    *rotator/pos, *ant/selected, station/log
    ```

    Los tópicos sin `*` se registran únicamente en el registro de mensajes. Los tópicos prefijados con `*` se registran y además se superponen en el panadapter.

3. Verifique que los campos Host, Port, User y Pass sean correctos para su broker.
4. Haga clic en Enable.
5. La etiqueta del botón cambia a "On" y la etiqueta de estado muestra "Connected" en verde. Los valores entrantes de los tópicos prefijados con `*` aparecen en el panadapter. Todos los mensajes recibidos aparecen en el registro de mensajes como líneas `topic: value`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Host | `localhost` | Cualquier nombre de host o IP | `MqttHost` | Nombre de host o dirección IP del broker. Se guarda al hacer clic en Enable. |
| Port | `1883` | 1–65535 | `MqttPort` | Puerto TCP del broker. Cambia automáticamente entre 1883 y 8883 al activar o desactivar TLS. |
| User | _(vacío)_ | Cualquier cadena | `MqttUser` | Nombre de usuario del broker. Opcional. |
| Pass | _(vacío)_ | Cualquier cadena | `MqttPass` | Contraseña del broker. Se muestra enmascarada. Opcional. |
| Topics | _(vacío)_ | Lista separada por comas | `MqttTopics` | Tópicos a los que suscribirse. Prefije con `*` para superponer el valor en el panadapter. |
| TLS | Off | On / Off | `MqttTls` | Habilita el cifrado TLS. Muestra la fila del certificado CA y cambia automáticamente el puerto entre 1883 y 8883. |
| CA cert | _(vacío)_ | Ruta de archivo | `MqttCaFile` | Ruta a un archivo de certificado CA. Si se deja en blanco, se utiliza el paquete CA del sistema. Visible solo cuando TLS está activado. |
| Enable | Off | Off / On | _(ninguno)_ | Conecta o desconecta el broker. Guarda todas las configuraciones al conectar. |
| Message log | — | Últimas 50 entradas | _(ninguno)_ | Muestra los mensajes recibidos como líneas `topic: value`. |

## Consejos

- En la superposición del panadapter solo se muestra el segmento final de la ruta del tópico. Por ejemplo, `rotator/pos` se muestra como `pos: <value>`. Si se suscribe a varios tópicos a la vez, utilice nombres cuyo último segmento sea autoexplicativo.
- La superposición se actualiza cada vez que llega un nuevo mensaje en el tópico. No hay promediado ni suavizado; se muestra el valor bruto del payload (hasta 80 caracteres).
- Si elimina el prefijo `*` de un tópico y hace clic en Enable nuevamente, la superposición de ese tópico se detiene sin cancelar la suscripción por completo. El valor sigue apareciendo en el registro de mensajes.
- Todas las configuraciones se guardan en almacenamiento persistente únicamente cuando se hace clic en Enable para conectar. Si edita los campos y cierra el applet sin hacer clic en Enable, los cambios se descartan.

## Solución de problemas

- **El estado muestra "Connected" pero no aparece ninguna superposición en el panadapter** — Confirme que la cadena del tópico en Topics coincida exactamente con lo que publica el broker, incluidas las mayúsculas y los separadores de ruta. La coincidencia de tópicos MQTT distingue entre mayúsculas y minúsculas.
- **El estado muestra un mensaje de error en lugar de "Connected"** — El broker rechazó la conexión. Verifique los campos Host, Port, User y Pass. Si TLS está habilitado, compruebe la ruta del certificado CA o déjela en blanco para usar el paquete CA del sistema.
- **La superposición desaparece tras una desconexión** — Cuando se pierde la conexión, AetherSDR borra la superposición del panadapter. Vuelva a conectarse haciendo clic en Enable para restaurarla.

## Relacionados

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a tópicos de rotador / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Habilitar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
- [Descripción general de MQTT](overview.md)
