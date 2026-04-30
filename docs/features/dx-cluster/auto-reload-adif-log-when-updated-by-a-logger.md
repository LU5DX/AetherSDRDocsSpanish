# Recargar automáticamente el registro ADIF cuando lo actualiza un programa de logging

Cuando la coloración DXCC está habilitada, AetherSDR lee su registro ADIF una sola vez al iniciar. Habilitar la recarga automática indica a AetherSDR que relea el archivo cada vez que su software de logging lo actualice, de modo que la coloración de trabajado/confirmado/necesario en el panadapter se mantenga actualizada sin intervención manual.

## Antes de comenzar

- La coloración DXCC debe estar habilitada y un archivo de registro ADIF ya debe estar cargado. Consulte [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su software de logging debe escribir las actualizaciones en la misma ruta de archivo ADIF almacenada en `DxccAdifPath`.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Confirme que `DXCC Coloring` está habilitado (el interruptor muestra su estado activo).
4. Confirme que `Log File (ADIF):` muestra la ruta de archivo correcta.
5. Haga clic en `Auto-Reload Log:` para habilitarlo.

AetherSDR ahora supervisa el archivo en `DxccAdifPath` para detectar cambios. Cada vez que su programa de logging escribe un nuevo QSO, AetherSDR relee el archivo y actualiza la coloración de los spots en el panadapter.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| `DXCC Coloring` | Interruptor maestro para colorear spots por estado trabajado/confirmado/necesario. La recarga automática no tiene efecto cuando está desactivado. | `DxccColoringEnabled` |
| `Log File (ADIF):` | Abre un selector de archivos para elegir el registro ADIF. La ruta elegida se persiste. | `DxccAdifPath` |
| `Auto-Reload Log:` | Interruptor. Cuando está habilitado, AetherSDR supervisa el archivo para detectar cambios y lo recarga automáticamente. | `DxccAutoReload` |
| `Enable FreeDV Reporter reporting when RADE is active` | Habilita el reporte de estación al mapa público FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo y cuadrícula válidos; si alguno de los campos está vacío o se resuelve como vacío, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport` |
| `Callsign: (FreeDV Reporter)` | Indicativo a reportar al mapa FreeDV Reporter. Solo lectura cuando `Use radio` está marcado. Cuando `Use radio` está marcado, el campo se mantiene sincronizado automáticamente si el indicativo se cambia en Radio Setup. | `FreeDvMyCallsign` |
| `Use radio (callsign)` | Completa previamente el campo de indicativo desde el indicativo configurado del radio y bloquea el campo como solo lectura. Habilitado de forma predeterminada. | `FreeDvUseRadioCallsign` |
| `Grid Square: (FreeDV Reporter)` | Cuadrícula Maidenhead a reportar (hasta seis caracteres). Solo lectura cuando `Use GPS` está marcado. | `FreeDvMyGrid` |
| `Use GPS (grid)` | Completa previamente el campo de cuadrícula desde el módulo GPS del radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. | `FreeDvUseGpsGrid` |
| `Station Msg: (FreeDV Reporter)` | Mensaje de texto libre opcional que aparece junto al indicativo en el mapa público FreeDV Reporter. | `FreeDvMyMessage` |

## Reporte FreeDV Reporter

El grupo **Station Reporting** dentro de la pestaña `FreeDV` permite que AetherSDR transmita la actividad de su estación al mapa público FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

### Requisitos

- La compilación debe incluir soporte WebSocket (`HAVE_WEBSOCKETS`). En Windows, también se requiere `HAVE_RADE`.
- Tanto un indicativo como una cuadrícula deben resolverse a valores no vacíos antes de que la casilla `Enable FreeDV Reporter reporting when RADE is active` pueda activarse.

### Cómo se resuelven el indicativo y la cuadrícula

Cuando habilita el reporte, AetherSDR resuelve el indicativo y la cuadrícula en el siguiente orden:

**Indicativo**
1. Si `Use radio` está marcado y el radio tiene un indicativo configurado, se utiliza ese indicativo.
2. De lo contrario, se utiliza el valor escrito en `Callsign:`.

**Cuadrícula**
1. Si `Use GPS` está marcado, el radio tiene hardware GPS y hay una cuadrícula derivada de GPS disponible, se utiliza esa cuadrícula.
2. De lo contrario, se utiliza el valor escrito en `Grid Square:`.

Si alguno de los valores está vacío después de la resolución, aparece un diálogo de advertencia y la casilla se revierte a desmarcada. Esto evita que valores en blanco o de marcador de posición (como `N0CALL` o `AA00`) se transmitan al mapa público compartido.

### Configurar el reporte

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `FreeDV`.
3. En el grupo **Station Reporting**, confirme que el campo de indicativo muestra el indicativo correcto.
   - Si `Use radio` está marcado, el campo se completa desde el indicativo configurado del radio y es solo lectura. Desmarque `Use radio` para ingresar un indicativo manualmente.
4. Confirme que el campo de cuadrícula muestra un localizador Maidenhead válido.
   - Si `Use GPS` está marcado (visible solo en radios con hardware GPS), el campo se completa desde el módulo GPS y es solo lectura. Desmarque `Use GPS` para ingresar una cuadrícula manualmente.
5. Opcionalmente, ingrese un mensaje corto en `Station Msg:`. Este texto aparece junto a su indicativo en el mapa público.
6. Marque `Enable FreeDV Reporter reporting when RADE is active`.
   - Si el indicativo o la cuadrícula están vacíos, aparece una advertencia y la casilla permanece desmarcada. Complete el campo faltante e intente de nuevo.

AetherSDR guarda la configuración en `FreeDvAutoReport` y comienza a reportar a qso.freedv.org siempre que el módem RADE esté activo.

## Consejos

- Si su programa de logging escribe un archivo temporal y luego lo renombra en su lugar, el observador de archivos puede no detectar cada guardado. Dirija su programa de logging para escribir directamente en el archivo en la ruta almacenada en `DxccAdifPath` para una detección confiable.
- Para archivos ADIF grandes, AetherSDR lee solo las últimas 500 líneas en cada recarga para evitar bloquear la interfaz de usuario.
- Si cambia el indicativo del radio en Radio Setup mientras `Use radio` está marcado, el campo `Callsign:` en la sección FreeDV Reporter se actualiza automáticamente.

## Solución de problemas

- **Los colores de los spots no se actualizan después de registrar un nuevo QSO** — Verifique que `Auto-Reload Log:` esté habilitado y que `DXCC Coloring` también esté habilitado. Confirme que su programa de logging escribe exactamente en la misma ruta de archivo que se muestra junto a `Log File (ADIF):`. Si la ruta ha cambiado, haga clic en `Log File (ADIF):` para volver a seleccionar el archivo.
- **El indicador de estadísticas DXCC muestra 0 QSOs** — El archivo ADIF puede no ser legible o puede estar vacío. Abra el archivo en un editor de texto para confirmar que contiene registros ADIF válidos, luego recargue AetherSDR o vuelva a seleccionar el archivo usando `Log File (ADIF):`.
- **La casilla FreeDV Reporter se revierte a desmarcada inmediatamente** — Falta un indicativo o cuadrícula, o está vacío. Complete ambos campos (o habilite `Use radio` / `Use GPS` para que el radio proporcione los valores) y luego marque la casilla nuevamente.
- **Los controles de FreeDV Reporter no son visibles** — La compilación no incluye soporte WebSocket. En Windows, el soporte RADE también puede estar ausente. Comuníquese con su proveedor de compilación o reconstruya con `HAVE_WEBSOCKETS` (y `HAVE_RADE` en Windows) habilitados.

## Relacionado

- [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Descripción general de SpotHub](overview.md)
