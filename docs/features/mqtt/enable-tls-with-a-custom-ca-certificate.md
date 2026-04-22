# Habilitar TLS con un certificado CA personalizado

Esta página explica cómo activar el cifrado TLS para la conexión MQTT y, de forma opcional, cómo suministrar un certificado CA personalizado cuando el bróker utiliza una autoridad de certificación privada o autofirmada.

## Antes de comenzar

- El applet de MQTT debe estar disponible. Si el botón de bandeja MQTT no es visible en la barra lateral derecha, es posible que su versión de AetherSDR no incluya soporte para MQTT.
- El bróker debe estar configurado para TLS, normalmente escuchando en el puerto 8883.
- Si su bróker utiliza una CA privada, tenga lista la ruta del archivo del certificado CA (formato PEM).

## Pasos

1. Haga clic en el botón de bandeja MQTT en la barra lateral derecha para abrir el applet de MQTT.
2. Si la conexión está activa en este momento (Enable muestra "On"), haga clic en Enable para cambiarla a "Off". No es posible modificar la configuración mientras hay una conexión activa.
3. Marque la casilla TLS. El campo Port cambia automáticamente de `1883` a `8883`, y la fila CA cert aparece debajo de TLS.
4. Confirme que el campo Port muestra el puerto correcto para su bróker. El valor predeterminado al habilitar TLS es `8883`; edítelo si su bróker utiliza un puerto diferente.
5. En el campo CA cert, introduzca la ruta completa al archivo del certificado CA. Deje el campo en blanco para utilizar el paquete CA del sistema.
6. Verifique que los campos Host, Port, User, Pass y Topics sean correctos.
7. Haga clic en Enable. El botón cambia a "On" y todas las configuraciones —incluidas `MqttTls` y `MqttCaFile`— se guardan. La etiqueta de estado cambia a "Connected" en color verde cuando el bróker acepta la conexión.

## Función de cada control

| Etiqueta | Tipo | Valor predeterminado | Notas | Clave de configuración |
|---|---|---|---|---|
| TLS | Casilla de verificación | Off (sin marcar) | Habilita el cifrado TLS. Muestra la fila CA cert y cambia automáticamente Port entre `1883` y `8883`. | `MqttTls` |
| CA cert | Campo de texto | *(en blanco)* | Ruta a un archivo de certificado CA. Visible únicamente cuando TLS está marcado. En blanco significa que se utiliza el paquete CA del sistema. | `MqttCaFile` |
| Port | Campo de texto | `1883` (sin TLS) / `8883` (con TLS) | Rango válido: 1–65535. Se actualiza automáticamente al activar o desactivar TLS, pero puede editarse manualmente. | `MqttPort` |
| Enable | Botón de alternancia | Off | Conecta o desconecta. Guarda todas las configuraciones —incluidas TLS y CA cert— al cambiar a "On". | *(no se persiste de forma independiente)* |

## Consejos

- Si desmarca TLS después de haberlo configurado con el puerto `8883`, el campo Port vuelve automáticamente a `1883`. Verifique el valor del puerto antes de hacer clic en Enable si su bróker utiliza un puerto no estándar.
- La fila CA cert queda oculta cuando TLS no está marcado. Si no puede ver el campo CA cert, confirme que la casilla TLS esté marcada.
- La configuración se guarda únicamente cuando se hace clic en Enable hasta la posición "On". Editar los campos y luego cerrar el applet sin hacer clic en Enable no persiste los cambios.
- La etiqueta de estado muestra "Disconnected" en gris, "Connected" en verde, o un mensaje de error si la conexión falla —por ejemplo, si la ruta del certificado CA es incorrecta o el certificado no valida el bróker.

## Resolución de problemas

- **La etiqueta de estado muestra un error al hacer clic en Enable con TLS activado** — No fue posible verificar el certificado del bróker. Confirme que la ruta de CA cert sea correcta y que el archivo sea legible. Si su bróker utiliza una CA pública, intente dejar CA cert en blanco para recurrir al paquete CA del sistema.
- **El campo CA cert no es visible** — La casilla TLS no está marcada. Marque la casilla TLS; la fila CA cert aparece de inmediato.
- **El puerto volvió a 1883 después de desmarcar TLS** — Este es el comportamiento esperado. Introduzca manualmente el puerto de su bróker si es no estándar.
- **Enable vuelve a "Off" inmediatamente** — El bróker no es accesible o rechazó la conexión. Verifique los ajustes de Host, Port y TLS, y confirme que el bróker esté en funcionamiento y accesible desde esta máquina.

## Relacionado

- [Conectarse a un bróker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a tópicos de rotador / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
