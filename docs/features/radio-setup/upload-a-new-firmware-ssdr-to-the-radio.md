# Cargar un nuevo firmware .ssdr en la radio

Use esta página para cargar una nueva imagen de firmware en su radio Flex. Necesitará un archivo de firmware `.ssdr` en su equipo local antes de comenzar.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La pestaña Radio en Radio Setup no está disponible sin una conexión activa.
- Descargue el archivo de firmware `.ssdr` de destino y anote su ubicación en el disco.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Browse .ssdr...** para abrir un selector de archivos, luego seleccione su archivo de firmware `.ssdr` y confirme.
4. Haga clic en **Upload Firmware**.
5. Observe el indicador de estado del firmware debajo del botón. Permanece vacío hasta que comienza la carga, luego muestra el progreso y un mensaje de resultado al finalizar.
6. Cierre el cuadro de diálogo cuando el indicador de estado confirme que la carga finalizó.

## Consejos

- Si desea que AetherSDR confirme qué versión de firmware tiene actualmente la radio antes de seleccionar un archivo, consulte **HW Version** en el grupo Radio Information de la misma pestaña.
- El botón **Check for Update** consulta las actualizaciones de firmware disponibles si su radio tiene acceso a internet configurado.

## Solución de problemas

- **Browse .ssdr... se abre pero no aparece ningún archivo en el selector** — Confirme que el archivo tenga la extensión `.ssdr`. El selector de archivos filtra por ese tipo.
- **Upload Firmware no responde después de hacer clic en Browse .ssdr...** — Aún no se ha seleccionado ningún archivo. Haga clic en **Browse .ssdr...** nuevamente y confirme un archivo antes de hacer clic en **Upload Firmware**.
- **El indicador de estado muestra un mensaje de error** — Verifique que la radio siga conectada (`Settings > Connect to Radio...`) y que ningún otro cliente tenga una sesión exclusiva activa. Luego reintente desde el paso 3.

## Relacionados

- [Consultar el número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
