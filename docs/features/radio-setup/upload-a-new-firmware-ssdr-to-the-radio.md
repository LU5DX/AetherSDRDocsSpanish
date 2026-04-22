# Cargar un nuevo firmware .ssdr en la radio

Esta página explica cómo cargar un archivo de imagen de firmware en su FLEX-8600 usando el cargador integrado de AetherSDR. Realice este proceso para actualizar la radio a una versión de firmware específica sin usar SmartSDR for Windows.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña `Radio (tab)` en Radio Setup requiere una conexión activa con la radio.
- Obtenga el archivo de firmware `.ssdr` correcto para su FLEX-8600 y anote su ubicación en el equipo.
- No interrumpa la alimentación de la radio ni cierre AetherSDR durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña `Radio (tab)` si no está seleccionada.
3. Haga clic en `Browse .ssdr...` para abrir el selector de archivos.
4. Navegue hasta su archivo `.ssdr`, selecciónelo y confirme.
5. Haga clic en `Upload Firmware`.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga se completó antes de realizar cualquier otra acción.
7. Reinicie la radio cuando se le indique o cuando el estado de la carga confirme la finalización.

## Consejos

- Si desea que AetherSDR verifique si hay una actualización disponible en lugar de proporcionar su propio archivo, haga clic en `Check for Update` en vez de `Browse .ssdr...`.
- El área de estado del firmware aparece en blanco hasta que comienza una carga. La barra de progreso y el texto de resultado aparecen una vez que se hace clic en `Upload Firmware`.

## Solución de problemas

- **"Browse .ssdr..." no responde o el diálogo se cierra de inmediato** — Verifique que esté conectado a la radio. Los controles de la pestaña Radio solo están activos con una conexión de radio establecida.
- **La carga se detiene o falla a mitad del proceso** — No cierre el diálogo. Compruebe que la conexión de red entre su equipo y la radio sea estable. Si usa una VPN o un enlace remoto, una conexión local por cable es más confiable para transferencias de firmware.
- **La radio no reinicia después de la carga** — Realice un ciclo de encendido manual del FLEX-8600 desde el panel frontal y vuelva a conectar AetherSDR.

## Relacionado

- [Verificar el número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
