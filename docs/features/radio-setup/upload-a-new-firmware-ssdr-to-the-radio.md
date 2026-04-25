# Cargar un nuevo archivo de firmware .ssdr en la radio

Esta página explica cómo cargar un archivo de imagen de firmware en su FLEX-8600 usando el cargador integrado de AetherSDR. Utilice este procedimiento cuando FlexRadio publique un nuevo paquete de firmware `.ssdr` y desee actualizar la radio sin salir de AetherSDR.

## Antes de comenzar

- La radio debe estar conectada. La pestaña `Radio` de Radio Setup solo funciona cuando AetherSDR tiene una conexión de radio activa.
- Descargue el archivo de firmware `.ssdr` desde FlexRadio a su computadora antes de abrir el diálogo.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña `Radio`.
3. Haga clic en `Browse .ssdr...` para abrir un diálogo de selección de archivos.
4. Navegue hasta el archivo `.ssdr` que descargó y selecciónelo. El nombre del archivo se mostrará junto al botón.
5. Haga clic en `Upload Firmware`.
6. Observe la barra de progreso y el texto de estado debajo del botón. La carga se completa cuando el texto de estado indica que fue exitosa.
7. Reinicie la radio según las instrucciones de las notas de la versión del firmware para aplicar el nuevo firmware.

## Consejos

- Si desea verificar si hay una versión de firmware más reciente disponible antes de obtener el archivo manualmente, haga clic en `Check for Update`. AetherSDR consultará las actualizaciones de firmware disponibles e informará el resultado en el área de estado.
- Los campos `Radio SN`, `HW Version` y `Model` en la misma pestaña confirman que está viendo la radio correcta antes de cargar.

## Solución de problemas

- **Upload Firmware no responde** — Aún no se ha seleccionado ningún archivo `.ssdr`. Haga clic primero en `Browse .ssdr...`, confirme que el archivo aparece y luego haga clic en `Upload Firmware`.
- **La barra de progreso se detiene o el estado muestra un error** — Verifique que la radio siga conectada y sea accesible en la red. Revise `Settings > Network...` para detectar problemas de conectividad y luego reintente la carga desde el paso 3.
- **Se actualizó la radio incorrecta** — Confirme que los indicadores `Radio SN` y `Model` en la pestaña Radio coincidan con la radio deseada antes de hacer clic en `Upload Firmware`.

## Relacionados

- [Consultar el número de serie, la versión de hardware, la región y las opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
- [Cambiar la radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
