# Recarga automática del registro ADIF cuando lo actualiza un programa de registro

Cuando el coloreado DXCC está habilitado, AetherSDR lee su registro ADIF una vez al inicio. Habilitar la recarga automática indica a AetherSDR que vuelva a leer el archivo cada vez que su programa de registro lo actualice, de modo que el coloreado de trabajados/confirmados/necesarios en el panadapter se mantenga actualizado sin intervención manual.

## Antes de comenzar

- El coloreado DXCC debe estar habilitado y un archivo de registro ADIF ya debe estar cargado. Consulte [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su programa de registro debe escribir las actualizaciones en la misma ruta de archivo ADIF almacenada en `DxccAdifPath`.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Confirme que `DXCC Coloring` esté habilitado (el interruptor muestra su estado activo).
4. Confirme que `Log File (ADIF):` muestre la ruta de archivo correcta.
5. Haga clic en `Auto-Reload Log:` para habilitarlo.

AetherSDR ahora supervisa el archivo en `DxccAdifPath` en busca de cambios. Cada vez que su programa de registro escribe un nuevo QSO, AetherSDR vuelve a leer el archivo y actualiza el coloreado de spots en el panadapter.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| `DXCC Coloring` | Interruptor principal para colorear spots según el estado de trabajado/confirmado/necesario. La recarga automática no tiene efecto cuando está desactivado. | `DxccColoringEnabled` |
| `Log File (ADIF):` | Abre un selector de archivos para elegir el registro ADIF. La ruta seleccionada se guarda de forma persistente. | `DxccAdifPath` |
| `Auto-Reload Log:` | Interruptor. Cuando está habilitado, AetherSDR supervisa el archivo en busca de cambios y lo recarga automáticamente. | `DxccAutoReload` |

## Sugerencias

- Si su programa de registro escribe en un archivo temporal y luego lo renombra en su lugar definitivo, el supervisor de archivos puede no detectar cada guardado. Configure su programa de registro para que escriba directamente en el archivo de la ruta almacenada en `DxccAdifPath` para una detección fiable.
- Para archivos ADIF de gran tamaño, AetherSDR lee únicamente las últimas 500 líneas en cada recarga para evitar bloquear la interfaz de usuario.

## Solución de problemas

- **Los colores de los spots no se actualizan después de registrar un nuevo QSO** — Verifique que `Auto-Reload Log:` esté habilitado y que `DXCC Coloring` también lo esté. Compruebe que su programa de registro esté escribiendo exactamente en la misma ruta de archivo que se muestra junto a `Log File (ADIF):`. Si la ruta ha cambiado, haga clic en `Log File (ADIF):` para volver a seleccionar el archivo.
- **El indicador de estadísticas DXCC muestra 0 QSOs** — Es posible que el archivo ADIF no sea legible o esté vacío. Abra el archivo en un editor de texto para confirmar que contiene registros ADIF válidos; luego recargue AetherSDR o vuelva a seleccionar el archivo usando `Log File (ADIF):`.

## Relacionado

- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Descripción general de SpotHub](overview.md)
