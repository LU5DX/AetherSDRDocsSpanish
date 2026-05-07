# Recarga automática del registro ADIF al ser actualizado por un registrador

Cuando la coloración DXCC está habilitada, AetherSDR lee su registro ADIF una vez al inicio. Habilitar la recarga automática indica a AetherSDR que vuelva a leer el archivo cada vez que su software de registro lo actualice, de modo que la coloración de trabajado/confirmado/necesario en el panadapter se mantenga actualizada sin intervención manual.

## Antes de comenzar

- La coloración DXCC debe estar habilitada y ya debe haberse cargado un archivo de registro ADIF. Consulte [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md).
- Su software de registro debe escribir las actualizaciones en la misma ruta de archivo ADIF almacenada en `DxccAdifPath`.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `Display`.
3. Confirme que `DXCC Coloring` esté habilitado (el interruptor muestra su estado activo).
4. Confirme que `Log File (ADIF):` muestre la ruta de archivo correcta.
5. Haga clic en `Auto-Reload Log:` para habilitarlo.

AetherSDR ahora monitorea el archivo en `DxccAdifPath` en busca de cambios. Cada vez que su registrador escribe un nuevo QSO, AetherSDR vuelve a leer el archivo y actualiza la coloración de los spots en el panadapter.

## Qué hace cada control

| Control                                                | Descripción                                                                                                                                                                                                                                                                                                                    | Clave de configuración  |
|--------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| `DXCC Coloring`                                        | Interruptor maestro para colorear spots según el estado de trabajado/confirmado/necesario. La recarga automática no tiene efecto cuando está desactivado.                                                                                                                                                                       | `DxccColoringEnabled`    |
| `Log File (ADIF):`                                     | Abre un selector de archivos para elegir el registro ADIF. La ruta seleccionada se conserva.                                                                                                                                                                                                                                   | `DxccAdifPath`           |
| `Auto-Reload Log:`                                     | Interruptor. Cuando está habilitado, AetherSDR monitorea el archivo en busca de cambios y lo recarga automáticamente.                                                                                                                                                                                                           | `DxccAutoReload`         |
| `Enable FreeDV Reporter reporting when RADE is active` | Habilita la notificación de estación al mapa público de FreeDV Reporter (qso.freedv.org) cada vez que el módem RADE está activo. Requiere un indicativo y una cuadrícula válidos; si alguno de los campos está en blanco o se resuelve como vacío, la casilla se niega a habilitarse y muestra una advertencia.                 | `FreeDvAutoReport`       |
| `Callsign: (FreeDV Reporter)`                          | Indicativo para notificar al mapa de FreeDV Reporter. Solo lectura cuando `Use radio` está marcado. Cuando `Use radio` está marcado, el campo se sincroniza automáticamente si el indicativo se cambia en Radio Setup.                                                                                                         | `FreeDvMyCallsign`       |
| `Use radio (callsign)`                                 | Rellena previamente el campo de indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Por defecto está habilitado.                                                                                                                                                                     | `FreeDvUseRadioCallsign` |
| `Grid Square: (FreeDV Reporter)`                       | Cuadrícula Maidenhead para notificar (hasta seis caracteres). Solo lectura cuando `Use GPS` está marcado.                                                                                                                                                                                                                      | `FreeDvMyGrid`           |
| `Use GPS (grid)`                                       | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS.                                                                                                                                                   | `FreeDvUseGpsGrid`       |
| `Station Msg: (FreeDV Reporter)`                       | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter.                                                                                                                                                                                                                      | `FreeDvMyMessage`        |
| `Auto Mode:`                                           | Interruptor. Cuando está habilitado, cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (por ejemplo, CW, FT8, RTTY). Por defecto está **Habilitado** a partir de la versión v0.9.5.1.                                                                                           | `SpotAutoSwitchMode`     |
| `Spot Lines:`                                          | Interruptor. Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Por defecto está **Habilitado**. Desactívelo durante concursos para reducir el desorden visual. Nuevo en v0.9.7.                                                                                                                             | `IsSpotsLinesEnabled`    |
| `Total Spots:`                                         | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cada vez que se agregan o eliminan spots. Se reinicia a 0 cuando se presiona **Clear All Spots**.                                                                                                                           | —                        |

## Sintonización desde la lista de spots

Al hacer doble clic en una fila de la pestaña Spot List, se sintoniza el slice activo a la frecuencia del spot. A partir de v0.9.7, AetherSDR también reenvía la información de modo extraída del comentario del spot. Si hay un modo reconocido (como CW, FT8 o SSB), el slice cambia a ese modo automáticamente, siempre que `Auto Mode:` esté habilitado en la pestaña Display.

## Notificación a FreeDV Reporter

El grupo **Station Reporting** dentro de la pestaña `FreeDV` permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org cada vez que el módem RADE esté activo.

### Requisitos

- La compilación debe incluir soporte para WebSocket (`HAVE_WEBSOCKETS`). En Windows, también se requiere `HAVE_RADE`.
- Tanto un indicativo como una cuadrícula deben resolverse a valores no vacíos antes de que se pueda activar la casilla `Enable FreeDV Reporter reporting when RADE is active`.

### Cómo se resuelven el indicativo y la cuadrícula

