# Habilitar colores DXCC desde un registro ADIF

El coloreado DXCC permite que AetherSDR marque los spots del panadapter según si la entidad DX ha sido trabajada, confirmada o aún se necesita, basado en los contactos en su archivo de registro ADIF. Esto le ayuda a distinguir rápidamente nuevas entidades de las que ya ha registrado.

## Antes de empezar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para configurar esta función.
- Necesita un archivo de registro ADIF exportado desde su software de logging. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (cluster DX, RBN, WSJT-X, POTA, etc.) debe estar activa para que aparezcan spots en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Coloring** para habilitarlo. El botón activa el coloreado DXCC (`DxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de registro ADIF. La ruta se almacena en `DxccAdifPath`.
5. Confirme que el indicador de estadísticas DXCC se actualiza mostrando el número de QSOs importados del archivo.
6. Si su software de logging actualiza el archivo ADIF mientras AetherSDR se está ejecutando y desea que los spots reflejen nuevos contactos automáticamente, habilite **Auto-Reload Log:** (`DxccAutoReload`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **DXCC Coloring** | Alternancia maestra. Colorea los spots del panadapter según el estado DXCC trabajado/confirmado/necesario. | `DxccColoringEnabled` |
| **Log File (ADIF):** | Abre un selector de archivos. El archivo ADIF elegido se lee para poblar el estado DXCC. | `DxccAdifPath` |
| **Auto-Reload Log:** | Cuando está habilitado, relee el archivo ADIF cada vez que cambia en disco. | `DxccAutoReload` |
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita la notificación de estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo y cuadrícula válidos; si alguno está en blanco o se resuelve como vacío, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport` |
| **Callsign: (FreeDV Reporter)** | Indicativo para reportar al mapa de FreeDV Reporter. Solo lectura cuando **Use radio (callsign)** está marcado. Se actualiza automáticamente si el indicativo configurado de la radio cambia mientras **Use radio (callsign)** está marcado. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena previamente el campo de indicativo desde el indicativo configurado de la radio y bloquea el campo como solo lectura. Habilitado por defecto. | `FreeDvUseRadioCallsign` |
| **Grid Square: (FreeDV Reporter)** | Cuadrícula Maidenhead para reportar. Solo lectura cuando **Use GPS (grid)** está marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Rellena previamente el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. Habilitado por defecto. | `FreeDvUseGpsGrid` |
| **Station Msg: (FreeDV Reporter)** | Mensaje de texto libre opcional mostrado junto al indicativo en el mapa público de FreeDV Reporter. | `FreeDvMyMessage` |

## Reporte a FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR difunda la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

### Requisitos antes de habilitar

- Debe estar disponible un indicativo no vacío, ya sea desde la radio (cuando **Use radio (callsign)** está marcado) o ingresado manualmente en el campo **Callsign:**.
- Debe estar disponible una cuadrícula Maidenhead no vacía, ya sea desde el GPS de la radio (cuando **Use GPS (grid)** está marcado, en hardware compatible) o ingresada manualmente en el campo **Grid Square:**.
- Si falta algún valor cuando marca **Enable FreeDV Reporter reporting when RADE is active**, aparece un diálogo de advertencia y la casilla vuelve a desmarcarse.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que **Use radio (callsign)** esté marcado si desea que AetherSDR obtenga el indicativo de la radio automáticamente. Desmarque y escriba un indicativo en **Callsign:** para ingresar uno manualmente.
3. Si su radio tiene hardware GPS, confirme que **Use GPS (grid)** esté marcado para rellenar **Grid Square:** automáticamente. De lo contrario, desmarque y escriba su cuadrícula Maidenhead (hasta seis caracteres) en **Grid Square:**.
4. Opcionalmente escriba un mensaje corto en **Station Msg:** para mostrar junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si falta el indicativo o la cuadrícula, aparece una advertencia — rellene el campo faltante e intente de nuevo.
6. Para que el reporte comience automáticamente cada vez que AetherSDR se inicie, habilite **Auto-start on startup (FreeDV)** (`FreeDvAutoStart`).

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra cuántos QSOs fueron importados desde el archivo ADIF. Si muestra cero después de cargarlo, verifique que el archivo sea un ADIF válido.
- El botón **Log File (ADIF):** almacena la ruta de forma persistente. No necesita volver a seleccionar el archivo después de reiniciar AetherSDR.
- Habilitar **Auto-Reload Log:** elimina la necesidad de reabrir el diálogo después de registrar un nuevo contacto — los colores de los spots en el panadapter se actualizan tan pronto como su logger escribe en el archivo.
- El coloreado DXCC es independiente de los colores de spots por fuente. Si **Override Colors:** también está activo, vea [Pick colors for each spot source](pick-colors-for-each-spot-source.md) para entender cómo interactúan esas configuraciones.
- Cuando **Use radio (callsign)** está marcado, el campo de indicativo se actualiza automáticamente si cambia el indicativo en Radio Setup sin reabrir SpotHub.
- La difusión del reporte está limitada por compilación a `HAVE_WEBSOCKETS`. En Windows además requiere `HAVE_RADE`. Si el grupo **Station Reporting** o la casilla de habilitación están ausentes, su compilación no incluye los componentes requeridos.

## Solución de problemas

- **DXCC stats muestra 0 QSOs después de seleccionar un archivo** — El archivo puede no ser un ADIF válido, puede estar vacío o usar una codificación que AetherSDR no pueda leer. Exporte un ADIF fresco desde su logger e intente de nuevo.
- **Los colores de spots no cambian después de habilitar DXCC Coloring** — Confirme que la alternancia **Spots:** en la pestaña **Display** esté habilitada (`IsSpotsEnabled`). También compruebe que **Override Colors:** (`IsSpotsOverrideColorsEnabled`) no esté activo, ya que fuerza un color único para todos los spots independientemente del estado DXCC.
- **Los nuevos contactos no se reflejan en los spots** — Habilite **Auto-Reload Log:** para que AetherSDR detecte cambios de archivo, o reseleccione manualmente el archivo de registro con **Log File (ADIF):** para activar una importación fresca.
- **Aparece una advertencia al habilitar FreeDV Reporter** — El campo de indicativo o cuadrícula está en blanco. Rellene ambos campos (o marque **Use radio (callsign)** / **Use GPS (grid)** para poblarlos desde la radio) antes de habilitar la casilla.
- **El grupo Station Reporting no es visible** — Las características de FreeDV y reporte requieren una compilación con soporte `HAVE_WEBSOCKETS`. En Windows, también se requiere `HAVE_RADE`. Contacte al mantenedor de su paquete si necesita estas características.

## Relacionado

- [Auto-reload ADIF log when updated by a logger](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Pick colors for each spot source](pick-colors-for-each-spot-source.md)
- [Tune spot density, position, font size and lifetime](tune-spot-density-position-font-size-and-lifetime.md)
- [SpotHub overview](overview.md)
