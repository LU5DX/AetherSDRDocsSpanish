# Suscribirse a tópicos de rotor / conmutador de antena

Use el applet MQTT para suscribirse a los tópicos publicados por su controlador de rotor o conmutador de antena. Los valores entrantes aparecen en el registro de mensajes y, si antepone `*` a un tópico, como superposición (overlay) en el panadapter.

## Antes de comenzar

- El applet MQTT debe estar visible. Si no lo ve, haga clic en el botón MQTT de la barra lateral derecha para mostrarlo.
- El broker MQTT de su estación debe estar en ejecución y ser accesible desde la máquina que ejecuta AetherSDR.
- Si aún no ha configurado las credenciales del broker, complete primero [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).

## Pasos

1. Abra el applet MQTT haciendo clic en el botón MQTT de la barra lateral derecha.
2. En el campo **Host**, confirme el nombre de host o la dirección IP del broker. Valor predeterminado: `localhost`.
3. En el campo **Port**, confirme el puerto del broker. Valor predeterminado: `1883`.
4. Si su broker requiere autenticación, ingrese los valores en los campos **User** y **Pass**.
5. En el campo **Topics**, ingrese una lista de tópicos separados por comas a los que desea suscribirse. Para mostrar además el valor de un tópico como superposición en el panadapter, anteponga `*`. Ejemplo:
   ```
   *rotator/pos, *ant/selected, station/log
   ```
6. Si su broker usa TLS, marque **TLS**. El puerto cambia automáticamente a `8883`. Si necesita un certificado CA personalizado, ingrese la ruta del archivo en **CA cert**; déjelo en blanco para usar el paquete CA del sistema.
7. Haga clic en **Enable** para conectarse. La etiqueta del botón cambia a **On** y la etiqueta de estado muestra **Connected** en verde. Todos los ajustes se guardan en este momento.

## Qué hace cada control

| Control | Predeterminado | Rango válido / notas | Clave de ajuste |
|---|---|---|---|
| **Host** | `localhost` | Nombre de host o IP del broker | `MqttHost` |
| **Port** | `1883` | 1–65535; cambia automáticamente a `8883` cuando TLS está habilitado | `MqttPort` |
| **User** | _(vacío)_ | Nombre de usuario del broker (opcional) | `MqttUser` |
| **Pass** | _(vacío)_ | Contraseña del broker (opcional); enmascarada | `MqttPass` |
| **Topics** | _(vacío)_ | Lista de tópicos separados por comas; anteponga `*` para superponer en el panadapter | `MqttTopics` |
| **TLS** | Off | Muestra/oculta la fila **CA cert**; alterna automáticamente el puerto entre `1883` y `8883` | `MqttTls` |
| **CA cert** | _(vacío)_ | Ruta al archivo de certificado CA; en blanco usa el paquete CA del sistema; visible solo cuando TLS está marcado | `MqttCaFile` |
| **Enable** | Off | Conecta (On) o desconecta (Off); guarda todos los ajustes al conectar | — |
| **Message log** | — | Muestra hasta los últimos 50 mensajes recibidos en formato `topic: value` | — |

## Consejos

- Un tópico debe ingresarse sin el prefijo `*` para poder suscribirse a él; el `*` solo controla si el valor aparece en la superposición del panadapter. La suscripción en sí siempre está activa una vez que hace clic en **Enable**.
- El registro de mensajes muestra únicamente el último segmento de la ruta del tópico (después de la `/` final) junto al valor, por lo que `rotator/pos` aparece como `pos: 180`.
- Los ajustes se escriben en disco solo cuando hace clic en **Enable** para conectarse. Si edita los campos y cierra el applet sin conectarse, los cambios no se guardarán.

## Solución de problemas

- **La etiqueta de estado muestra un mensaje de error en lugar de "Connected"** — El broker no es accesible o las credenciales son incorrectas. Verifique los valores de **Host**, **Port**, **User** y **Pass**, luego haga clic en **Enable** nuevamente.
- **El campo Topics acepta las entradas pero no aparecen mensajes en el registro** — Confirme que el broker esté publicando exactamente en esas cadenas de tópicos. La coincidencia de tópicos MQTT distingue entre mayúsculas y minúsculas.
- **La casilla TLS está marcada pero la fila CA cert no es visible** — Desactive y vuelva a activar **TLS** para forzar la actualización de la fila.
- **El puerto no cambió a 8883 al marcar TLS** — El cambio automático solo se aplica cuando el valor del puerto actual es exactamente `1883`. Si ingresó un puerto personalizado, este se conserva.

## Relacionados

- [Conectarse a un broker MQTT de estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Superponer un valor MQTT en el panadapter (anteponer * al tópico)](overlay-an-mqtt-value-on-the-panadapter-prefix-topic-with.md)
- [Habilitar TLS con un certificado CA personalizado](enable-tls-with-a-custom-ca-certificate.md)
- [Publicar un mensaje predefinido con un botón (p. ej., posición preestablecida de rotor)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
