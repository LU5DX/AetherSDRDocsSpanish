# Recarga automática del registro ADIF al actualizarlo con un programa de log

Cuando el coloreado DXCC está activo, AetherSDR puede vigilar su archivo de registro ADIF y recargarlo automáticamente cada vez que su programa de log escribe un nuevo QSO. Esto mantiene el estado trabajado/confirmado/necesario actualizado en el panadapter sin intervención manual.

## Antes de comenzar

- El coloreado DXCC debe estar habilitado y ya debe haber un archivo ADIF seleccionado. Consulte [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su programa de log debe escribir las actualizaciones en la misma ruta de archivo ADIF almacenada en `DxccAdifPath`.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Confirme que `DXCC Coloring` está habilitado (el botón de alternancia aparece activo).
4. Confirme que `Log File (ADIF):` muestra la ruta de archivo correcta.
5. Haga clic en `Auto-Reload Log:` para habilitarlo.

El botón de alternancia activa la supervisión de cambios de archivo en la ruta almacenada en `DxccAdifPath`. Cada vez que su programa de log guarda el archivo, AetherSDR lo vuelve a leer y actualiza el coloreado DXCC en el panadapter.

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| `DXCC Coloring` | Alternancia principal; colorea los spots según el estado trabajado/confirmado/necesario. Debe estar activo para que la recarga automática tenga algún efecto. | `DxccColoringEnabled` |
| `Log File (ADIF):` | Abre un selector de archivos y almacena la ruta ADIF seleccionada. | `DxccAdifPath` |
| `Auto-Reload Log:` | Supervisa el archivo ADIF en busca de cambios y lo recarga automáticamente cuando el archivo se actualiza. | `DxccAutoReload` |

## Consejos

- Si su programa de log escribe en un archivo temporal y luego lo renombra sobre la ruta de destino, la recarga se activará al momento del renombrado, siempre que la ruta final coincida con `DxccAdifPath`.
- Deshabilitar `DXCC Coloring` mientras `Auto-Reload Log:` está activo no afecta el estado del botón de alternancia; el monitor de archivos reanuda las actualizaciones de coloreado si vuelve a habilitar `DXCC Coloring` sin cambiar ninguna otra configuración.

## Resolución de problemas

- **Los spots no se actualizan después de registrar un nuevo QSO** — Confirme que `Auto-Reload Log:` está habilitado y que `Log File (ADIF):` muestra exactamente el archivo en el que su programa de log está escribiendo. Si su programa de log escribe en una ruta diferente o en un archivo temporal que nunca se renombra a la ruta configurada, AetherSDR no detectará el cambio. Vuelva a seleccionar el archivo mediante `Log File (ADIF):` después de confirmar la ruta correcta.
- **El coloreado DXCC no refleja el registro recargado** — Verifique que `DXCC Coloring` está habilitado. La recarga automática no tiene ningún efecto visible mientras la alternancia principal está desactivada.

## Relacionado

- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Ajustar la densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
