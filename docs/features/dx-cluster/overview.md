# Resumen de SpotHub

SpotHub es el centro central de AetherSDR para recibir spots de DX de múltiples fuentes y mostrarlos como superposiciones en el panadapter. Úselo para conectarse a clusters DX tradicionales, la Red de Balizas Inversa (RBN), WSJT-X, SpotCollector, POTA y FreeDV, todo desde un mismo diálogo.

## Antes de comenzar

- Abra SpotHub a través de `Settings > SpotHub...`. No se requiere conexión de radio.
- Tenga su indicativo de inicio de sesión listo si planea conectarse a un cluster DX o a RBN.
- Tenga disponible un archivo de registro ADIF si desea colorear por DXCC.

## Cómo funciona

SpotHub agrega spots de hasta seis fuentes independientes. Cada fuente se ejecuta de forma independiente: puede habilitar cualquier combinación simultáneamente. Todos los spots entrantes se fusionan en una lista unificada y se representan como marcadores de frecuencia en el panadapter.

Los spots de cada fuente tienen un código de color separado para que pueda distinguir su origen de un vistazo. Una capa de visualización global (la pestaña **Display**) controla cómo aparecen todos los spots en el panadapter, independientemente de la fuente.

### Fuentes

**Pestaña Cluster**: se conecta a un cluster DX mediante una sesión telnet. Usted proporciona el nombre de host (`ClusterHost`), el puerto (`ClusterPort`, 1–65535) y el indicativo de inicio de sesión (`ClusterCallsign`). La **Cluster Console** muestra el tráfico telnet sin procesar. Puede escribir comandos del cluster en el campo de línea de comandos y enviarlos con Send. El color del spot se establece mediante **Spot Color:**, persistido como `ClusterSpotColor`.

**Pestaña RBN**: se conecta a la Red de Balizas Inversa mediante telnet. La configuración es similar a la pestaña Cluster: `RbnHost`, `RbnPort` (1–65535), `RbnCallsign`. La caja de selección **Rate Limit:** (`RbnRateLimit`) limita la cantidad de spots aceptados por segundo, lo cual es útil porque el volumen de tráfico de RBN puede ser muy alto. La **RBN Console** muestra el tráfico sin procesar. El color del spot se establece mediante **Spot Color:** (`RbnSpotColor`).

**Pestaña WSJT-X**: escuta datagramas UDP transmitidos por una instancia de WSJT-X en ejecución. Configure la dirección de enlace (`WsjtxAddress`) y el puerto (`WsjtxPort`, 1–65535), luego haga clic en Start. Tres casillas de verificación filtran qué decodificaciones aparecen como spots: **CQ** (`WsjtxFilterCQ`), **CQ POTA** (`WsjtxFilterPOTA`) y **Calling Me** (`WsjtxFilterCallingMe`). Cada categoría tiene su propio selector de color: color CQ (`WsjtxColorCQ`), color POTA (`WsjtxColorPOTA`), color Calling Me (`WsjtxColorCallingMe`) y color Por defecto (`WsjtxColorDefault`). **Spot Life:** (`WsjtxSpotLife`) controla cuánto tiempo permanecen los spots de WSJT-X en el panadapter. La consola **WSJT-X Decodes** muestra el flujo de decodificaciones sin procesar.

**Pestaña SpotCollector**: escuta en un puerto UDP las transmisiones de spots de Ham Radio Deluxe SpotCollector. Configure **UDP Port:** (`SpotCollectorPort`, 1–65535) y haga clic en Start. La consola **SpotCollector Spots** muestra los spots recibidos.

**Pestaña POTA**: consulta `api.pota.app` a través de HTTP en un intervalo configurable (**Poll Interval:**, `PotaPollInterval`). La dirección del servidor es fija y se muestra como un indicador. La consola **POTA Activations** muestra el flujo de activaciones. El color del spot se establece mediante **Spot Color:** (`PotaSpotColor`).

**Pestaña FreeDV**: se conecta al QSO Reporter de FreeDV a través de WebSocket en `qso.freedv.org`. La dirección del servidor es fija. La consola **FreeDV Spots** muestra la actividad. El color del spot se establece mediante **Spot Color:** (`FreeDvSpotColor`). Esta pestaña solo está presente en compilaciones que incluyen soporte WebSocket.

### Conexión automática e inicio automático

Cada fuente tiene una opción **Auto-connect on startup** o **Auto-start on startup**. Cuando está habilitada, esa fuente se conecta o se inicia automáticamente cada vez que se lanza AetherSDR, sin intervención manual. Las claves persistidas son `ClusterAutoConnect`, `RbnAutoConnect`, `WsjtxAutoStart`, `SpotCollectorAutoStart`, `PotaAutoStart` y `FreeDvAutoStart`.

### Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y ordenable de todos los spots activos de todas las fuentes activas. Las columnas son: Hora, Frec (kHz), Indicativo DX, Modo, Comentario, Spotter, Banda y Fuente. Las casillas de verificación por banda debajo de **Bands:** alternan la visibilidad de cada banda de aficionados. Haga clic en **Clear** para vaciar la lista actual. Haga doble clic en cualquier fila para sintonizar el VFO activo a la frecuencia de ese spot y, cuando el spot contenga información de modo (por ejemplo, CW, FT8 o RTTY), cambie automáticamente la porción a ese modo.

### Pestaña Display

La pestaña **Display** controla cómo aparecen los spots en el panadapter.

| Control                          | Clave de configuración                                                    | Valor predeterminado                                                                          |
|----------------------------------|--------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **Spots:**                       | `IsSpotsEnabled`                                                         | Habilitado                                                                                    |
| **Memories:**                    | `IsMemoriesShownOnPanadapter`                                            | Deshabilitado                                                                                 |
| **Auto Mode:**                   | `SpotsAutoMode`                                                          | Habilitado                                                                                    |
| **Levels:**                      | `SpotsStackLevels`                                                       | —                                                                                             |
| **Position:**                    | `SpotsPosition`                                                          | —                                                                                             |
| **Font Size:**                   | `SpotsFontSize`                                                          | —                                                                                             |
| **Spot Lifetime:**               | `SpotsLifetime`                                                          | —                                                                                             |
| **Override Colors:**             | `IsSpotsOverrideColorsEnabled`                                           | —                                                                                             |
| **Override Background: Enabled** | `IsSpotsOverrideBackgroundColorsEnabled`                                 | —                                                                                             |
| **Override Background: Auto**    | `IsSpotsOverrideToAutoBackgroundColorEnabled`                            | —                                                                                             |
| **Background Opacity:**          | `SpotsOverrideBgOpacity`                                                 | 48                                                                                            |
| **DXCC Coloring**                | `DxccColoringEnabled`                                                    | —                                                                                             |
| **Log File (ADIF):**             | `DxccAdifPath`                                                           | —                                                                                             |
| **Auto-Reload Log:**             | `DxccAutoReload`                                                         | —                                                                                             |
| **Spot Lines:**                  | `IsSpotsLinesEnabled`                                                    | Habilitado                                                                                    |
| **Clear All Spots**              | —                                                                        | —                                                                                             |
| Total Spots:                     | Lectura en vivo de cuántos spots se están rastreando actualmente en todas las fuentes. | Se actualiza cuando se agregan o eliminan spots. Se restablece a 0 cuando se presiona **Clear All Spots**. |

**Spot Lines:** dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot. Desactívelo durante los concursos para reducir el desorden visual. La configuración se persiste como `IsSpotsLinesEnabled` y el valor predeterminado es Habilitado.

**Auto Mode** tiene como valor predeterminado **Enabled** (`SpotsAutoMode` tiene como valor predeterminado `True`). Si anteriormente dependía de que el Modo Automático estuviera desactivado de forma predeterminada, verifique esta configuración después de actualizar.

### Reporte de FreeDV Reporter

La pestaña **FreeDV** incluye una sección **Station Reporting** que permite a AetherSDR transmitir su actividad de estación al mapa público de FreeDV Reporter en `qso.freedv.org` siempre que el módem RADE esté activo. Esta función solo está presente en compilaciones compiladas con soporte WebSocket.

#### Habilitar el reporte

1. Abra la pestaña **FreeDV**.
2. Complete un indicativo y un cuadrado de cuadrícula válidos en los campos **Callsign:** y **Grid Square:** (vea a continuación). La casilla de verificación se niega a habilitarse si alguno de los campos está en blanco o no se puede resolver.
3. Marque **Enable FreeDV Reporter reporting when RADE is active** (`FreeDvAutoReport`). Si el indicativo o la cuadrícula no se pueden resolver, aparece un diálogo de advertencia y la casilla de verificación vuelve a estar desmarcada.

> **Nota:** Los datos del Reporter se publican en un mapa público compartido por la comunidad. No habilite el reporte con valores de marcador de posición.

#### Campo de indicativo

