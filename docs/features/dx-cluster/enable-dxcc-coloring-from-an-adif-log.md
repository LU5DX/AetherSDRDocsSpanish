# Habilitar la coloración de entidades DXCC desde un archivo de registro ADIF

La coloración de entidades DXCC permite a AetherSDR marcar los puntos (spots) en el panadapter según si la entidad DX ha sido trabajada, confirmada o aún es necesaria, basándose en los contactos de su archivo de registro ADIF. Esto le ayuda a distinguir rápidamente las nuevas entidades de aquellas que ya ha registrado.

## Antes de comenzar

- AetherSDR debe estar ejecutándose. No se requiere una conexión de radio para configurar esta función.
- Necesita un archivo de registro ADIF exportado desde su software de registro. El archivo debe usar el formato estándar `.adi` o `.adif`.
- Al menos una fuente de spots (DX cluster, RBN, WSJT-X, POTA, etc.) debe estar activa para que aparezcan puntos en el panadapter.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Display**.
3. Haga clic en el botón de alternancia **DXCC Coloring** para habilitarlo. El botón activa la coloración de entidades DXCC (`DxccColoringEnabled`).
4. Haga clic en **Log File (ADIF):** para abrir un selector de archivos. Seleccione su archivo de registro ADIF. La ruta se almacena en `DxccAdifPath`.
5. Confirme que el indicador de estadísticas de entidades DXCC se actualice para mostrar la cantidad de QSO importados desde el archivo.
6. Si su software de registro actualiza el archivo ADIF mientras AetherSDR está ejecutándose y desea que los spots reflejen nuevos contactos automáticamente, habilite **Auto-Reload Log:** (`DxccAutoReload`).

## Qué hace cada control

| Control                                                  | Comportamiento                                                                                                                                                                                                                                                   | Clave de configuración   |
|----------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|
| **DXCC Coloring**                                        | Activación principal. Colorea los spots del panadapter según el estado trabajado/confirmado/necesario de la entidad DXCC.                                                                                                                                       | `DxccColoringEnabled`    |
| **Log File (ADIF):**                                     | Abre un selector de archivos. El archivo ADIF elegido se lee para poblar el estado de las entidades DXCC.                                                                                                                                                         | `DxccAdifPath`           |
| **Auto-Reload Log:**                                     | Cuando está habilitado, vuelve a leer el archivo ADIF cada vez que cambia en el disco.                                                                                                                                                                          | `DxccAutoReload`         |
| **Auto Mode:**                                           | Selecciona automáticamente la densidad de spots según el nivel de zoom. Por defecto está **Habilitado** a partir de v0.9.5.1.                                                                                                                                   | `SpotsAutoMode`          |
| **Spot Lines:**                                          | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. Nuevo en v0.9.7.                                                                                                          | `IsSpotsLinesEnabled`    |
| **Enable FreeDV Reporter reporting when RADE is active** | Habilita el informe de estación al mapa público de FreeDV Reporter (qso.freedv.org) siempre que el módem RADE esté activo. Requiere un indicativo y un cuadrado de cuadrícula válidos; si alguno de los campos está en blanco o se resuelve vacío, la casilla se niega a habilitarse y muestra una advertencia. | `FreeDvAutoReport`       |
| **Callsign: (FreeDV Reporter)**                          | Indicativo para informar al mapa de FreeDV Reporter. Solo lectura cuando **Use radio (callsign)** está marcado. Se actualiza automáticamente si el indicativo configurado de la radio cambia mientras **Use radio (callsign)** está marcado.                   | `FreeDvMyCallsign`       |
| **Use radio (callsign)**                                 | Pre-completa el campo de indicativo desde el indicativo configurado de la radio y bloquea el campo como solo lectura. Por defecto está habilitado.                                                                                                            | `FreeDvUseRadioCallsign` |
| **Grid Square: (FreeDV Reporter)**                       | Cuadrado de cuadrícula Maidenhead para informar. Solo lectura cuando **Use GPS (grid)** está marcado.                                                                                                                                                          | `FreeDvMyGrid`           |
| **Use GPS (grid)**                                       | Pre-completa el campo de cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. Por defecto está habilitado.                                                              | `FreeDvUseGpsGrid`       |
| **Station Msg: (FreeDV Reporter)**                       | Mensaje de texto libre opcional que se muestra junto al indicativo en el mapa público de FreeDV Reporter.                                                                                                                                                      | `FreeDvMyMessage`        |
| Total Spots:                                             | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. Se actualiza cuando se añaden o borran spots. Se restablece a 0 cuando se presiona **Clear All Spots**.                                                                   | —                        |

## Sintonización desde la lista de spots

Hacer doble clic en una fila de la pestaña **Spot List** sintoniza el receptor activo en la frecuencia de ese spot. A partir de v0.9.7, AetherSDR también reenvía el modo derivado del comentario del spot, por lo que el receptor cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

## Informes de FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público de FreeDV Reporter en qso.freedv.org siempre que el módem RADE esté activo.

### Requisitos antes de habilitar

