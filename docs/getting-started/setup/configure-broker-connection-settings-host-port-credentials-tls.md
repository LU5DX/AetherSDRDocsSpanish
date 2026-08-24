# Configurar los ajustes de conexión del broker (host, puerto, credenciales, TLS)

Configure la dirección del broker MQTT, la autenticación y las opciones TLS que AetherSDR utiliza para conectarse al broker MQTT de su estación.

## Antes de comenzar

- El applet MQTT debe estar visible en la barra lateral derecha. Si está oculto, haga clic en el botón de la bandeja MQTT para mostrarlo.
- Necesita el nombre de host o la dirección IP de su broker, el puerto y, si corresponde, el nombre de usuario y la contraseña.

## Pasos

1. Abra `Settings > MQTT...` para mostrar el diálogo MQTT Settings.
2. En la pestaña **Broker Connection**, ingrese lo siguiente:
   - **Host** — el nombre de host o la dirección IP de su broker.
   - **Port** — el puerto TCP (el valor predeterminado depende de su broker; los valores comunes son 1883 para TCP sin cifrar o 8883 para TLS).
   - **Username** — opcional; déjelo en blanco si su broker no requiere autenticación.
   - **Password** — opcional; se almacena en el llavero del sistema cuando se habilita la conexión por primera vez (no en texto plano).
3. Para habilitar TLS:
   - Marque **Use TLS**.
   - Si su broker utiliza un certificado CA personalizado, ingrese la ruta del archivo en **CA Certificate File** (o haga clic en **Browse...** para ubicarlo).
4. Haga clic en **OK** para guardar los ajustes y cerrar el diálogo.
5. En el applet MQTT, haga clic en **Off** para cambiarlo a **On**. AetherSDR se conecta con los nuevos ajustes. La etiqueta de estado cambia a **Connected** (verde) en caso de éxito, o muestra un mensaje de error si la conexión falla.

## Qué hace cada control

| Control             | Predeterminado                                                                                                                                             | Notas                                                                                                                                                                                                    |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Username            | (vacío)                                                                                                                                                    | Nombre de usuario de autenticación                                                                                                                                                                       |
| Password            | (vacío)                                                                                                                                                    | Se almacena en el llavero del sistema cuando se usa por primera vez                                                                                                                                      |
| Use TLS             | sin marcar                                                                                                                                                 | Activa o desactiva el cifrado TLS                                                                                                                                                                        |
| CA Certificate File | (vacío)                                                                                                                                                    | Ruta al certificado CA personalizado para TLS                                                                                                                                                            |
| Settings...         |                                                                                                                                                            | Abre el diálogo MQTT Settings (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. Nuevo en v26.5.3. Reemplaza los campos integrados Host/Port/User/Pass/TLS/Topics. |
| Enable (Off/On)     | Conecta o desconecta del broker usando los ajustes de MqttSettings. Emite connectRequested / disconnectRequested y guarda el estado de conexión habilitada. | La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'.                          |
| Publish buttons     | Hacer clic publica la carga útil configurada en el tema configurado mediante MqttClient::publish. Los botones se configuran en el diálogo MQTT Settings.   | Solo están activos mientras está conectado. Se configuran mediante la pestaña Publish Buttons de MqttSettingsDialog.                                                                                     |
| Message log         | Muestra los mensajes recibidos como líneas 'tema: valor'. También procesa actualizaciones de alias de antena desde MQTT.                                  | Limitado a 50 entradas.                                                                                                                                                                                  |
| Status label        | Disconnected                                                                                                                                               | Muestra "Connected" (verde) en caso de éxito, "Disconnected" (gris) cuando está apagado o falla, o un mensaje de error (color predeterminado).                                                            |

## Consejos

- La contraseña se migra al llavero del sistema la primera vez que habilita la conexión MQTT. Si la migración falla, AetherSDR registra una advertencia y conserva la entrada en texto plano para reintentar.
- v26.8.4: Si una contraseña MQTT llega mediante importación XML (RFC #4603), se almacena en un almacén de credenciales de sesión y se usa de inmediato. Si el llavero no está disponible, la contraseña permanece solo en la sesión y nunca se escribe en los ajustes en texto plano.
- Si habilita la conexión ("On") pero la contraseña aún no se ha cargado desde el llavero, el estado muestra **Waiting for keychain** hasta que se complete la lectura del llavero.
- v26.6.1: El applet MQTT ahora usa colores adaptados al tema para todos los elementos de la interfaz, adaptándose automáticamente a los temas claro y oscuro.
- v26.6.3: El registro de mensajes ahora también muestra los mensajes transmitidos como líneas `TX tema: carga útil`, lo que le ayuda a confirmar que los botones de publicación envían los datos correctos.
- Los temas de alias de antena se suscriben automáticamente.

## Solución de problemas

- **El estado muestra "Disconnected" después de activar On** — Verifique que el host y el puerto sean correctos y accesibles desde su equipo. Si usa TLS, compruebe que la ruta del certificado CA sea válida.
- **El estado muestra un mensaje de error** — El broker rechazó la conexión. Confirme el nombre de usuario y la contraseña, y que los ajustes TLS coincidan con la configuración de su broker.
- **"Waiting for keychain" nunca se resuelve** — El llavero del sistema puede estar bloqueado o no disponible. Desbloquee su llavero y cambie la conexión a Off y luego a On nuevamente.
- **Los mensajes publicados no aparecen en el registro** — Verifique que el tema y la carga útil del botón de publicación estén configurados correctamente en el diálogo MQTT Settings. El registro solo muestra transmisiones de AetherSDR, no de otros clientes MQTT.

## Relacionados

- [Conectarse a un broker MQTT de estación](connect-to-a-station-mqtt-broker.md)
- [Habilitar TLS con un certificado CA personalizado](../../features/mqtt/enable-tls-with-a-custom-ca-certificate.md)
- [Abrir ajustes MQTT desde el applet](../../features/mqtt/open-mqtt-settings-from-the-applet.md)
