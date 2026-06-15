# Applet MQTT

El applet MQTT integra AetherSDR con un broker MQTT de la estación. Permite publicar mensajes predefinidos con botones editables por el usuario, monitorear mensajes entrantes, ver mensajes publicados en el registro de mensajes y superponer valores de temas en el panadapter.

## Descripción general

El applet MQTT proporciona cuatro funciones principales:
- **Botones de publicación**: Hasta 12 botones definidos por el usuario que envían cargas útiles fijas a temas fijos al hacer clic.
- **Registro de mensajes**: Muestra hasta 50 mensajes recibidos y mensajes publicados como líneas "tema: valor".
- **Registro de mensajes publicados**: Muestra los mensajes enviados con el prefijo "TX" en el registro de mensajes.
- **Control de conexión**: Botón de activación/desactivación para conectar o desconectar del broker.

## Configuración de conexión

Los ajustes de conexión (host, puerto, credenciales, TLS y suscripciones) se configuran en el diálogo dedicado de Ajustes MQTT.

1. En el applet MQTT, haga clic en **Settings...**.
2. En el diálogo de Ajustes MQTT, configure la conexión al broker:
   - **Host**: Nombre de host o dirección IP del broker.
   - **Port**: Puerto del broker (1883 por defecto para conexión simple, 8883 para TLS).
   - **User**: Nombre de usuario para autenticación (déjelo en blanco si no es necesario).
   - **Password**: Contraseña para autenticación. Se almacena en el llavero de claves del sistema.
   - **TLS**: Habilite el cifrado TLS.
   - **CA cert**: Ruta al archivo de certificado CA (opcional; en blanco usa el paquete de CA del sistema).
3. Configure los temas de suscripción en la pestaña **Subscriptions**:
   - Ingrese temas separados por comas para suscribirse.
   - Anteponga `*` para mostrar en la superposición del panadapter.
   - Ejemplo: `*rotator/pos, *ant/selected, station/log`
4. Configure los botones de publicación en la pestaña **Publish Buttons**.
5. Haga clic en **OK** para guardar los ajustes.

## Conectar al broker

1. En el applet MQTT, haga clic en **Enable** (botón de activación/desactivación) para conectar.
2. La etiqueta de estado muestra el estado de la conexión:
   - **Disconnected** (gris) - no conectado.
   - **Connected** (verde) - conectado y listo.
   - Mensaje de error (color por defecto) - falló la conexión.

Al activar por primera vez, la contraseña se carga desde el llavero de claves del sistema. Si la contraseña del llavero aún no se ha cargado, el estado muestra "Waiting for keychain".

Para desconectar, haga clic en **Enable** nuevamente.

## Botones de publicación

El applet MQTT admite hasta 12 botones de publicación definidos por el usuario. Cada botón envía una carga útil fija a un tema fijo al hacer clic.

### Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- No es necesario estar conectado al broker para editar los botones. Sin embargo, los botones solo publican cuando el applet está conectado (el estado muestra "Connected").
- Las definiciones de botones se almacenan en `MqttButtons` y persisten entre sesiones.

### Agregar un botón

1. En el applet MQTT, haga clic en **Settings...**.
2. En el diálogo de Ajustes MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic en **Add**.
4. En el diálogo que se abre, ingrese una etiqueta, un tema y una carga útil para el nuevo botón.
5. Haga clic en **OK** para confirmar.
6. Haga clic en **OK** en el diálogo de Ajustes MQTT para guardar.

### Editar un botón existente

1. Haga clic en **Settings...**.
2. En el diálogo de Ajustes MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic en el botón que desea cambiar. Se abre un diálogo de edición que muestra la etiqueta, el tema y la carga útil actuales.
4. Cambie los valores según sea necesario y haga clic en **OK**.
5. Haga clic en **OK** en el diálogo de Ajustes MQTT para guardar.

### Eliminar un botón

1. Haga clic en **Settings...**.
2. En el diálogo de Ajustes MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic derecho en el botón que desea eliminar.
4. Haga clic en **Remove** en el menú contextual que aparece.
5. Haga clic en **OK** en el diálogo de Ajustes MQTT para guardar.

## Qué hace cada control

| Control             | Por defecto                                                                                                                               | Notas                                                                                                                                                                                                                                                                  |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Settings...**     | —                                                                                                                                         | Abre el diálogo de Ajustes MQTT (MqttSettingsDialog) para la conexión al broker, suscripciones y configuración de botones de publicación. Nuevo en v26.5.3. Reemplaza los campos en línea Host/Port/User/Pass/TLS/Topics.                                             |
| Botones de publicación | Al hacer clic publica la carga útil configurada en el tema configurado a través de MqttClient::publish. Los botones se configuran en el diálogo de Ajustes MQTT. | Solo activos mientras está conectado. Se configuran a través de la pestaña Publish Buttons de MqttSettingsDialog.                                                                                                                                                       |
| Registro de mensajes | Muestra los mensajes recibidos como líneas 'tema: valor'. También muestra los mensajes enviados con el prefijo 'TX'. Procesa actualizaciones de alias de antena desde MQTT. | Limitado a 50 entradas. Los mensajes enviados se registran con el nombre corto del tema y los primeros 80 caracteres de la carga útil.                                                                                                                                 |
| **Enable** (Off/On) | Off                                                                                                                                       | Conecta o desconecta del broker usando los ajustes de MqttSettings. La contraseña se carga desde el llavero de claves del sistema al activar por primera vez. Si la contraseña del llavero aún no se ha cargado, muestra el estado 'Waiting for keychain'.              |

## Comportamiento del registro de mensajes

El registro de mensajes muestra tanto los mensajes recibidos como los publicados:
- **Mensajes recibidos**: Se muestran como `tema: valor` donde el tema es el último segmento de la ruta completa del tema.
- **Mensajes publicados**: Se muestran como `TX tema: valor` donde el tema es el último segmento de la ruta del tema de publicación y el valor son los primeros 80 caracteres de la carga útil.

El registro tiene un límite de 50 entradas. Cuando se alcanza el límite, se elimina la entrada más antigua para dejar espacio a nuevas entradas.

## Indicadores de estado

| Indicador     | Estados                                          | Significado                                                                                                        |
|---------------|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, \<mensaje de error\>    | Estado de la conexión con color: verde cuando está conectado, gris cuando está desconectado, por defecto en error. |

## Consejos

- La información sobre herramientas de los botones muestra el tema de destino y la carga útil cuando el applet está en modo normal (`tema → carga útil`).
- Los botones están inactivos cuando el applet está desconectado. Conéctese primero, luego use los botones para publicar.
- Si necesita publicar en el mismo tema con diferentes cargas útiles, cree un botón por carga útil.
- La contraseña se almacena en el llavero de claves del sistema por seguridad.
- El registro de mensajes muestra los mensajes publicados con un prefijo "TX", lo que le ayuda a confirmar que sus botones de publicación están enviando correctamente.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que la etiqueta de estado diga "Connected". Si dice "Disconnected" o muestra un mensaje de error, haga clic en **Enable** para conectar.
- **No se pueden agregar más de 12 botones** — 12 es el número máximo de botones de publicación. Elimine al menos un botón antes de agregar otro.
- **La conexión falla** — Verifique que el host, puerto y credenciales del broker en Settings... sean correctos. Asegúrese de que el broker esté en ejecución y sea accesible.
- **Aparece la solicitud de contraseña en cada conexión** — Es posible que el llavero de claves del sistema no sea accesible. Verifique la configuración de su llavero de claves del sistema.

## Relacionados

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [MQTT overview](overview.md)
