# Suscribirse a temas de rotador / conmutador de antena

Utilice el applet MQTT para suscribirse a temas publicados por su controlador de rotador o conmutador de antena. Los valores entrantes aparecen en el registro de mensajes y, si antepone un tema con `*`, como una superposición en el panadapter.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo ve, haga clic en el botón MQTT de la barra lateral derecha para mostrarlo.
- El broker MQTT de su estación debe estar ejecutándose y ser accesible desde la máquina que ejecuta AetherSDR.
- Si aún no ha configurado las credenciales del broker, complete primero [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).

## Pasos

1. Abra el applet MQTT haciendo clic en el botón MQTT de la barra lateral derecha.
2. En el campo **Host**, confirme el nombre de host o la dirección IP del broker. Valor predeterminado: `localhost`.
3. En el campo **Port**, confirme el puerto del broker. Valor predeterminado: `1883`.
4. Si su broker requiere autenticación, ingrese los valores en los campos **User** y **Pass**.
5. En el campo **Topics**, ingrese una lista separada por comas de los temas a los que desea suscribirse. Para mostrar también el valor de un tema como superposición en el panadapter, antepóngale `*`. Ejemplo:
   ```
   *rotator/pos, *ant/selected, station/log
   ```
6. Si su broker usa TLS, marque **TLS**. El puerto cambia automáticamente a `8883`. Si necesita un certificado CA personalizado, ingrese la ruta del archivo en **CA cert**; déjelo en blanco para usar el conjunto de CA del sistema.
7. Haga clic en **Enable** para conectarse. La etiqueta del botón cambia a **On** y la etiqueta de estado muestra **Connected** en verde. Todos los ajustes se guardan en este punto.

## Función de cada control

| Control | Valor predeterminado | Rango válido / notas | Clave de configuración |
|---|---|---|---|
| **Host** | `localhost` | Nombre de host o IP del broker | `MqttHost` |
| **Port** | `1883` | 1–65535; cambia automáticamente a `8883` cuando TLS está habilitado | `MqttPort` |
| **User** | _(vacío)_ | Nombre de usuario opcional del broker | `MqttUser` |
| **Pass** | _(vacío)_ | Contraseña opcional del broker; oculta | `MqttPass` |
| **Topics** | _(vacío)_ | Lista de temas separados por comas; anteponer `*` para superponer en el panadapter | `MqttTopics` |
| **TLS** | Desactivado | Muestra/oculta la fila **CA cert**; cambia automáticamente el puerto entre `1883` y `8883` | `MqttTls` |
| **CA cert** | _(vacío)_ | Ruta al archivo de certificado CA; en blanco usa el conjunto de CA del sistema; visible solo cuando TLS está marcado | `MqttCaFile` |
| **Enable** | Desactivado | Conecta (On) o desconecta (Off); guarda todos los ajustes al conectar | — |
| **Message log** | — | Muestra hasta los últimos 50 mensajes recibidos como líneas `topic: value` | — |

## Consejos

- Se debe ingresar un tema sin el prefijo `*` para suscribirse; el `*` solo controla si el valor aparece en la superposición del panadapter. La suscripción en sí siempre está activa una vez que hace clic en **Enable**.
- El registro de mensajes muestra solo el último segmento de la ruta del tema (después de la `/` final) junto al valor, por lo que `rotator/pos` aparece como `pos: 180`.
- Los ajustes se escriben en el disco solo cuando hace clic en **Enable** para conectarse. Si edita los campos y cierra el applet sin conectarse, los cambios no se guardan.

## Solución de problemas

- **La etiqueta de estado muestra un mensaje de error en lugar de "Connected"** — El broker es inalcanzable o las credenciales son incorrectas. Verifique los valores de **Host**, **Port**, **User** y **Pass**, luego haga clic en **Enable** nuevamente.
- **El campo Topics acepta sus entradas pero no aparecen mensajes en el registro** — Confirme que el broker esté publicando exactamente en esas cadenas de tema. La coincidencia de temas MQTT distingue entre mayúsculas y minúsculas.
- **La casilla TLS está marcada pero la fila CA cert no es visible** — Alterne **TLS** a desactivado y luego a activado nuevamente para forzar la actualización de la fila.
- **El puerto no cambió a 8883 cuando marqué TLS** — El cambio automático solo se aplica cuando el valor actual del puerto es exactamente `1883`. Si ingresó un puerto personalizado, se conserva.

## Relacionados

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Superponer un valor MQTT en el panadapter (anteponer tema con *)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Habilitar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
- [Publicar un mensaje predefinido con un botón (ej. preajuste de rotador)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
