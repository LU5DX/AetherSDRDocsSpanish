# Recarga automática del registro ADIF cuando lo actualiza un programa de registro

Cuando el coloreado DXCC está activo, AetherSDR puede vigilar su archivo de registro ADIF y recargarlo automáticamente cada vez que su programa de registro guarda un nuevo QSO. Esto mantiene al día los colores de spots trabajados/confirmados/necesarios en el panadapter sin ninguna intervención manual.

## Antes de comenzar

- El coloreado DXCC debe estar habilitado y un archivo de registro ADIF debe estar ya cargado. Consulte [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su programa de registro debe escribir los QSO en el mismo archivo ADIF que AetherSDR tiene cargado.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Confirme que **DXCC Coloring** está activo (el interruptor aparece habilitado) y que **Log File (ADIF):** muestra la ruta de archivo correcta.
4. Haga clic en **Auto-Reload Log:** para habilitarlo.

AetherSDR comenzará a monitorear el archivo. Cada vez que el archivo cambie en disco, el registro ADIF se vuelve a leer y el coloreado DXCC en el panadapter se actualiza automáticamente.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **DXCC Coloring** | Interruptor principal. Colorea los spots según el estado de trabajado/confirmado/necesario basándose en el registro ADIF cargado. | `DxccColoringEnabled` |
| **Log File (ADIF):** | Abre un selector de archivos para elegir el archivo de registro ADIF. La ruta seleccionada se guarda de forma persistente. | `DxccAdifPath` |
| **Auto-Reload Log:** | Vuelve a leer el archivo ADIF cada vez que cambia en disco. | `DxccAutoReload` |

## Consejos

- Si su programa de registro sobreescribe el archivo ADIF en su lugar en cada guardado (comportamiento habitual en Log4OM, DXKeeper y similares), la recarga automática incorporará cada nuevo QSO en cuestión de segundos desde que se escriba.
- Deshabilitar **Auto-Reload Log:** no borra los datos del registro ya cargado. El coloreado DXCC continúa usando el último archivo leído correctamente hasta que realice una recarga manual o cambie el archivo.

## Solución de problemas

- **Los colores de los spots no se actualizan tras registrar un QSO** — Confirme que **Auto-Reload Log:** está habilitado en la pestaña **Display**. Verifique también que su programa de registro está escribiendo en el archivo exacto que se muestra en **Log File (ADIF):**. Algunos programas de registro escriben en un archivo temporal y luego lo renombran; esto puede no activar una recarga en todas las plataformas. En ese caso, deshabilite **Auto-Reload Log:**, vuelva a abrir `Settings > SpotHub...` y haga clic en **Log File (ADIF):** para recargar manualmente.
- **El interruptor DXCC Coloring está disponible pero no produce cambios de color** — El recuento de QSO importados que muestra el indicador de estadísticas DXCC será cero si la ruta del archivo ADIF no es válida o el archivo no es legible. Vuelva a seleccionar el archivo mediante **Log File (ADIF):**.

## Relacionados

- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Ajustar densidad, posición, tamaño de fuente y tiempo de vida de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Descripción general de SpotHub](overview.md)
