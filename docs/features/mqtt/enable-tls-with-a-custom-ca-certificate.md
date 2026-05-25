# Habilitar TLS con un certificado CA personalizado

Esta página explica cómo activar el cifrado TLS para la conexión MQTT y, opcionalmente, proporcionar un certificado CA personalizado cuando su broker utiliza una autoridad de certificación privada o autofirmada.

## Antes de comenzar

- El applet MQTT debe estar disponible. Si el botón de la bandeja MQTT no es visible en la barra lateral derecha, su compilación de AetherSDR puede no incluir soporte MQTT.
- Su broker debe estar configurado para TLS, normalmente escuchando en el puerto 8883.
- Si su broker utiliza una CA privada, tenga lista la ruta del archivo del certificado CA (formato PEM).

## Pasos

1. Haga clic en el botón MQTT de la bandeja en la barra lateral derecha para abrir el applet MQTT.
2. Si la conexión está actualmente activa (Enable muestra "On"), haga clic en Enable para cambiarlo a "Off". No se pueden cambiar los ajustes mientras está conectado.
3. Haga clic en **Settings...** para abrir el diálogo MQTT Settings.
4. En el diálogo **MQTT Settings**, configure los ajustes TLS:
   - Cambie a la pestaña **Connection**.
   - Active la casilla **Use TLS**.
   - El campo Port cambia automáticamente de `1883` a `8883`.
   - En el campo **CA certificate**, introduzca la ruta completa a su archivo de certificado CA. Deje el campo en blanco para usar el paquete de CA del sistema.
5. Confirme que los campos Host, Port y otros campos de conexión son correctos.
6. Haga clic en **OK** para guardar los ajustes de conexión y cerrar el diálogo.
7. Haga clic en Enable. El botón cambia a "On" y todos los ajustes se guardan. La etiqueta de estado cambia a "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Etiqueta     | Tipo                                                                                                                         | Valor predeterminado                                                      |
|--------------|------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| Enable       | Botón de alternancia                                                                                                         | Off                                                                       |
| Settings...  | Botón pulsador                                                                                                               | Abre el diálogo MQTT Settings (MqttSettingsDialog) para configuración del broker, suscripciones y botones de publicación. Nuevo en v26.5.3. Reemplaza los campos Host/Port/User/Pass/TLS/Topics en línea. |
| Botones de publicación | Botón pulsador (hasta 12)                                                                                          | Ninguno                                                                   |
| Registro de mensajes | Lista                                                                                                                 | Muestra los mensajes recibidos como líneas 'topic: value'. Limitado a 50 entradas. |

## Consejos

- La contraseña se almacena en el llavero del sistema y se carga automáticamente cuando activa la conexión por primera vez.
- Si desmarca TLS después de haberlo configurado en el puerto `8883`, el campo Port vuelve automáticamente a `1883`. Verifique el valor del puerto antes de hacer clic en Enable si su broker utiliza un puerto no estándar.
- El campo CA certificate solo está disponible cuando la casilla Use TLS está marcada.
- Los ajustes se guardan al hacer clic en **OK** en el diálogo MQTT Settings o cuando Enable se cambia a la posición "On".
- La etiqueta de estado muestra "Disconnected" en gris, "Connected" en verde o un mensaje de error si la conexión falla — por ejemplo, si la ruta del certificado CA es incorrecta o el certificado no valida el broker.

## Solución de problemas

- **La etiqueta de estado muestra un error después de hacer clic en Enable con TLS activado** — No se pudo verificar el certificado del broker. Confirme que la ruta del certificado CA es correcta y que el archivo se puede leer. Si su broker utiliza una CA pública, intente dejar el campo CA certificate en blanco para usar el paquete de CA del sistema.
- **El campo CA certificate no es visible** — La casilla Use TLS no está marcada. Marque la casilla Use TLS; el campo CA certificate aparece inmediatamente.
- **El puerto volvió a 1883 después de desmarcar TLS** — Este comportamiento es esperado. Vuelva a introducir manualmente el puerto de su broker si no es estándar.
- **Enable vuelve a "Off" inmediatamente** — El broker es inalcanzable o rechazó la conexión. Verifique los ajustes Host, Port y TLS, y confirme que el broker está funcionando y es accesible desde esta máquina.
- **El estado muestra 'Waiting for keychain'** — El llavero del sistema no está desbloqueado o la contraseña aún no se ha guardado. Vuelva a introducir la contraseña en el diálogo MQTT Settings e intente nuevamente.

## Relacionado

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Subscribe to rotator / antenna switch topics](subscribe-to-rotator-antenna-switch-topics.md)
- [MQTT overview](overview.md)