- Debe estar disponible un indicativo no vacío, ya sea desde la radio (cuando **Use radio (callsign)** está marcado) o ingresado manualmente en el campo **Callsign:**.
- Debe estar disponible un cuadrado de cuadrícula Maidenhead no vacío, ya sea desde el GPS de la radio (cuando **Use GPS (grid)** está marcado, en hardware compatible) o ingresado manualmente en el campo **Grid Square:**.
- Si falta alguno de los valores al marcar **Enable FreeDV Reporter reporting when RADE is active**, aparece un cuadro de diálogo de advertencia y la casilla vuelve a estar desmarcada.

### Pasos

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme que **Use radio (callsign)** esté marcado si desea que AetherSDR obtenga el indicativo de la radio automáticamente. Desmárquelo y escriba un indicativo en **Callsign:** para ingresarlo manualmente.
3. Si su radio tiene hardware GPS, confirme que **Use GPS (grid)** esté marcado para poblar **Grid Square:** automáticamente. De lo contrario, desmárquelo y escriba su cuadrado de cuadrícula Maidenhead (hasta seis caracteres) en **Grid Square:**.
4. Opcionalmente, escriba un mensaje corto en **Station Msg:** para que se muestre junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si falta el indicativo o la cuadrícula, aparece una advertencia; complete el campo faltante e intente de nuevo.
6. Para que los informes se inicien automáticamente cada vez que AetherSDR se inicie, habilite **Auto-start on startup (FreeDV)** (`FreeDvAutoStart`).

## Consejos

- El indicador de estadísticas de entidades DXCC en el cuadro de diálogo muestra cuántos QSO se importaron del archivo ADIF. Si muestra cero después de cargar, verifique que el archivo sea un ADIF válido.
- El botón **Log File (ADIF):** almacena la ruta de forma persistente. No es necesario volver a seleccionar el archivo después de reiniciar AetherSDR.
- Habilitar **Auto-Reload Log:** elimina la necesidad de volver a abrir el cuadro de diálogo después de registrar un nuevo contacto: los colores de los spots en el panadapter se actualizan tan pronto como su registrador escribe en el archivo.
- La coloración de entidades DXCC es independiente de los colores de los spots por fuente. Si **Override Colors:** también está activo, consulte [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md) para saber cómo interactúan esas configuraciones.
- **Auto Mode:** (`SpotsAutoMode`) por defecto está **Habilitado** a partir de v0.9.5.1. Si lo deshabilitó anteriormente, verifique el estado actual en la pestaña **Display** después de actualizar.
- **Spot Lines:** (`IsSpotsLinesEnabled`) por defecto está **Habilitado**. Durante concursos o cuando el panadapter se siente visualmente recargado, deshabilite esta opción en la pestaña **Display** para eliminar las líneas verticales mientras mantiene visibles las etiquetas de los spots.
- Cuando **Use radio (callsign)** está marcado, el campo de indicativo se actualiza automáticamente si cambia el indicativo en la configuración de la radio sin volver a abrir SpotHub.
- La transmisión del informe depende de la compilación y requiere `HAVE_WEBSOCKETS`. En Windows, también requiere `HAVE_RADE`. Si el grupo **Station Reporting** o la casilla de verificación están ausentes, su compilación no incluye los componentes necesarios.

## Solución de problemas

- **Las estadísticas de entidades DXCC muestran 0 QSO después de seleccionar un archivo** — Es posible que el archivo no sea un ADIF válido, que esté vacío o que use una codificación que AetherSDR no puede leer. Exporte un ADIF nuevo desde su registrador e intente de nuevo.
- **Los colores de los spots no cambian después de habilitar la coloración de entidades DXCC** — Confirme que la opción **Spots:** en la pestaña **Display** esté habilitada (`IsSpotsEnabled`). También verifique que **Override Colors:** (`IsSpotsOverrideColorsEnabled`) no esté activo, ya que fuerza un solo color para todos los spots independientemente del estado de la entidad DXCC.
- **Los nuevos contactos no se reflejan en los spots** — Habilite **Auto-Reload Log:** para que AetherSDR detecte los cambios en el archivo, o seleccione manualmente el archivo de registro nuevamente con **Log File (ADIF):** para activar una importación nueva.
- **Hacer doble clic en un spot no cambia el modo** — El modo se deriva del texto del comentario del spot. Si el comentario no contiene un token de modo reconocible, solo cambia la frecuencia.
- **Aparece una advertencia al habilitar FreeDV Reporter** — El campo de indicativo o de cuadrado de cuadrícula está en blanco. Complete ambos campos (o marque **Use radio (callsign)** / **Use GPS (grid)** para poblarlos desde la radio) antes de habilitar la casilla.
- **El grupo Station Reporting no es visible** — Las funciones FreeDV y de informes requieren una compilación con soporte `HAVE_WEBSOCKETS`. En Windows, también se requiere `HAVE_RADE`. Comuníquese con el mantenedor de su paquete si necesita estas funciones.

## Relacionado

- [Recargar automáticamente el registro ADIF cuando un registrador lo actualiza](auto-reload-adif-log-when-updated-by-a-logger.md)
- [Elegir colores para cada fuente de spots](pick-colors-for-each-spot-source.md)
- [Ajustar densidad, posición, tamaño de fuente y duración de los spots](tune-spot-density-position-font-size-and-lifetime.md)
- [Descripción general de SpotHub](overview.md)

<!-- docmesh:llm version=V0.9.7 date=2026-05-03 -->
