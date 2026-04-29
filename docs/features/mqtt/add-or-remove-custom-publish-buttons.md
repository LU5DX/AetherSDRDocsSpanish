# Agregar o eliminar botones de publicación personalizados

El applet de MQTT admite hasta 12 botones de publicación definidos por el usuario. Cada botón envía una carga útil fija a un tema fijo al hacer clic. Esta página explica cómo agregar nuevos botones, editar los existentes y eliminar los que ya no necesita.

## Antes de comenzar

- El applet de MQTT debe estar visible. Si no lo está, haga clic en el botón de bandeja MQTT en la barra lateral derecha para mostrarlo.
- No es necesario estar conectado al broker para editar botones. Sin embargo, los botones solo publican cuando el applet está conectado (el estado muestra "Connected").
- Las definiciones de los botones se almacenan en `MqttButtons` y persisten entre sesiones.

## Pasos

### Agregar un botón

1. En el applet de MQTT, haga clic en **Edit**. El área de botones entra en modo de edición: los botones existentes cambian de apariencia y aparece una ficha **+**.
2. Haga clic en la ficha **+**.
3. En el cuadro de diálogo que se abre, ingrese una etiqueta, un tema y una carga útil para el nuevo botón.
4. Confirme el cuadro de diálogo.
5. Haga clic en **Done** para salir del modo de edición.

### Editar un botón existente

1. Haga clic en **Edit**.
2. Haga clic en el botón que desea cambiar. Se abre un cuadro de diálogo de edición con la etiqueta, el tema y la carga útil actuales.
3. Cambie los valores según sea necesario y confirme.
4. Haga clic en **Done**.

### Eliminar un botón

1. Haga clic en **Edit**.
2. Haga clic con el botón derecho en el botón que desea eliminar.
3. Haga clic en **Remove** en el menú contextual que aparece.
4. Haga clic en **Done**.

## Qué hace cada control

| Control | Valor predeterminado | Notas |
|---|---|---|
| **Edit** / **Done** | **Edit** | Alterna el modo de edición. En modo de edición, hacer clic en un botón abre el cuadro de diálogo de edición; hacer clic derecho muestra la opción Remove; la ficha **+** es visible. |
| Botones de publicación | — | Cada botón publica su carga útil configurada en su tema configurado. Activo solo mientras está conectado. Hasta 12 botones. Almacenados en `MqttButtons`. |
| Ficha **+** | — | Visible solo en modo de edición. Abre el cuadro de diálogo para agregar un botón. Se deshabilita una vez que existen 12 botones. |

## Consejos

- Los tooltips de los botones muestran el tema de destino y la carga útil cuando el applet está en modo normal (`topic → payload`). En modo de edición muestran la misma información precedida por "Click to edit".
- Los botones están inactivos cuando el applet está desconectado. Conéctese primero y luego use los botones para publicar.
- Si necesita publicar en el mismo tema con diferentes cargas útiles, cree un botón por cada carga útil.

## Solución de problemas

- **Hacer clic en un botón de publicación no hace nada** — El applet no está conectado. Verifique que la etiqueta de estado muestre "Connected". Si muestra "Disconnected" o un mensaje de error, haga clic en **Enable** para conectarse. Consulte [Conectarse al broker MQTT de una estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md).
- **La ficha + no aparece** — Ya tiene 12 botones, que es el máximo. Elimine al menos un botón antes de agregar otro.
- **Los cambios en los botones se pierden después de reiniciar** — Los cambios se guardan automáticamente al confirmar el cuadro de diálogo de edición. Si el applet se cerró inesperadamente antes de guardar, se restaura el valor anterior de `MqttButtons`.

## Relacionados

- [Conectarse al broker MQTT de una estación](../../getting-started/setup/connect-to-a-station-mqtt-broker.md)
- [Publicar un mensaje predefinido con un botón (p. ej., preajuste de rotador)](publish-a-canned-message-with-a-button-e-g-rotator-preset.md)
- [Descripción general de MQTT](overview.md)
