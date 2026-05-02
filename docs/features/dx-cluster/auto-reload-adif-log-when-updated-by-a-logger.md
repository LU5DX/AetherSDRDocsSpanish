# Recarga automática del registro ADIF cuando lo actualiza un programa de log

Cuando el coloreado DXCC está habilitado, AetherSDR lee su registro ADIF una vez al inicio. Habilitar la recarga automática indica a AetherSDR que vuelva a leer el archivo cada vez que su programa de log lo actualice, de modo que el coloreado de trabajados/confirmados/necesarios en el panadapter se mantenga al día sin intervención manual.

## Antes de comenzar

- El coloreado DXCC debe estar habilitado y un archivo de registro ADIF debe estar ya cargado. Consulte [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su programa de log debe escribir las actualizaciones en la misma ruta de archivo ADIF almacenada en `DxccAdifPath`.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Confirme que `DXCC Coloring` está habilitado (el interruptor muestra su estado activo).
4. Confirme que `Log File (ADIF):` muestra la ruta de archivo correcta.
5. Haga clic en `Auto-Reload Log:` para habilitarlo.

AetherSDR ahora vigila el archivo en `DxccAdifPath` en busca de cambios. Cada vez que su programa de log escribe un nuevo QSO, AetherSDR vuelve a leer el archivo y actualiza el coloreado de spots en el panadapter.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| `DXCC Coloring` | Interruptor principal para colorear spots según el estado trabajado/confirmado/necesario. La recarga automática no tiene efecto cuando está desactivado. | `DxccColoringEnabled` |
| `Log File (ADIF):` | Abre un selector de archivos para elegir el registro ADIF. La ruta seleccionada se conserva. | `DxccAdifPath` |
| `Auto-Reload Log:` | Interruptor. Cuando está habilitado, AetherSDR vigila el archivo en busca de cambios y lo recarga automáticamente. | `DxccAutoReload` |
| `Enable FreeDV Reporter reporting when RADE is active` | Habilita el reporte de la estación al mapa público de FreeDV Reporter (qso.freedv.org) cuando el módem RADE está activo. Requiere un indicativo y un localizador de cuadrícula válidos; si alguno de los campos está vacío o se resuelve como vacío, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport` |
| `Callsign: (FreeDV Reporter)` | Indicativo para reportar al mapa de FreeDV Reporter. Solo lectura cuando `Use radio` está marcado. Cuando `Use radio` está marcado, el campo se sincroniza automáticamente si el indicativo cambia en Radio Setup. | `FreeDvMyCallsign` |
| `Use radio (callsign)` | Rellena el campo de indicativo con el indicativo configurado en el equipo y bloquea el campo como solo lectura. Habilitado por defecto. | `FreeDvUseRadioCallsign` |
| `Grid Square: (FreeDV Reporter)` | Localizador Maidenhead a reportar (hasta seis caracteres). Solo lectura cuando `Use GPS` está marcado. | `FreeDvMyGrid` |
| `Use GPS (grid)` | Rellena el campo de cuadrícula con los datos del módulo GPS del equipo y bloquea el campo como solo lectura. Solo se muestra en modelos de equipo que disponen de hardware GPS. | `FreeDvUseGpsGrid` |
| `Station Msg: (FreeDV Reporter)` | Mensaje de texto libre opcional que aparece junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |
| `Auto Mode:` | Interruptor. Cuando está habilitado, selecciona automáticamente la densidad de spots según el nivel de zoom del panadapter. Habilitado por defecto a partir de la versión v0.9.5.1. | `SpotAutoSwitchMode` |

## Reporte a FreeDV Reporter

El grupo **Station Reporting** dentro de la pestaña `FreeDV` permite a AetherSDR transmitir la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org cuando el módem RADE está activo.

### Requisitos

- La compilación debe incluir soporte WebSocket (`HAVE_WEBSOCKETS`). En Windows, también se requiere `HAVE_RADE`.
- Tanto el indicativo como el localizador de cuadrícula deben resolverse como valores no vacíos antes de poder activar la casilla `Enable FreeDV Reporter reporting when RADE is active`.

### Cómo se resuelven el indicativo y la cuadrícula

Al habilitar el reporte, AetherSDR resuelve el indicativo y la cuadrícula en el siguiente orden:

**Indicativo**
1. Si `Use radio` está marcado y el equipo tiene un indicativo configurado, se usa ese indicativo.
2. En caso contrario, se usa el valor escrito en `Callsign:`.

**Localizador de cuadrícula**
1. Si `Use GPS` está marcado, el equipo dispone de hardware GPS y hay una cuadrícula derivada del GPS disponible, se usa esa cuadrícula.
2. En caso contrario, se usa el valor escrito en `Grid Square:`.

Si alguno de los valores queda vacío tras la resolución, aparece un diálogo de advertencia y la casilla vuelve a estar desmarcada. Esto evita que valores en blanco o de marcador de posición (como `N0CALL` o `AA00`) se transmitan al mapa público compartido.

### Configurar el reporte

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `FreeDV`.
3. En el grupo **Station Reporting**, confirme que el campo de indicativo muestra el indicativo correcto.
   - Si `Use radio` está marcado, el campo se rellena con el indicativo configurado en el equipo y es de solo lectura. Desmarque `Use radio` para introducir un indicativo manualmente.
4. Confirme que el campo de localizador de cuadrícula muestra un localizador Maidenhead válido.
   - Si `Use GPS` está marcado (visible solo en equipos con hardware GPS), el campo se rellena con los datos del módulo GPS y es de solo lectura. Desmarque `Use GPS` para introducir una cuadrícula manualmente.
5. Opcionalmente, introduzca un mensaje breve en `Station Msg:`. Este texto aparece junto a su indicativo en el mapa público.
6. Marque `Enable FreeDV Reporter reporting when RADE is active`.
   - Si el indicativo o la cuadrícula están vacíos, aparece una advertencia y la casilla permanece desmarcada. Rellene el campo que falta e inténtelo de nuevo.

AetherSDR guarda la configuración en `FreeDvAutoReport` y comienza a reportar a qso.freedv.org cada vez que el módem RADE está activo.

## Consejos

- Si su programa de log escribe en un archivo temporal y luego lo renombra en su lugar, es posible que el monitor de archivos no detecte cada guardado. Configure su programa de log para que escriba directamente en el archivo de la ruta almacenada en `DxccAdifPath` para una detección fiable.
- Para archivos ADIF de gran tamaño, AetherSDR lee solo las últimas 500 líneas en cada recarga para evitar bloquear la interfaz.
- Si cambia el indicativo del equipo en Radio Setup mientras `Use radio` está marcado, el campo `Callsign:` en la sección de FreeDV Reporter se actualiza automáticamente.
- `Auto Mode:` está habilitado por defecto en la versión v0.9.5.1. Si la densidad de spots en el panadapter cambia inesperadamente al hacer zoom, compruebe si `Auto Mode:` está activado y desactívelo para usar una densidad fija en su lugar.

## Solución de problemas

- **Los colores de los spots no se actualizan tras registrar un nuevo QSO** — Verifique que `Auto-Reload Log:` está habilitado y que `DXCC Coloring` también está habilitado. Compruebe que su programa de log está escribiendo exactamente en la misma ruta de archivo que se muestra junto a `Log File (ADIF):`. Si la ruta ha cambiado, haga clic en `Log File (ADIF):` para volver a seleccionar el archivo.
- **El indicador de estadísticas DXCC muestra 0 QSOs** — Es posible que el archivo ADIF no sea legible o esté vacío. Abra el archivo en un editor de texto para confirmar que contiene registros ADIF válidos y, a continuación, recargue AetherSDR o vuelva a seleccionar el archivo con `Log File (ADIF):`.
- **La casilla de FreeDV Reporter vuelve a desmarcarse inmediatamente** — Falta un indicativo o un localizador de cuadrícula, o están vacíos. Rellene ambos campos (o habilite `Use radio` / `Use GPS` para que el equipo suministre los valores) y marque la casilla de nuevo.
- **Los controles de FreeDV Reporter no son visibles** — La compilación no incluye soporte WebSocket. En Windows, es posible que el soporte RADE también esté ausente. Contacte con su proveedor de compilación o recompile con `HAVE_WEBSOCKETS` (y `HAVE_RADE` en Windows) habilitados.

## Relacionados

- [Habilitar el coloreado DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Descripción general de SpotHub](overview.md)