| Control | Clave de configuración | Valor predeterminado | Notas |
|---|---|---|---|
| **Callsign:** | `FreeDvMyCallsign` | — | El indicativo enviado al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use radio** está marcado. |
| **Use radio** | `FreeDvUseRadioCallsign` | True | Rellena previamente el indicativo desde el indicativo configurado en la radio y bloquea el campo como solo lectura. Se actualiza automáticamente si cambia el indicativo en Radio Setup. |

Cuando **Use radio** está marcado, el campo muestra el indicativo de la radio. Desmárquelo para ingresar un indicativo manualmente.

#### Campo de cuadrado de cuadrícula

| Control | Clave de configuración | Valor predeterminado | Notas |
|---|---|---|---|
| **Grid Square:** | `FreeDvMyGrid` | — | Cuadrado de cuadrícula Maidenhead enviado al mapa de FreeDV Reporter. El campo es de solo lectura cuando **Use GPS** está marcado. |
| **Use GPS** | `FreeDvUseGpsGrid` | True | Rellena previamente la cuadrícula desde el módulo GPS de la radio y bloquea el campo como solo lectura. Solo se muestra en modelos de radio que tienen hardware GPS. |

#### Mensaje de estación

| Control | Clave de configuración | Valor predeterminado | Notas |
|---|---|---|---|
| **Station Msg:** | `FreeDvMyMessage` | — | Texto libre opcional que se muestra junto a su indicativo en el mapa público de FreeDV Reporter. |

## Superposición de barrido de ROE

La versión V0.9.4 agrega una superposición de barrido de ROE que traza la ROE versus la frecuencia directamente en el panadapter. Una fuente externa (por ejemplo, una integración de analizador de antena) proporciona los datos llamando a `setSwrSweepPoints()`. El panadapter representa la curva a través de la capa interna `drawSwrSweep()`.

### Suministro de datos de barrido

Llame a `setSwrSweepPoints()` con un vector de valores `SwrSweepPoint`. Cada punto tiene dos campos:

| Campo | Tipo | Valor predeterminado | Descripción |
|---|---|---|---|
| `freqMhz` | `double` | `0.0` | Frecuencia de la medición en MHz. |
| `swr` | `float` | `1.0` | Valor de ROE en esa frecuencia. |

La firma del método es:

```
setSwrSweepPoints(points, running, currentFreqMhz, sourceLabel)
```

| Parámetro | Tipo | Valor predeterminado | Descripción |
|---|---|---|---|
| `points` | `QVector<SwrSweepPoint>` | — | Los datos de barrido a mostrar. |
| `running` | `bool` | `false` | Pase `true` mientras un barrido está en curso para indicar una traza en vivo e incompleta. |
| `currentFreqMhz` | `double` | `-1.0` | La frecuencia que se está barriendo actualmente. Pase `-1.0` para suprimir el cursor. |
| `sourceLabel` | `QString` | *(vacío)* | Etiqueta opcional que identifica la fuente de los datos de barrido, que se muestra en la superposición. |

### Limpieza de datos de barrido

Llame a `clearSwrSweepPoints()` para eliminar todos los datos de barrido y ocultar la superposición.

## Consejos

- RBN produce una tasa de spots muy alta. Establezca **Rate Limit:** en un valor que su pantalla pueda manejar antes de conectarse, para evitar inundar el panadapter.
- Los spots de WSJT-X son efímeros por naturaleza. Establezca **Spot Life:** para que coincida con la duración del ciclo de transmisión de FT8 o FT4 (15 o 7.5 segundos) si desea que los spots se borren entre períodos.
- El filtro **Calling Me** en la pestaña WSJT-X resalta las decodificaciones dirigidas específicamente a su indicativo, lo que facilita ver cuándo una estación está respondiendo a su CQ.
- **Auto Mode:** tiene como valor predeterminado Habilitado. Cambia automáticamente el modo de la porción cuando hace doble clic en un spot que incluye información de modo (por ejemplo, CW, FT8 o RTTY).
- Al hacer doble clic en un spot en la **Spot List**, ahora también se reenvía la sugerencia de modo del comentario del spot, por lo que la porción cambia a CW, SSB o al modo digital apropiado automáticamente, no solo la frecuencia.
- Desactive **Spot Lines:** durante los concursos para reducir el desorden visual en el panadapter. Vuelva a habilitarlo después para restaurar las guías de línea vertical (`IsSpotsLinesEnabled`).
- Antes de habilitar **Enable FreeDV Reporter reporting when RADE is active**, confirme que su indicativo y cuadrado de cuadrícula estén configurados correctamente. La casilla de verificación no se habilitará si alguno de los valores está en blanco.
- Llame a `clearSwrSweepPoints()` después de que se complete un barrido si no desea que la traza terminada persista en el panadapter.
