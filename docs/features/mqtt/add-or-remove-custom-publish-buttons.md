# Applet MQTT

El applet MQTT integra AetherSDR con un broker MQTT de la estación. Permite publicar mensajes predefinidos con botones editables por el usuario, monitorear mensajes entrantes, ver mensajes publicados en el registro de mensajes y superponer valores de tópicos en el panadapter.

## Resumen

El applet MQTT proporciona cuatro funciones principales:
- **Botones de publicación**: Hasta 12 botones definidos por el usuario que envían cargas útiles fijas a tópicos fijos al hacer clic.
- **Registro de mensajes**: Muestra hasta 50 mensajes recibidos y publicados como líneas de "tópico: valor".
- **Registro de mensajes publicados**: Muestra los mensajes enviados con el prefijo "TX" en el registro de mensajes.
- **Control de conexión**: Alternancia Habilitar/Deshabilitar para conectar o desconectar del broker.

## Configuración de conexión

Los ajustes de conexión (host, puerto, credenciales, TLS y suscripciones) se configuran en el diálogo dedicado de Configuración MQTT.

1. En el applet MQTT, haga clic en **Settings...**.
2. En el diálogo de Configuración MQTT, configure la conexión al broker:
   - **Host**: Nombre de host o dirección IP del broker.
   - **Port**: Puerto del broker (1883 por defecto para conexión simple, 8883 para TLS).
   - **User**: Nombre de usuario para autenticación (déjelo en blanco si no es necesario).
   - **Password**: Contraseña para autenticación. Se almacena en el llavero del sistema.
   - **TLS**: Active el cifrado TLS.
   - **CA cert**: Ruta al archivo del certificado CA (opcional; en blanco usa el paquete CA del sistema).
3. Configure los tópicos de suscripción en la pestaña **Subscriptions**:
   - Ingrese tópicos separados por coma para suscribirse.
   - Anteponga `*` para mostrarlos en la superposición del panadapter.
   - Ejemplo: `*rotator/pos, *ant/selected, station/log`
4. Configure los botones de publicación en la pestaña **Publish Buttons**.
5. Haga clic en **OK** para guardar los ajustes.

## Conectarse al broker

1. En el applet MQTT, haga clic en **Enable** (botón de alternancia) para conectarse.
2. La etiqueta de estado muestra el estado de la conexión:
   - **Disconnected** (gris) - no conectado.
   - **Connected** (verde) - conectado y listo.
   - Mensaje de error (color predeterminado) - conexión fallida.

Al habilitar por primera vez, la contraseña se carga desde el llavero del sistema. Si la contraseña del llavero aún no se ha cargado, el estado muestra "Waiting for keychain".

Para desconectarse, haga clic en **Enable** nuevamente.

## Botones de publicación

El applet MQTT admite hasta 12 botones de publicación definidos por el usuario. Cada botón envía una carga útil fija a un tópico fijo al hacer clic.

### Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- No es necesario estar conectado al broker para editar botones. Sin embargo, los botones solo publican cuando el applet está conectado (el estado muestra "Connected").
- Las definiciones de botones se almacenan en `MqttButtons` y persisten entre sesiones.

### Agregar un botón

1. En el applet MQTT, haga clic en **Settings...**.
2. En el diálogo de Configuración MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic en **Add**.
4. En el diálogo que se abre, ingrese una etiqueta, un tópico y una carga útil para el nuevo botón.
5. Haga clic en **OK** para confirmar.
6. Haga clic en **OK** en el diálogo de Configuración MQTT para guardar.

### Editar un botón existente

1. Haga clic en **Settings...**.
2. En el diálogo de Configuración MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic en el botón que desea cambiar. Se abre un diálogo de edición que muestra la etiqueta, el tópico y la carga útil actuales.
4. Cambie los valores según sea necesario y haga clic en **OK**.
5. Haga clic en **OK** en el diálogo de Configuración MQTT para guardar.

### Eliminar un botón

1. Haga clic en **Settings...**.
2. En el diálogo de Configuración MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic derecho en el botón que desea eliminar.
4. Haga clic en **Remove** en el menú contextual que aparece.
5. Haga clic en **OK** en el diálogo de Configuración MQTT para guardar.

## Función de cada control

| Control             | Predeterminado                                                                                                                            | Notas                                                                                                                                                                                                                          |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Settings...**     | —                                                                                                                                         | Abre el diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. Nuevo en v26.5.3. Reemplaza los campos en línea Host/Puerto/Usuario/Pass/TLS/Topics. |
| Botones de publicación | Al hacer clic, publica la carga útil configurada en el tópico configurado a través de MqttClient::publish. Los botones se configuran en el diálogo de Configuración MQTT. | Solo están activos mientras está conectado. Se configuran a través de la pestaña Publish Buttons del MqttSettingsDialog.                                                                                                            |
| Registro de mensajes | Muestra los mensajes recibidos como líneas de 'tópico: valor'. También procesa actualizaciones de alias de antena desde MQTT.               | Limitado a 50 entradas.                                                                                                                                                                                                          |
| **Enable** (Off/On) | Off                                                                                                                                       | Conecta o desconecta del broker usando los ajustes de MqttSettings. La contraseña se carga desde el llavero del sistema al habilitar por primera vez. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'. |
| Settings...         | Abre el diálogo de Configuración MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. | Nuevo en v26.5.3. Reemplaza los campos en línea Host/Puerto/Usuario/Pass/TLS/Topics.                                                                                                                                              |

## Comportamiento del registro de mensajes

El registro de mensajes muestra tanto los mensajes recibidos como los publicados:
- **Mensajes recibidos**: Se muestran como `tópico: valor` donde tópico es el último segmento de la ruta completa del tópico.
- **Mensajes publicados**: Se muestran como `TX tópico: valor` donde tópico es el último segmento de la ruta del tópico de publicación y valor son los primeros 80 caracteres de la carga útil.

El registro tiene un límite de 50 entradas. Cuando se alcanza el límite, la entrada más antigua se elimina para dejar espacio a nuevas entradas.

## Indicadores de estado

| Indicador     | Estados                                          | Significado                                                                               |
|---------------|---------------------------------------------------|-------------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, \<mensaje de error\>   | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, predeterminado en caso de error. |

## Consejos

- Los tooltips de los botones muestran el tópico de destino y la carga útil cuando el applet está en modo normal (`tópico → carga útil`).
- Los botones están inactivos cuando el applet está desconectado. Conéctese primero, luego use los botones para publicar.
- Si necesita publicar en el mismo tópico con diferentes cargas útiles, cree un botón por carga útil.
- La contraseña se almacena en el llavero del sistema por seguridad.
- El registro de mensajes muestra los mensajes publicados con un prefijo "TX", lo que ayuda a confirmar que sus botones de publicación están enviando correctamente.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected". Si muestra "Disconnected" o un mensaje de error, haga clic en **Enable** para conectarse.
- **No se pueden agregar más de 12 botones** — 12 es el número máximo de botones de publicación. Elimine al menos un botón antes de agregar otro.
- **La conexión falla** — Verifique que el host, puerto y credenciales del broker en Settings... sean correctos. Asegúrese de que el broker esté en ejecución y sea accesible.
- **El mensaje de contraseña aparece en cada conexión** — Es posible que el llavero del sistema no sea accesible. Verifique la configuración de su llavero del sistema.

## Relacionado

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [MQTT overview](overview.md)
