# Habilitar el coloreado DXCC desde un registro ADIF

El coloreado DXCC permite que AetherSDR marque los spots del panadapter según si la entidad DX ya fue trabajada, confirmada o aún es necesaria, basándose en los contactos de su archivo de registro ADIF. Esto le ayuda a distinguir rápidamente las entidades nuevas de las que ya ha registrado.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere conexión con un radio para configurar esta función.
- Necesita un archivo de registro ADIF exportado desde su software de registro. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (clúster DX, RBN, WSJT-X, POTA, etc.) debe estar activa para que los spots aparezcan en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Coloring** para habilitarlo. El botón activa el coloreado DXCC (`DxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de registro ADIF. La ruta se almacena en `DxccAdifPath`.
5. Confirme que el indicador de estadísticas DXCC se actualiza y muestra el número de QSOs importados del archivo.
6. Si su software de registro actualiza el archivo ADIF mientras AetherSDR está en ejecución y desea que los spots reflejen los nuevos contactos automáticamente, habilite **Auto-Reload Log:** (`DxccAutoReload`).

## Qué hace cada control

| Control | Comportamiento | Clave de configuración |
|---|---|---|
| **DXCC Coloring** | Alternancia principal. Colorea los spots del panadapter según el estado DXCC: trabajado, confirmado o necesario. | `DxccColoringEnabled` |
| **Log File (ADIF):** | Abre un selector de archivos. El archivo ADIF seleccionado se lee para determinar el estado DXCC. | `DxccAdifPath` |
| **Auto-Reload Log:** | Cuando está habilitado, vuelve a leer el archivo ADIF cada vez que cambia en el disco. | `DxccAutoReload` |
| **Auto Mode:** | Selecciona automáticamente la densidad de spots según el nivel de zoom. Habilitado por defecto. | `SpotAutoSwitchMode` |
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el reporte de la estación al mapa público FreeDV Reporter (qso.freedv.org) cuando el módem RADE está activo. Requiere un indicativo y un cuadrado de localizador válidos; si alguno de los campos está vacío, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport` |
| **Callsign: (FreeDV Reporter)** | Indicativo a reportar al mapa FreeDV Reporter. Es de solo lectura cuando **Use radio (callsign)** está marcado. Se actualiza automáticamente si el indicativo configurado en el radio cambia mientras **Use radio (callsign)** está marcado. | `FreeDvMyCallsign` |
| **Use radio (callsign)** | Rellena previamente el campo de indicativo con el indicativo configurado en el radio y bloquea el campo como solo lectura. Habilitado por defecto. | `FreeDvUseRadioCallsign` |
| **Grid Square: (FreeDV Reporter)** | Cuadrado Maidenhead a reportar. Es de solo lectura cuando **Use GPS (grid)** está marcado. | `FreeDvMyGrid` |
| **Use GPS (grid)** | Rellena previamente el campo de localizador con el módulo GPS del radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. Habilitado por defecto. | `FreeDvUseGpsGrid` |
| **Station Msg: (FreeDV Reporter)** | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público FreeDV Reporter. | `FreeDvMyMessage` |

## Reporte a FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público FreeDV Reporter en qso.freedv.org cuando el módem RADE está activo.

### Requisitos antes de habilitar

- Debe estar disponible un indicativo no vacío, ya sea proveniente del radio (cuando **Use radio (callsign)** está marcado) o ingresado manualmente en el campo **Callsign:**.
- Debe estar disponible un cuadrado Maidenhead no vacío, ya sea desde el GPS del radio (cuando **Use GPS (grid)** está marcado, en hardware compatible) o ingresado manualmente en el campo **Grid Square:**.
- Si alguno de los valores falta al marcar **Enable FreeDV Reporter reporting when RADE is active**, aparece un diálogo de advertencia y la casilla vuelve a desmarcarse.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que **Use radio (callsign)** está marcado si desea que AetherSDR obtenga el indicativo del radio automáticamente. Desmarque la opción y escriba un indicativo en **Callsign:** para ingresarlo manualmente.
3. Si su radio tiene hardware GPS, confirme que **Use GPS (grid)** está marcado para rellenar **Grid Square:** automáticamente. De lo contrario, desmarque la opción y escriba su cuadrado Maidenhead (hasta seis caracteres) en **Grid Square:**.
4. Opcionalmente, escriba un mensaje corto en **Station Msg:** para mostrarlo junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si el indicativo o el localizador faltan, aparece una advertencia — complete el campo faltante e intente de nuevo.
6. Para que el reporte se inicie automáticamente cada vez que AetherSDR se ejecute, habilite **Auto-start on startup (FreeDV)** (`FreeDvAutoStart`).

## Consejos

- El indicador de estadísticas DXCC en el diálogo muestra cuántos QSOs fueron importados del archivo ADIF. Si indica cero después de cargarlo, verifique que el archivo sea ADIF válido.
- El botón **Log File (ADIF):** almacena la ruta de forma persistente. No es necesario volver a seleccionar el archivo después de reiniciar AetherSDR.
- Habilitar **Auto-Reload Log:** elimina la necesidad de reabrir el diálogo después de registrar un nuevo contacto — los colores de los spots en el panadapter se actualizan en cuanto su software de registro escribe en el archivo.
- El coloreado DXCC es independiente de los colores de spots por fuente. Si **Override Colors:** también está activo, consulte [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md) para ver cómo interactúan esas configuraciones.
- **Auto Mode:** (`SpotAutoSwitchMode`) está habilitado por defecto a partir de la versión v0.9.5.1. Si lo deshabilitó anteriormente, verifique el estado actual en la pestaña **Display** después de actualizar.
- Cuando **Use radio (callsign)** está marcado, el campo de indicativo se actualiza automáticamente si cambia el indicativo en Radio Setup sin necesidad de reabrir SpotHub.
- La transmisión al Reporter está condicionada en la compilación por `HAVE_WEBSOCKETS`. En Windows, además requiere `HAVE_RADE`. Si el grupo **Station Reporting** o la casilla de habilitación no aparecen, su compilación no incluye los componentes necesarios.

## Solución de problemas

- **Las estadísticas DXCC muestran 0 QSOs después de seleccionar un archivo** — Es posible que el archivo no sea ADIF válido, esté vacío o use una codificación que AetherSDR no puede leer. Exporte un nuevo ADIF desde su software de registro e intente de nuevo.
- **Los colores de los spots no cambian después de habilitar DXCC Coloring** — Confirme que la alternancia **Spots:** en la pestaña **Display** está habilitada (`IsSpotsEnabled`). También verifique que **Override Colors:** (`IsSpotsOverrideColorsEnabled`) no esté activo, ya que fuerza un único color para todos los spots independientemente del estado DXCC.
- **Los nuevos contactos no se reflejan en los spots** — Habilite **Auto-Reload Log:** para que AetherSDR detecte los cambios en el archivo, o vuelva a seleccionar manualmente el archivo de registro con **Log File (ADIF):** para forzar una nueva importación.
- **Aparece una advertencia al habilitar FreeDV Reporter** — El campo de indicativo o de cuadrado de localizador está vacío. Complete ambos campos (o marque **Use radio (callsign)** / **Use GPS (grid)** para rellenarlos desde el radio) antes de habilitar la casilla.
- **El grupo Station Reporting no es visible** — Las funciones de FreeDV y reporte requieren una compilación con soporte `HAVE_WEBSOCKETS`. En Windows, también se requiere `HAVE_RADE`. Contacte al responsable de su paquete si necesita estas funciones.

## Relacionados

- [Recarga automática del registro ADIF cuando es actualizado por un software de registro](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Descripción general de SpotHub](overview.md)
