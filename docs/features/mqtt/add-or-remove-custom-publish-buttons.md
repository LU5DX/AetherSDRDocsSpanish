# Agregar o eliminar botones de publicación personalizados

El applet de MQTT admite hasta 12 botones de publicación definidos por el usuario. Cada botón envía una carga útil fija a un tema fijo al hacer clic en él. Esta página explica cómo agregar nuevos botones, editar los existentes y eliminar los que ya no necesite.

## Antes de comenzar

- El applet de MQTT debe estar visible. Si no lo está, haga clic en el botón MQTT de la bandeja en la barra lateral derecha para mostrarlo.
- No es necesario estar conectado al broker para editar botones. Sin embargo, los botones solo publican cuando el applet está conectado (el estado muestra "Connected").
- Las definiciones de los botones se almacenan en `MqttButtons` y persisten entre sesiones.

## Pasos

### Agregar un botón

1. En el applet de MQTT, haga clic en **Edit**. El área de botones entra en modo de edición: los botones existentes cambian de apariencia y aparece un mosaico **+**.
2. Haga clic en el mosaico **+**.
3. En el diálogo que se abre, ingrese una etiqueta, un tema y una carga útil para el nuevo botón.
4. Confirme el diálogo.
5. Haga clic en **Done** para salir del modo de edición.

### Editar un botón existente

1. Haga clic en **Edit**.
2. Haga clic en el botón que desea modificar. Se abre un diálogo de edición que muestra la etiqueta, el tema y la carga útil actuales.
3. Cambie los valores según sea necesario y confirme.
4. Haga clic en **Done**.

### Eliminar un botón

1. Haga clic en **Edit**.
2. Haga clic con el botón derecho en el botón que desea eliminar.
3. Haga clic en **Remove** en el menú contextual que aparece.
4. Haga clic en **Done**.

## Qué hace cada control

| Control | Predeterminado | Notas |
|---|---|---|
| **Edit** / **Done** | **Edit** | Alterna el modo de edición. En modo de edición, hacer clic en un botón abre el diálogo de edición; hacer clic con el botón derecho muestra la opción Remove; el mosaico **+** está visible. |
| Botones de publicación | — | Cada botón publica su carga útil configurada en su tema configurado. Activos solo mientras esté conectado. Hasta 12 botones. Almacenados en `MqttButtons`. |
| Mosaico **+** | — | Visible solo en modo de edición. Abre el diálogo para agregar botones. Se deshabilita cuando ya existen 12 botones. |

## Consejos

- Los tooltips de los botones muestran el tema de destino y la carga útil cuando el applet está en modo normal (`topic → payload`). En modo de edición muestran la misma información con el prefijo "Click to edit".
- Los botones están inactivos cuando el applet está desconectado. Conéctese primero y luego use los botones para publicar.
- Si necesita publicar en el mismo tema con diferentes cargas útiles, cree un botón por cada carga útil.

## Solución de problemas

- **Al hacer clic en un botón de publicación no ocurre nada** — El applet no está conectado. Verifique que la etiqueta de estado indique "Connected". Si indica "Disconnected" o un mensaje de error, haga clic en **Enable** para conectarse. Consulte [Conectarse al broker MQTT de una estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- **El mosaico + no aparece** — Ya tiene 12 botones, que es el máximo. Elimine al menos un botón antes de agregar otro.
- **Los cambios en los botones se pierden después de reiniciar** — Los cambios se guardan automáticamente al confirmar el diálogo de edición. Si el applet se cerró inesperadamente antes de guardar, se restaura el valor anterior de `MqttButtons`.

## Relacionado

- [Conectarse al broker MQTT de una estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Publicar un mensaje predefinido con un botón (p. ej., preajuste de rotador)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Descripción general de MQTT](overview.md)
