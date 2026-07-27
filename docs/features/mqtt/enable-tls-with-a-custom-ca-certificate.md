# Habilitar TLS con un certificado CA personalizado

Esta página explica cómo activar el cifrado TLS para la conexión MQTT y, opcionalmente, proporcionar un certificado CA personalizado cuando su broker utiliza una autoridad de certificación privada o autofirmada.

## Antes de comenzar

- El applet MQTT debe estar disponible. Si el botón MQTT en la bandeja no es visible en la barra lateral derecha, su compilación de AetherSDR puede no incluir soporte MQTT.
- Su broker debe estar configurado para TLS, normalmente escuchando en el puerto 8883.
- Si su broker utiliza una CA privada, tenga lista la ruta del archivo del certificado CA (formato PEM).

## Pasos

1. Haga clic en el botón MQTT en la bandeja de la barra lateral derecha para abrir el applet MQTT.
2. Si la conexión está actualmente activa (Enable muestra "On"), haga clic en Enable para cambiarlo a "Off". No se pueden cambiar los ajustes mientras está conectado.
3. Haga clic en **Settings...** para abrir el diálogo de Configuración MQTT.
4. En el diálogo **MQTT Settings**, configure los ajustes TLS:
   - Cambie a la pestaña **Connection**.
   - Active la casilla **Use TLS**.
   - El campo Port cambia automáticamente de `1883` a `8883`.
   - En el campo **CA certificate**, introduzca la ruta completa a su archivo de certificado CA. Deje el campo en blanco para usar el conjunto de CA del sistema.
5. Confirme que los campos Host, Port y otros campos de conexión sean correctos.
6. Haga clic en **OK** para guardar los ajustes de conexión y cerrar el diálogo.
7. Haga clic en Enable. El botón cambia a "On" y todos los ajustes se guardan. La etiqueta de estado cambia a "Connected" en verde cuando el broker acepta la conexión.

## Qué hace cada control

| Etiqueta        | Tipo                                                                                                                                                | Valor predeterminado                                                                   |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| Enable          | Botón de alternancia. Conecta o desconecta del broker. La contraseña se carga desde el llavero del sistema al habilitar por primera vez.            | Off                                                                                    |
| Settings...     | Botón pulsador. Abre el diálogo de Configuración MQTT para la conexión al broker, suscripciones y configuración de los botones de publicación.      | Ninguno                                                                                |
| Botones de publicación | Al hacer clic, se publica la carga útil configurada en el tema configurado a través de MqttClient::publish. Los botones se configuran en el diálogo de Configuración MQTT. | Solo activos mientras está conectado. Configurados en la pestaña Publish Buttons del diálogo MqttSettingsDialog. |
| Registro de mensajes | Muestra los mensajes recibidos como líneas 'topic: value'. También procesa actualizaciones de alias de antena desde MQTT.                            | Limitado a 50 entradas.                                                                |

## Indicadores

| Etiqueta       | Estados                                    | Significado                                                                                   |
|----------------|--------------------------------------------|-----------------------------------------------------------------------------------------------|
| Etiqueta de estado | "Disconnected", "Connected", <mensaje de error> | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, por defecto en error. |

## Consejos

- La contraseña se almacena en el llavero del sistema y se carga automáticamente cuando habilita la conexión por primera vez.
- Si desmarca TLS después de haberlo configurado en el puerto `8883`, el campo Port vuelve automáticamente a `1883`. Verifique el valor del puerto antes de hacer clic en Enable si su broker utiliza un puerto no estándar.
- El campo CA certificate solo está disponible cuando la casilla Use TLS está marcada.
- Los ajustes se guardan cuando hace clic en **OK** en el diálogo de Configuración MQTT o cuando Enable se cambia a la posición "On".
- La etiqueta de estado muestra "Disconnected" en gris, "Connected" en verde o un mensaje de error si la conexión falla — por ejemplo, si la ruta del certificado CA es incorrecta o el certificado no valida al broker.
- El applet MQTT ahora admite temas. Los colores se adaptan al tema seleccionado usando `ThemeManager`.
- El registro de mensajes ahora muestra tanto los mensajes recibidos como los publicados. Los mensajes publicados tienen el prefijo "TX" seguido del tema y la carga útil (truncados a 80 caracteres).

## Solución de problemas

- **La etiqueta de estado muestra un error después de hacer clic en Enable con TLS activado** — El certificado del broker no pudo verificarse. Confirme que la ruta del certificado CA sea correcta y el archivo sea legible. Si su broker utiliza una CA pública, intente dejar el campo CA cert en blanco para usar el conjunto de CA del sistema.
- **El campo CA certificate no es visible** — La casilla Use TLS no está marcada. Marque la casilla Use TLS; el campo CA certificate aparece inmediatamente.
- **El puerto volvió a 1883 después de desmarcar TLS** — Este es un comportamiento esperado. Vuelva a introducir manualmente el puerto de su broker si no es estándar.
- **Enable vuelve a "Off" inmediatamente** — El broker no es accesible o rechazó la conexión. Verifique los ajustes de Host, Port y TLS, y confirme que el broker esté en ejecución y sea accesible desde esta máquina.
- **El estado muestra 'Waiting for keychain'** — El llavero del sistema no está desbloqueado o la contraseña aún no se ha guardado. Vuelva a introducir la contraseña en el diálogo de Configuración MQTT e intente nuevamente.

## Relacionado

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Suscribirse a temas de rotador / conmutador de antena](subscribe-to-rotator-antenna-switch-topics.md)
- [Descripción general de MQTT](overview.md)
