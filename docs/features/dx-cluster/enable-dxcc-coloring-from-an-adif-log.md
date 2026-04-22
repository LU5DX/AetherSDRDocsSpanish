# Activar la coloración DXCC desde un registro ADIF

La coloración DXCC superpone etiquetas de spots en el panadapter con colores que reflejan el estado de trabajado, confirmado o necesitado para cada entidad. Para gestionar esa coloración, AetherSDR lee un archivo de registro ADIF que usted exporta desde su software de registro.

## Antes de comenzar

- Tiene un archivo de registro ADIF (.adi o .adif) exportado desde su software de registro.
- La superposición de spots está activa: `IsSpotsEnabled` está habilitado. Si los spots no son visibles en el panadapter, la coloración DXCC no tendrá ningún efecto visible.
- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, etc.) está conectada y entregando spots.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en **DXCC Coloring** para habilitarlo. El interruptor debe estar activo para que se aplique la coloración.
4. Haga clic en **Log File (ADIF):** para abrir un explorador de archivos y, a continuación, seleccione su archivo de registro ADIF.
5. Confirme que el indicador de estadísticas DXCC situado debajo del control muestra un número de QSOs importados distinto de cero. Esto confirma que el archivo se analizó correctamente.
6. Si su software de registro actualiza el archivo ADIF automáticamente mientras AetherSDR está en ejecución, haga clic en **Auto-Reload Log:** para habilitarlo. AetherSDR volverá a leer el archivo cada vez que cambie en el disco.

## Qué hace cada control

| Control | Qué hace | Clave persistida |
|---|---|---|
| **DXCC Coloring** (interruptor) | Interruptor principal. Habilita o deshabilita la coloración de spots basada en DXCC en el panadapter. | `DxccColoringEnabled` |
| **Log File (ADIF):** (botón) | Abre un selector de archivos. La ruta seleccionada se guarda y el archivo se analiza de inmediato. | `DxccAdifPath` |
| **Auto-Reload Log:** (interruptor) | Vuelve a leer el archivo ADIF automáticamente cada vez que cambia en el disco. | `DxccAutoReload` |

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra el número de QSOs importados desde el archivo ADIF. Si marca cero tras la carga, el archivo puede estar vacío o en un formato no compatible.
- Si su programa de registro añade entradas al archivo ADIF en tiempo real (habitual en Log4OM, DXKeeper y aplicaciones similares), habilite **Auto-Reload Log:** para que su estado de trabajado se mantenga actualizado sin necesidad de reabrir el diálogo.
- La coloración DXCC funciona junto con los colores de spots por fuente. Si **Override Colors:** también está activo, el color de anulación tiene prioridad. Deshabilite **Override Colors:** si la coloración DXCC no aparece como se esperaba.

## Solución de problemas

- **Las estadísticas DXCC muestran cero QSOs tras seleccionar el archivo** — Es posible que el archivo no tenga un formato ADIF válido o que esté vacío. Vuelva a exportar desde su software de registro e inténtelo de nuevo.
- **Los colores de los spots en el panadapter no cambian después de habilitar DXCC Coloring** — Compruebe que **Override Colors:** no esté activo en la pestaña **Display**; anulará la coloración DXCC. Confirme también que **Spots:** está habilitado.
- **Los colores no se actualizan al registrar un nuevo QSO** — Habilite **Auto-Reload Log:** para que AetherSDR detecte los cambios en el archivo automáticamente.

## Relacionado

- [Recarga automática del registro ADIF cuando lo actualiza un programa de registro](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Seleccionar colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Descripción general de SpotHub](overview.md)
