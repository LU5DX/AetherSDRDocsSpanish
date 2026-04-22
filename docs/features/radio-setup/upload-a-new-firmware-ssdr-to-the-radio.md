# Cargar un nuevo firmware .ssdr en la radio

Use esta página para cargar una nueva imagen de firmware en su FLEX-8600 desde un archivo `.ssdr` local. Realice este procedimiento para actualizar el firmware de la radio manualmente, sin depender de una verificación de actualizaciones por internet.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña `Radio` no es accesible sin una conexión activa.
- Descargue el archivo de firmware `.ssdr` en su computadora antes de abrir el diálogo.
- No desconecte la radio ni cierre el diálogo mientras la carga esté en progreso.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña `Radio`.
3. Haga clic en `Browse .ssdr...` para abrir un selector de archivos.
4. Navegue hasta su archivo de firmware `.ssdr`, selecciónelo y confirme la selección.
5. Haga clic en `Upload Firmware`.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga se completó antes de realizar cualquier otra acción.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| `Check for Update` | Botón | Consulta a la radio si hay actualizaciones de firmware disponibles. |
| `Browse .ssdr...` | Botón | Abre un diálogo de archivo para seleccionar una imagen de firmware `.ssdr` local. |
| `Upload Firmware` | Botón | Inicia la carga del firmware. Durante la transferencia aparecen y se actualizan una barra de progreso y un texto de estado. |

## Consejos

- Use `Check for Update` primero si no está seguro de si el firmware actual ya está al día.
- El área de estado del firmware debajo de `Upload Firmware` aparece vacía hasta que comienza una carga. Si el texto deja de actualizarse de forma inesperada, no desconecte la radio; espere para confirmar si la transferencia se completó.

## Solución de problemas

- **`Upload Firmware` no tiene efecto** — Confirme que se ha seleccionado un archivo con `Browse .ssdr...` primero. El botón requiere que se haya establecido una ruta de archivo antes de continuar.
- **La carga comienza pero no se completa** — No cierre el diálogo ni desconecte la radio. Verifique que la conexión de red entre su computadora y la radio sea estable. Si la carga falla, puede intentarlo nuevamente haciendo clic en `Upload Firmware` sin volver a explorar los archivos, siempre que la ruta del archivo aún se muestre.

## Relacionado

- [Verificar número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
