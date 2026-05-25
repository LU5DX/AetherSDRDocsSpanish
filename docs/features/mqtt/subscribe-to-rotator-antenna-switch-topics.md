# Suscribirse a temas del rotador / conmutador de antenas

Utilice el applet MQTT para suscribirse a temas publicados por su controlador de rotador o conmutador de antenas. Los valores entrantes aparecen en el registro de mensajes y, si antepone el prefijo `*` a un tema, también aparecen como superposición en el panadapter.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo ve, haga clic en el botón de la bandeja MQTT en la barra lateral derecha para mostrarlo.
- El broker MQTT de su estación debe estar en ejecución y ser accesible desde el equipo que ejecuta AetherSDR.
- Si aún no ha configurado las credenciales del broker, complete primero [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).

## Pasos

1. Abra el applet MQTT haciendo clic en el botón de la bandeja MQTT en la barra lateral derecha.
2. Haga clic en **Settings...** para abrir el diálogo Configuración MQTT. Configure allí los detalles de conexión del broker, los temas de suscripción y los botones de publicación.
3. En el diálogo Configuración MQTT, ingrese el nombre de host o la dirección IP del broker, el puerto, el nombre de usuario y la contraseña. Si su broker utiliza TLS, habilite TLS y opcionalmente especifique un archivo de certificado CA.
4. En la pestaña **Subscriptions**, ingrese una lista separada por comas de los temas a los que desea suscribirse. Para mostrar también el valor de un tema como superposición en el panadapter, anteponga el prefijo `*`. Ejemplo:
   ```
   *rotator/pos, *ant/selected, station/log
   ```
5. Haga clic en **OK** para guardar la configuración y cerrar el diálogo.
6. De vuelta en el applet MQTT, haga clic en **Enable** para conectarse. La etiqueta del botón cambia a **On** y la etiqueta de estado muestra **Connected** en verde. La contraseña se carga desde el llavero del sistema al activarlo por primera vez.

## Función de cada control

| Control           | Valor predeterminado | Rango válido / Notas                                                                                      |
|-------------------|----------------------|----------------------------------------------------------------------------------------------------------|
| **Settings...**   | —                    | Abre el diálogo Configuración MQTT para la conexión al broker, suscripciones y configuración de botones de publicación.   |
| **Botones de publicación** | —        | Hasta 12 botones; cada uno publica una carga útil configurada en un tema configurado. Solo activos mientras está conectado.|
| **Registro de mensajes** | —          | Muestra hasta los últimos 50 mensajes recibidos como líneas `tema: valor`. También procesa actualizaciones de alias de antena desde MQTT. |
| **Enable (Off/On)** | Off               | Conecta o desconecta del broker usando la configuración del diálogo Configuración MQTT. La contraseña se carga desde el llavero del sistema al activarlo por primera vez. |

### Indicador de estado de conexión

| Etiqueta de estado | Significado                                                       |
|--------------------|-------------------------------------------------------------------|
| **Disconnected**   | No conectado al broker. Color gris.                              |
| **Connected**      | Conectado exitosamente al broker. Color verde.                   |
| *Mensaje de error* | Falló la conexión. Muestra el error en el color de texto predeterminado. |

## Consejos

- Un tema debe ingresarse sin el prefijo `*` para suscribirse; el `*` solo controla si el valor aparece en la superposición del panadapter. La suscripción en sí está siempre activa una vez que hace clic en **Enable**.
- El registro de mensajes muestra solo el último segmento de la ruta del tema (después de la `/` final) junto al valor, por lo que `rotator/pos` aparece como `pos: 180`.
- La configuración se guarda al hacer clic en **OK** en el diálogo Configuración MQTT. No es necesario hacer clic en **Enable** para conservarla.

## Solución de problemas

- **La etiqueta de estado muestra un mensaje de error en lugar de "Connected"** — El broker es inalcanzable o las credenciales son incorrectas. Abra **Settings...** y verifique los valores de host, puerto, nombre de usuario y contraseña, luego intente nuevamente.
- **Los temas están configurados pero no aparecen mensajes en el registro** — Confirme que el broker está publicando exactamente en esas cadenas de tema. La coincidencia de temas MQTT distingue entre mayúsculas y minúsculas.
- **Aparece el estado "Waiting for keychain"** — La contraseña aún no se ha cargado desde el llavero del sistema. Haga clic en **Enable** nuevamente para activar la solicitud del llavero.
- **Los botones de publicación están atenuados** — Debe estar conectado al broker. Haga clic en **Enable** para conectarse primero.

## Relacionado

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Superponer un valor MQTT en el panadapter (anteponer * al tema)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Habilitar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
- [Publicar un mensaje predefinido con un botón (ej. preset del rotador)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
