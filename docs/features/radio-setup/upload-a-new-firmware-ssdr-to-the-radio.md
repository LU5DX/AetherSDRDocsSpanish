# Cargar un nuevo archivo de firmware .ssdr en la radio

Esta página explica cómo cargar un archivo de imagen de firmware en su FLEX-8600 usando AetherSDR. Realice este procedimiento para actualizar la radio a una nueva versión de firmware que haya descargado como archivo `.ssdr`.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de la pestaña Radio no están disponibles sin una conexión activa.
- Descargue el archivo de firmware `.ssdr` en su computadora antes de abrir este diálogo.
- No transmita ni desconecte la radio durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Browse .ssdr...** para abrir el selector de archivos.
4. Navegue hasta su archivo de firmware `.ssdr`, selecciónelo y confirme la selección.
5. Haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado que aparece debajo del botón. Espere hasta que el estado indique que la carga se ha completado antes de realizar cualquier otra acción.

## Consejos

- El área de estado del firmware aparece en blanco hasta que comienza una carga. Una vez iniciada, muestra el progreso y el resultado. Si el texto de estado no se actualiza después de hacer clic en **Upload Firmware**, verifique que el archivo seleccionado tenga la extensión `.ssdr` y que la radio siga conectada.
- Puede verificar la versión de hardware actual antes y después de la carga mediante el indicador **HW Version** en la misma pestaña **Radio**.

## Solución de problemas

- **Browse .ssdr... se abre pero no hay archivos seleccionables** — El selector de archivos filtra por archivos `.ssdr`. Confirme que el archivo descargado tenga esa extensión y que no haya sido renombrado ni extraído de un archivo comprimido.
- **Upload Firmware no responde** — Confirme que AetherSDR esté conectado a la radio. Los controles de la pestaña Radio requieren una conexión activa. Use `Settings > Connect to Radio...` si es necesario y vuelva a intentarlo.
- **La carga parece detenerse** — No interrumpa la conexión. Los archivos de firmware de gran tamaño requieren tiempo para transferirse. Espere a que el texto de estado muestre un resultado antes de tomar cualquier acción.

## Relacionados

- [Verificar número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
