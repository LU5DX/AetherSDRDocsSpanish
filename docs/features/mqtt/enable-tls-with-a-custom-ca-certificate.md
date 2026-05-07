# Habilitar TLS con un certificado CA personalizado

Esta página explica cómo activar el cifrado TLS para la conexión MQTT y, opcionalmente, proporcionar un certificado CA personalizado cuando su broker utiliza una autoridad de certificación privada o autofirmada.

## Antes de comenzar

- La applet MQTT debe estar disponible. Si el botón de la bandeja MQTT no es visible en la barra lateral derecha, su versión de AetherSDR puede no incluir soporte MQTT.
- Su broker debe estar configurado para TLS, normalmente escuchando en el puerto 8883.
- Si su broker utiliza una CA privada, tenga lista la ruta del archivo del certificado CA (formato PEM).

## Pasos

1. Haga clic en el botón de la bandeja MQTT en la barra lateral derecha para abrir la applet MQTT.
2. Si la conexión está actualmente activa (Enable muestra "On"), haga clic en Enable para cambiarlo a "Off". Los ajustes no se pueden modificar mientras está conectado.
3. Marque la casilla TLS. El campo Port cambia automáticamente de `1883` a `8883`, y la fila CA cert aparece debajo de TLS.
4. Confirme que el campo Port muestra el puerto correcto para su broker. El valor predeterminado después de habilitar TLS es `8883`; edítelo si su broker usa un puerto diferente.
5. En el campo CA cert, introduzca la ruta completa a su archivo de certificado CA. Deje el campo en blanco para usar el conjunto de CA del sistema en su lugar.
6. Verifique que los campos Host, Port, User, Pass y Topics sean correctos.
7. Haga clic en Enable. El botón cambia a "On" y todos los ajustes — incluyendo `MqttTls` y `MqttCaFile` — se guardan. La etiqueta de estado cambia a "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Notas | Clave de ajuste |
|---|---|---|---|---|
| TLS | Casilla de verificación | Off (sin marcar) | Habilita el cifrado TLS. Muestra la fila CA cert y cambia automáticamente Port entre `1883` y `8883`. | `MqttTls` |
| CA cert | Campo de texto | *(en blanco)* | Ruta a un archivo de certificado CA. Visible solo cuando TLS está marcado. En blanco significa que se usa el conjunto de CA del sistema. | `MqttCaFile` |
| Port | Campo de texto | `1883` (sin TLS) / `8883` (con TLS) | Rango válido: 1–65535. Se actualiza automáticamente al alternar TLS, pero se puede editar manualmente. | `MqttPort` |
| Enable | Botón de alternancia | Off | Conecta o desconecta. Guarda todos los ajustes — incluyendo TLS y CA cert — cuando se cambia a "On". | *(no se persiste de forma independiente)* |

## Consejos

- Si desmarca TLS después de haberlo configurado en el puerto `8883`, el campo Port vuelve automáticamente a `1883`. Verifique el valor del puerto antes de hacer clic en Enable si su broker utiliza un puerto no estándar.
- La fila CA cert está oculta cuando TLS no está marcado. Si no puede ver el campo CA cert, confirme que la casilla TLS esté marcada.
- Los ajustes se guardan solo cuando se hace clic en Enable en la posición "On". Editar los campos y luego cerrar la applet sin hacer clic en Enable no conserva los cambios.
- La etiqueta de estado muestra "Disconnected" en gris, "Connected" en verde, o un mensaje de error si la conexión falla — por ejemplo, si la ruta del certificado CA es incorrecta o el certificado no valida el broker.

## Solución de problemas

- **La etiqueta de estado muestra un error después de hacer clic en Enable con TLS activado** — El certificado del broker no pudo ser verificado. Confirme que la ruta de CA cert es correcta y que el archivo se puede leer. Si su broker utiliza una CA pública, intente dejar CA cert en blanco para recurrir al conjunto de CA del sistema.
- **El campo CA cert no es visible** — La casilla TLS no está marcada. Marque la casilla TLS; la fila CA cert aparece inmediatamente.
- **El puerto volvió a 1883 después de desmarcar TLS** — Este es el comportamiento esperado. Vuelva a introducir manualmente el puerto de su broker si no es estándar.
- **Enable vuelve a "Off" inmediatamente** — El broker no es accesible o rechazó la conexión. Verifique los ajustes de Host, Port y TLS, y confirme que el broker está en funcionamiento y es accesible desde esta máquina.

## Relacionados

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a temas de rotador / interruptor de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Visión general de MQTT](overview.md)
