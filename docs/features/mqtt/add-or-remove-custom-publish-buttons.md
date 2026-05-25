# Applet MQTT

El applet MQTT integra AetherSDR con un broker MQTT de la estación. Permite publicar mensajes predefinidos mediante botones editables por el usuario, monitorear mensajes entrantes y superponer valores de temas en el panadaptador.

## Vista general

El applet MQTT proporciona tres funciones principales:
- **Botones de publicación**: Hasta 12 botones definidos por el usuario que envían cargas útiles fijas a temas fijos al hacer clic.
- **Registro de mensajes**: Muestra hasta 50 mensajes recibidos como líneas "tema: valor".
- **Control de conexión**: Botón de alternancia Activar/Desactivar para conectar o desconectar del broker.

## Configuración de conexión

Los ajustes de conexión (host, puerto, credenciales, TLS y suscripciones) se configuran en el cuadro de diálogo dedicado de Configuración MQTT.

1. En el applet MQTT, haga clic en **Settings...**.
2. En el cuadro de diálogo de Configuración MQTT, configure la conexión al broker:
   - **Host**: Nombre de host o dirección IP del broker.
   - **Port**: Puerto del broker (predeterminado 1883 para conexión simple, 8883 para TLS).
   - **User**: Nombre de usuario para autenticación (dejar en blanco si no es necesario).
   - **Password**: Contraseña para autenticación. Se almacena en el llavero del sistema.
   - **TLS**: Activar cifrado TLS.
   - **CA cert**: Ruta al archivo de certificado CA (opcional; en blanco usa el paquete CA del sistema).
3. Configure los temas de suscripción en la pestaña **Subscriptions**:
   - Ingrese temas separados por comas para suscribirse.
   - Anteponga `*` para mostrar en la superposición del panadaptador.
   - Ejemplo: `*rotator/pos, *ant/selected, station/log`
4. Configure los botones de publicación en la pestaña **Publish Buttons**.
5. Haga clic en **OK** para guardar los ajustes.

## Conectar al broker

1. En el applet MQTT, haga clic en **Enable** (botón de alternancia) para conectar.
2. La etiqueta de estado muestra el estado de conexión:
   - **Disconnected** (gris) - no conectado.
   - **Connected** (verde) - conectado y listo.
   - Mensaje de error (color predeterminado) - error de conexión.

Al activar por primera vez, la contraseña se carga desde el llavero del sistema. Si la contraseña del llavero aún no está cargada, el estado muestra "Waiting for keychain".

Para desconectar, haga clic en **Enable** nuevamente.

## Botones de publicación

El applet MQTT admite hasta 12 botones de publicación definidos por el usuario. Cada botón envía una carga útil fija a un tema fijo al hacer clic.

### Antes de comenzar

- El applet MQTT debe estar visible. Si no lo está, haga clic en el botón de bandeja MQTT en la barra lateral derecha para mostrarlo.
- No es necesario estar conectado al broker para editar botones. Sin embargo, los botones solo publican cuando el applet está conectado (el estado muestra "Connected").
- Las definiciones de botones se almacenan en `MqttButtons` y persisten entre sesiones.

### Agregar un botón

1. En el applet MQTT, haga clic en **Settings...**.
2. En el cuadro de diálogo de Configuración MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic en **Add**.
4. En el cuadro de diálogo que se abre, ingrese una etiqueta, un tema y una carga útil para el nuevo botón.
5. Haga clic en **OK** para confirmar.
6. Haga clic en **OK** en el cuadro de diálogo de Configuración MQTT para guardar.

### Editar un botón existente

1. Haga clic en **Settings...**.
2. En el cuadro de diálogo de Configuración MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic en el botón que desea modificar. Se abre un cuadro de diálogo de edición que muestra la etiqueta, el tema y la carga útil actuales.
4. Cambie los valores según sea necesario y haga clic en **OK**.
5. Haga clic en **OK** en el cuadro de diálogo de Configuración MQTT para guardar.

### Eliminar un botón

1. Haga clic en **Settings...**.
2. En el cuadro de diálogo de Configuración MQTT, vaya a la pestaña **Publish Buttons**.
3. Haga clic derecho en el botón que desea eliminar.
4. Haga clic en **Remove** en el menú contextual que aparece.
5. Haga clic en **OK** en el cuadro de diálogo de Configuración MQTT para guardar.

## Función de cada control

| Control           | Predeterminado | Notas                                                                                                                            |
|-------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------|
| **Settings...**   | —              | Abre el cuadro de diálogo de Configuración MQTT (MqttSettingsDialog) para conexión al broker, suscripciones y configuración de botones de publicación. Nuevo en v26.5.3. |
| Botones de publicación | —          | Al hacer clic, publica la carga útil configurada en el tema configurado mediante MqttClient::publish. Solo activo mientras está conectado. Se configuran mediante la pestaña Publish Buttons de MqttSettingsDialog. |
| Registro de mensajes | —            | Muestra los mensajes recibidos como líneas "tema: valor". También procesa actualizaciones de alias de antena desde MQTT. Limitado a 50 entradas. |
| **Enable** (Off/On)| Off           | Conecta o desconecta del broker usando los ajustes de MqttSettings. La contraseña se carga desde el llavero del sistema al activar por primera vez. |

## Indicadores de estado

| Indicador     | Estados                                         | Significado                                                                          |
|---------------|-------------------------------------------------|--------------------------------------------------------------------------------------|
| Etiqueta de estado | Disconnected, Connected, \<mensaje de error\>  | Estado de conexión con color: verde cuando está conectado, gris cuando está desconectado, color predeterminado en caso de error. |

## Consejos

- La información sobre herramientas de los botones muestra el tema y la carga útil de destino cuando el applet está en modo normal (`tema → carga útil`).
- Los botones están inactivos cuando el applet está desconectado. Conéctese primero, luego use los botones para publicar.
- Si necesita publicar en el mismo tema con diferentes cargas útiles, cree un botón por cada carga útil.
- La contraseña se almacena en el llavero del sistema por seguridad.

## Solución de problemas

- **Al hacer clic en un botón de publicación no sucede nada** — El applet no está conectado. Verifique que la etiqueta de estado diga "Connected". Si dice "Disconnected" o muestra un mensaje de error, haga clic en **Enable** para conectar.
- **No se pueden agregar más de 12 botones** — 12 es el número máximo de botones de publicación. Elimine al menos un botón antes de agregar otro.
- **La conexión falla** — Verifique que el host, puerto y credenciales del broker en Settings... sean correctos. Asegúrese de que el broker esté funcionando y sea accesible.
- **Aparece el aviso de contraseña en cada conexión** — Es posible que el llavero del sistema no sea accesible. Verifique la configuración del llavero de su sistema.

## Relacionados

- [Connect to a station MQTT broker](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Publish a canned message with a button (e.g. rotator preset)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [MQTT overview](overview.md)
