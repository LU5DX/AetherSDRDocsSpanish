# Cargar un nuevo archivo de firmware .ssdr en la radio

Esta página explica cómo cargar un archivo de imagen de firmware en su FLEX-8600 mediante el diálogo Radio Setup. Realice este procedimiento para actualizar la radio a una versión de firmware específica sin utilizar la verificación de actualizaciones automática.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Radio (tab) no se poblará correctamente sin una conexión activa.
- Obtenga el archivo de firmware `.ssdr` de FlexRadio y tome nota de dónde está guardado en su computadora.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Browse .ssdr...** para abrir un selector de archivos.
4. Navegue hasta el archivo `.ssdr` en su computadora, selecciónelo y confirme.
5. Haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga se completó antes de realizar cualquier otra acción.
7. Reinicie la radio según las instrucciones de las notas de la versión del firmware para aplicar el nuevo firmware.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón | Consulta automáticamente si hay actualizaciones de firmware disponibles. Utilice esta opción en lugar de **Browse .ssdr...** si desea que AetherSDR encuentre la actualización por usted. |
| **Browse .ssdr...** | Botón | Abre un diálogo de archivo para seleccionar una imagen de firmware `.ssdr` local. |
| **Upload Firmware** | Botón | Inicia la carga utilizando el archivo seleccionado con **Browse .ssdr...**. Una barra de progreso y texto de estado aparecen debajo y se actualizan conforme avanza la transferencia. |

## Consejos

- Si solo desea verificar si existe una versión más reciente en lugar de cargar un archivo específico, utilice **Check for Update** en lugar del flujo de trabajo manual de exploración y carga.
- El área de estado del firmware está vacía hasta que comienza una carga. Si no ve ninguna barra de progreso después de hacer clic en **Upload Firmware**, confirme que se haya seleccionado un archivo con **Browse .ssdr...** primero.

## Solución de problemas

- **Upload Firmware no hace nada** — No se ha seleccionado ningún archivo `.ssdr`. Haga clic primero en **Browse .ssdr...**, seleccione el archivo y luego haga clic en **Upload Firmware**.
- **Los controles de la pestaña Radio no están poblados o aparecen deshabilitados** — AetherSDR no está conectado a la radio. Establezca una conexión mediante `Settings > Connect to Radio...` antes de abrir Radio Setup.

## Relacionados

- [Verificar el número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