Cuando habilita la notificación, AetherSDR resuelve el indicativo y la cuadrícula en el siguiente orden:

**Indicativo**
1. Si `Use radio` está marcado y la radio tiene un indicativo configurado, se usa ese indicativo.
2. De lo contrario, se usa el valor escrito en `Callsign:`.

**Cuadrícula**
1. Si `Use GPS` está marcado, la radio tiene hardware GPS y hay una cuadrícula derivada del GPS disponible, se usa esa cuadrícula.
2. De lo contrario, se usa el valor escrito en `Grid Square:`.

Si alguno de los valores está vacío después de la resolución, aparece un cuadro de diálogo de advertencia y la casilla vuelve al estado desmarcado. Esto evita que se transmitan valores en blanco o de marcador de posición (como `N0CALL` o `AA00`) al mapa público compartido.

### Configuración de la notificación

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña `FreeDV`.
3. En el grupo **Station Reporting**, confirme que el campo de indicativo muestre el indicativo correcto.
   - Si `Use radio` está marcado, el campo se rellena desde el indicativo configurado en la radio y es de solo lectura. Desmarque `Use radio` para ingresar un indicativo manualmente.
4. Confirme que el campo de cuadrícula muestre un localizador Maidenhead válido.
   - Si `Use GPS` está marcado (visible solo en radios con hardware GPS), el campo se rellena desde el módulo GPS y es de solo lectura. Desmarque `Use GPS` para ingresar una cuadrícula manualmente.
5. Opcionalmente, ingrese un mensaje breve en `Station Msg:`. Este texto aparece junto a su indicativo en el mapa público.
6. Marque `Enable FreeDV Reporter reporting when RADE is active`.
   - Si el indicativo o la cuadrícula están vacíos, aparece una advertencia y la casilla permanece desmarcada. Complete el campo faltante e intente nuevamente.

AetherSDR guarda la configuración en `FreeDvAutoReport` y comienza a notificar a qso.freedv.org cada vez que el módem RADE esté activo.

## Consejos

- Si su registrador escribe un archivo temporal y luego lo renombra en su lugar, el monitor de archivos puede no detectar cada guardado. Configure su registrador para que escriba directamente en el archivo en la ruta almacenada en `DxccAdifPath` para una detección confiable.
- Para archivos ADIF grandes, AetherSDR lee solo las últimas 500 líneas en cada recarga para evitar bloquear la interfaz de usuario.
- Si cambia el indicativo de la radio en Radio Setup mientras `Use radio` está marcado, el campo `Callsign:` en la sección de FreeDV Reporter se actualiza automáticamente.
- `Auto Mode:` está **Habilitado** de forma predeterminada. Si el modo del slice cambia inesperadamente al hacer clic en un spot, abra la pestaña Display y configure `Auto Mode:` en Deshabilitado.
- `Spot Lines:` está **Habilitado** de forma predeterminada. Durante concursos, desactivarlo reduce el desorden visual en el panadapter.

## Solución de problemas

- **Los colores de los spots no se actualizan después de registrar un nuevo QSO** — Verifique que `Auto-Reload Log:` esté habilitado y que `DXCC Coloring` también lo esté. Compruebe que su registrador esté escribiendo en la misma ruta de archivo que se muestra junto a `Log File (ADIF):`. Si la ruta ha cambiado, haga clic en `Log File (ADIF):` para volver a seleccionar el archivo.
- **El indicador de estadísticas DXCC muestra 0 QSO** — Es posible que el archivo ADIF no sea legible o esté vacío. Abra el archivo en un editor de texto para confirmar que contiene registros ADIF válidos, luego recargue AetherSDR o vuelva a seleccionar el archivo usando `Log File (ADIF):`.
- **La casilla FreeDV Reporter vuelve al estado desmarcado inmediatamente** — Falta un indicativo o una cuadrícula, o están vacíos. Complete ambos campos (o habilite `Use radio` / `Use GPS` para que la radio proporcione los valores) y luego marque la casilla nuevamente.
- **Los controles de FreeDV Reporter no son visibles** — La compilación no incluye soporte para WebSocket. En Windows, también puede faltar soporte RADE. Comuníquese con su proveedor de compilación o recompile con `HAVE_WEBSOCKETS` (y `HAVE_RADE` en Windows) habilitados.
- **Auto Mode estaba previamente deshabilitado y ahora se comporta de manera diferente después de actualizar** — El valor predeterminado para `Auto Mode:` cambió a **Habilitado** en v0.9.5.1. Si desea mantener el comportamiento anterior, abra la pestaña **Display** y configure `Auto Mode:` en **Deshabilitado**.
- **Al hacer doble clic en un spot ya no sintoniza sin cambiar de modo** — A partir de v0.9.7, la sintonización desde la lista de spots también reenvía información de modo al slice. Si no desea el cambio automático de modo, abra la pestaña **Display** y configure `Auto Mode:` en **Deshabilitado**.

## Relacionados

- [Habilitar coloración DXCC desde un registro ADIF](enable-dxcc-coloring-from-an-adif-log.md)
- [Descripción general de SpotHub](overview.md)
<!-- docmesh:llm version=v0.9.7 date=2026-05-03 -->
