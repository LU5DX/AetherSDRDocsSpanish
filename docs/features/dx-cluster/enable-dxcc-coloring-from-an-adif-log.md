# Habilitar coloración DXCC desde un registro ADIF

La coloración DXCC permite que AetherSDR resalte los spots del panadapter en diferentes colores según si ya ha trabajado, confirmado o aún necesita una entidad DXCC. Para activarla, indique a AetherSDR la ruta de un archivo de registro ADIF exportado desde su software de registro de QSOs.

## Antes de comenzar

- Tiene un archivo de registro ADIF (.adi o .adif) exportado desde su logger.
- Al menos una fuente de spots está activa y los spots aparecen en el panadapter. La coloración DXCC solo afecta la forma en que se colorean los spots existentes; no crea spots por sí sola.
- La visualización de spots está habilitada: el interruptor `IsSpotsEnabled` en SpotHub está activado.

## Pasos

1. Vaya a `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **DXCC Coloring** para habilitarlo. El interruptor debe estar activo antes de que se utilice la ruta del archivo de registro.
4. Haga clic en **Log File (ADIF):**. Se abre un navegador de archivos.
5. Navegue hasta su archivo ADIF y selecciónelo. La ruta se guarda en `DxccAdifPath`.
6. Confirme que el indicador de estadísticas DXCC debajo de los controles muestra un número de QSOs importados distinto de cero. Esto confirma que el archivo se leyó correctamente.
7. Si desea que AetherSDR vuelva a leer el archivo automáticamente cada vez que su logger lo actualice, habilite **Auto-Reload Log:**. Esto se guarda en `DxccAutoReload`.

## Qué hace cada control

| Control | Función | Clave de configuración |
|---|---|---|
| **DXCC Coloring** | Interruptor principal. Colorea los spots según el estado trabajado/confirmado/necesitado de la entidad DXCC. | `DxccColoringEnabled` |
| **Log File (ADIF):** | Abre un navegador de archivos para seleccionar su registro ADIF. La ruta elegida se conserva. | `DxccAdifPath` |
| **Auto-Reload Log:** | Vuelve a leer el archivo ADIF automáticamente cuando cambia en el disco. Útil cuando un logger escribe en el archivo en tiempo real. | `DxccAutoReload` |

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra el número de QSOs importados desde el archivo ADIF. Si indica cero después de seleccionar un archivo, es posible que el archivo esté vacío o en un formato no compatible.
- Si su logger añade entradas continuamente al archivo ADIF durante una sesión, habilite **Auto-Reload Log:** para que la coloración se mantenga actualizada sin necesidad de volver a abrir SpotHub.
- La coloración DXCC se aplica sobre los colores de la fuente de spots. Si **Override Colors:** también está habilitado, el color de anulación tiene precedencia. Deshabilite **Override Colors:** si la coloración DXCC no es visible.

## Solución de problemas

- **Las estadísticas DXCC muestran 0 QSOs después de seleccionar un archivo** — Es posible que el archivo no sea ADIF válido, esté vacío o esté abierto en modo exclusivo por otra aplicación. Cierre cualquier bloqueo exclusivo del archivo en su logger, vuelva a exportarlo si es necesario y seleccione el archivo de nuevo.
- **Los colores de los spots no cambian después de habilitar DXCC Coloring** — Compruebe que **Override Colors:** en la misma pestaña **Display** no esté activo. Override Colors tiene precedencia sobre la coloración DXCC. Confirme también que **Spots:** esté habilitado (`IsSpotsEnabled`).
- **Auto-Reload Log: no detecta los nuevos QSOs** — Algunos loggers escriben en un archivo temporal y luego lo renombran, lo que puede no activar una notificación de cambio de archivo. En ese caso, deshabilite **Auto-Reload Log:** y seleccione el archivo manualmente después de cada sesión.

## Relacionado

- [Recarga automática del registro ADIF cuando lo actualiza un logger](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Descripción general de SpotHub](overview.md)
