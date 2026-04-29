# Habilitar TLS con un certificado CA personalizado

Esta página explica cómo activar el cifrado TLS para la conexión MQTT y, opcionalmente, cómo suministrar un certificado CA personalizado cuando el broker utiliza una autoridad de certificación privada o autofirmada.

## Antes de comenzar

- El applet de MQTT debe estar disponible. Si el botón de bandeja de MQTT no es visible en la barra lateral derecha, es posible que su versión de AetherSDR no incluya soporte para MQTT.
- El broker debe estar configurado para TLS, escuchando típicamente en el puerto 8883.
- Si su broker utiliza una CA privada, tenga lista la ruta al archivo de certificado CA (formato PEM).

## Pasos

1. Haga clic en el botón de bandeja de MQTT en la barra lateral derecha para abrir el applet de MQTT.
2. Si la conexión está activa en ese momento (Enable muestra "On"), haga clic en Enable para cambiarla a "Off". No es posible modificar la configuración mientras hay una conexión activa.
3. Marque la casilla TLS. El campo Port cambia automáticamente de `1883` a `8883`, y aparece la fila de CA cert debajo de TLS.
4. Confirme que el campo Port muestra el puerto correcto para su broker. El valor predeterminado al habilitar TLS es `8883`; edítelo si su broker utiliza un puerto diferente.
5. En el campo CA cert, ingrese la ruta completa al archivo de certificado CA. Deje el campo en blanco para usar el paquete CA del sistema en su lugar.
6. Verifique que los campos Host, Port, User, Pass y Topics sean correctos.
7. Haga clic en Enable. El botón cambia a "On" y todos los ajustes —incluidos `MqttTls` y `MqttCaFile`— se guardan. La etiqueta de estado cambia a "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Etiqueta | Tipo | Valor predeterminado | Notas | Clave de configuración |
|---|---|---|---|---|
| TLS | Casilla de verificación | Off (sin marcar) | Habilita el cifrado TLS. Muestra la fila de CA cert y alterna automáticamente Port entre `1883` y `8883`. | `MqttTls` |
| CA cert | Campo de texto | *(en blanco)* | Ruta a un archivo de certificado CA. Solo visible cuando TLS está marcado. En blanco indica que se usa el paquete CA del sistema. | `MqttCaFile` |
| Port | Campo de texto | `1883` (sin TLS) / `8883` (con TLS) | Rango válido: 1–65535. Se actualiza automáticamente al alternar TLS, pero puede editarse manualmente. | `MqttPort` |
| Enable | Botón de alternancia | Off | Conecta o desconecta. Guarda todos los ajustes —incluidos TLS y CA cert— al cambiar a "On". | *(no se persiste de forma independiente)* |

## Consejos

- Si desmarca TLS después de haberlo configurado en el puerto `8883`, el campo Port revierte automáticamente a `1883`. Verifique el valor del puerto antes de hacer clic en Enable si su broker usa un puerto no estándar.
- La fila de CA cert se oculta cuando TLS está desmarcado. Si no puede ver el campo CA cert, confirme que la casilla TLS esté marcada.
- Los ajustes se guardan únicamente cuando se hace clic en Enable hasta la posición "On". Editar los campos y luego cerrar el applet sin hacer clic en Enable no preserva los cambios.
- La etiqueta de estado muestra "Disconnected" en gris, "Connected" en verde, o un mensaje de error si la conexión falla —por ejemplo, si la ruta del certificado CA es incorrecta o el certificado no valida el broker.

## Solución de problemas

- **La etiqueta de estado muestra un error al hacer clic en Enable con TLS activo** — No fue posible verificar el certificado del broker. Confirme que la ruta de CA cert sea correcta y que el archivo sea legible. Si su broker utiliza una CA pública, intente dejar CA cert en blanco para recurrir al paquete CA del sistema.
- **El campo CA cert no es visible** — La casilla TLS no está marcada. Marque la casilla TLS; la fila de CA cert aparece de inmediato.
- **El puerto revirtió a 1883 al desmarcar TLS** — Este es el comportamiento esperado. Ingrese manualmente el puerto de su broker si es no estándar.
- **Enable vuelve a "Off" de inmediato** — El broker no es accesible o rechazó la conexión. Verifique los ajustes de Host, Port y TLS, y confirme que el broker esté en ejecución y sea accesible desde este equipo.

## Relacionados

- [Conectarse al broker MQTT de una estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a tópicos de rotador / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
