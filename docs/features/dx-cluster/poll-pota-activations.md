# SpotHub (Diálogo de Cluster DX)

AetherSDR puede conectarse a múltiples fuentes de spots DX—telnet de cluster DX, Red de Balizas Inversa (RBN), WSJT-X, SpotCollector, POTA y FreeDV—y mostrar los spots en su panadapter. El diálogo unificado de SpotHub centraliza todas las configuraciones de conexión, filtro, color y visualización.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar las fuentes de spots.
- Para conexiones de cluster DX y RBN, el acceso telnet saliente a los servidores respectivos no debe estar bloqueado por un cortafuegos.
- Para WSJT-X, SpotCollector y FreeDV, las aplicaciones respectivas deben estar en ejecución y configuradas para transmitir en los puertos o punto final WebSocket esperados.
- Para POTA, el acceso HTTP saliente a `api.pota.app` no debe estar bloqueado por un cortafuegos.

## Abrir SpotHub

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo **SpotHub**.

El diálogo está organizado en pestañas para cada fuente de spots, más una pestaña unificada **Spot List** y una pestaña **Display** para la configuración de visualización en el panadapter.

## Consultar activaciones de POTA

Esta sección describe cómo configurar la pestaña **POTA** para obtener periódicamente activaciones actuales de Parks on the Air desde `api.pota.app` y mostrarlas como spots en su panadapter.

### Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:**, que muestra `api.pota.app (HTTP polling)`. Este punto final es fijo y no se puede cambiar.
4. Establezca **Poll Interval:** en el número de segundos entre cada consulta. Este valor se persiste como `PotaPollInterval`.
5. Haga clic en **Start** para comenzar la consulta. El indicador de estado cambia a **Polling** cuando está activo. Haga clic en **Stop** para detener la consulta en cualquier momento.
6. Para cambiar el color utilizado para los spots de POTA en el panadapter, haga clic en **Spot Color:**. Seleccione un color del selector. Esto se persiste como `PotaSpotColor`.
7. Para iniciar la consulta automáticamente cada vez que se lance AetherSDR, active **Auto-start on startup** para que esté habilitado. Esto se persiste como `PotaAutoStart`.
8. Supervise las activaciones entrantes en la consola **POTA Activations** en la misma pestaña.

### Controles de la pestaña POTA

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Muestra el punto final de consulta fijo: `api.pota.app (HTTP polling)`. No configurable. |
| **Poll Interval:** | Spinbox | Segundos entre consultas a la API de POTA. Se persiste como `PotaPollInterval`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene la consulta de POTA. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente la consulta de POTA al lanzar AetherSDR. Se persiste como `PotaAutoStart`. |
| **POTA Activations** | Campo de texto | Consola de solo lectura que muestra el flujo de activaciones. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los spots de POTA en el panadapter. Se persiste como `PotaSpotColor`. |

## Controles de la pestaña Cluster

Los siguientes controles aparecen en la pestaña **Cluster** para conexiones telnet de cluster DX.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Campo de texto | Nombre de host del cluster DX al que conectarse. Se persiste como `ClusterHost`. |
| **Port:** | Spinbox | Puerto telnet del cluster DX. Rango 1-65535. Se persiste como `ClusterPort`. |
| **Callsign:** | Campo de texto | Indicativo de inicio de sesión enviado al cluster. Se persiste como `ClusterCallsign`. |
| **Connect / Disconnect** | Botón pulsador | Alterna la conexión telnet al cluster. |
| **Auto-connect on startup** | Botón de alternancia | Conecta automáticamente el cluster al inicio. Se persiste como `ClusterAutoConnect`. |
| **Cluster Console** | Campo de texto | Consola telnet de solo lectura del tráfico bruto del cluster. |
| **Send** | Botón pulsador | Envía un comando escrito al cluster. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los spots del cluster. Se persiste como `ClusterSpotColor`. |

## Controles de la pestaña RBN

Los siguientes controles aparecen en la pestaña **RBN** para conexiones telnet de la Red de Balizas Inversa.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Campo de texto | Nombre de host telnet de RBN. Se persiste como `RbnHost`. |
| **Port:** | Spinbox | Puerto telnet de RBN. Rango 1-65535. Se persiste como `RbnPort`. |
| **Callsign:** | Campo de texto | Indicativo de inicio de sesión para RBN. Se persiste como `RbnCallsign`. |
| **Rate Limit:** | Spinbox | Limita los spots de RBN por segundo. Se persiste como `RbnRateLimit`. |
| **Connect / Disconnect (RBN)** | Botón pulsador | Alterna la conexión RBN. |
| **Auto-connect on startup (RBN)** | Botón de alternancia | Inicia RBN automáticamente. Se persiste como `RbnAutoConnect`. |
| **RBN Console** | Campo de texto | Consola de solo lectura del tráfico de RBN. |
| **Send (RBN)** | Botón pulsador | Envía un comando a RBN. |
| **Spot Color: (RBN)** | Botón pulsador | Selector de color para spots de RBN. Se persiste como `RbnSpotColor`. |

## Controles de la pestaña WSJT-X

Los siguientes controles aparecen en la pestaña **WSJT-X** para la escucha de mensajes UDP.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Address:** | Campo de texto | Dirección de enlace UDP para mensajes de WSJT-X. Se persiste como `WsjtxAddress`. |
| **Port:** | Spinbox | Puerto UDP para WSJT-X. Rango 1-65535. Se persiste como `WsjtxPort`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene el listener UDP. |
| **Auto-start on startup (WSJT-X)** | Botón de alternancia | Inicia automáticamente el listener al inicio. Se persiste como `WsjtxAutoStart`. |
| **CQ** | Casilla de verificación | Muestra solo llamadas CQ de WSJT-X. Se persiste como `WsjtxFilterCQ`. |
| **CQ POTA** | Casilla de verificación | Muestra llamadas CQ POTA. Se persiste como `WsjtxFilterPOTA`. |
| **Calling Me** | Casilla de verificación | Muestra solo decodificaciones dirigidas a su indicativo. Se persiste como `WsjtxFilterCallingMe`. |
| **CQ color / POTA color / Calling Me color / Default color** | Botón pulsador | Selectores de color para cada categoría de spot de WSJT-X. Se persisten como `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault`. |
| **WSJT-X Decodes** | Campo de texto | Consola de transmisiones decodificadas. |
| **Spot Life:** | Spinbox | Segundos que los spots de WSJT-X permanecen en el panadapter. Se persiste como `WsjtxSpotLife`. |

## Controles de la pestaña SpotCollector

Los siguientes controles aparecen en la pestaña **SpotCollector** para la escucha de la transmisión UDP de Ham Radio Deluxe SpotCollector.

| Control | Tipo | Comportamiento |
|---|---|---|
| **UDP Port:** | Spinbox | Puerto UDP en el que transmite SpotCollector. Rango 1-65535. Se persiste como `SpotCollectorPort`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene el listener UDP. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente el listener al inicio. Se persiste como `SpotCollectorAutoStart`. |
| **SpotCollector Spots** | Campo de texto | Consola de solo lectura de los spots de SpotCollector recibidos. |

## Controles de la pestaña FreeDV

Los siguientes controles aparecen en la pestaña **FreeDV** para el flujo WebSocket de spots del reportero QSO de FreeDV. Esta pestaña solo está disponible cuando AetherSDR se compila con soporte WebSocket.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Muestra el punto final WebSocket fijo: `qso.freedv.org (WebSocket)`. No configurable. |
| **Start / Stop** | Botón pulsador | Conecta o desconecta el WebSocket de FreeDV. |
| **Auto-start on startup** | Botón de alternancia | Inicia FreeDV automáticamente al inicio. Se persiste como `FreeDvAutoStart`. |
| **FreeDV Spots** | Campo de texto | Consola de solo lectura de la actividad de FreeDV. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los spots de FreeDV. Se persiste como `FreeDvSpotColor`. |

## Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y buscable de todos los spots activos de todas las fuentes conectadas.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Bands:** | Grupo de casillas de verificación | Las casillas de verificación por banda alternan la visibilidad en la tabla. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas usan un diseño de flujo que pasa a una nueva fila cuando el espacio horizontal es escaso, manteniendo las etiquetas legibles. |
| **Clear** | Botón pulsador | Vacía la lista de spots actual. |
| **Spot table** | Lista / Tabla | Tabla ordenable de spots. Haga doble clic en una fila para sintonizar la radio a esa frecuencia. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. La visibilidad de las columnas se puede alternar mediante un menú contextual con clic derecho en el encabezado de la tabla; el menú permanece abierto mientras se alternan varias columnas, lo que permite mostrar u ocultar varias columnas en una sola pasada. |

## Pestaña Display

La pestaña **Display** controla cómo se visualizan los spots en el panadapter, incluyendo parámetros ajustables de Signal History y coloración de DXCC. En la v26.5.1, la pestaña se reorganizó para tener una fila superior de botones de alternancia, controles deslizantes comunes, luego una sección de dos columnas con DXCC Coloring (izquierda) y Signal History (derecha).

### Controles de la pestaña Display

| Control | Tipo | Comportamiento |
|---|---|---|
| **Spots:** | Botón de alternancia | Activación maestra de la superposición de spots DX. Se persiste como `IsSpotsEnabled`. |
| **Memories:** | Botón de alternancia | Alterna la superposición de canales de memoria en el panadapter. Se persiste como `IsMemorySpotsEnabled`. |
| **Auto:** | Botón de alternancia | Cambia automáticamente el modo del slice al hacer clic en un spot que incluye información de modo (p. ej., CW, FT8, RTTY). Se persiste como `SpotAutoSwitchMode`. |
| **Signals (Signal History)** | Botón de alternancia | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Se persiste como `SHistoryMarkersEnabled`. Misma alternancia que View > Signal History Markers. |
| **QRM (Signal History)** | Botón de alternancia | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Se persiste como `SHistoryQrmEnabled`. Misma alternancia que View > QRM History Markers. |
| **Clear All** | Botón pulsador | Limpia todos los spots DX, el flujo de memoria, los marcadores de Signal History y los marcadores de QRM del espectro. |
| **Levels:** | Control deslizante | Número de filas de apilamiento vertical para spots. Rango 1-10. Valor predeterminado 3. Se persiste como `SpotsMaxLevel`. |
| **Position:** | Control deslizante | Posición vertical en el panadapter. Rango 0-100. Valor predeterminado 50. Se persiste como `SpotsStartingHeightPercentage`. |
| **Font Size:** | Control deslizante | Tamaño del texto de los spots. Rango 8-32. Valor predeterminado 16. Se persiste como `SpotFontSize`. |
| **Spot Lifetime:** | Control deslizante | Segundos antes de que un spot se desvanezca. Pasos no lineales desde 10 seg hasta 24 horas. Se persiste como `DxClusterSpotLifetimeSec`. |
| **Override Colors:** | Botón de alternancia | Fuerza un solo color de texto para todos los spots. Se persiste como `IsSpotsOverrideColorsEnabled`. |
| Selector de color de texto de spot | Botón pulsador | Abre QColorDialog para elegir el color del texto del spot. Valor predeterminado #FFFF00. Se persiste como `SpotsOverrideColor`. |
| **Override Background: Enabled** | Botón de alternancia | Habilita un color de fondo personalizado para los spots. Se persiste como `IsSpotsOverrideBackgroundColorsEnabled`. |
| **Override Background: Auto** | Botón de alternancia | Selecciona automáticamente el color de fondo para contraste. Se persiste como `IsSpotsOverrideToAutoBackgroundColorEnabled`. |
| Selector de color de fondo de spot | Botón pulsador | Abre QColorDialog para el color de fondo del spot. Valor predeterminado #000000. Se persiste como `SpotsOverrideBgColor`. |
| **Background Opacity:** | Control deslizante | Opacidad del color de fondo del spot. Rango 0-100. Valor predeterminado 48. Se persiste como `SpotsBackgroundOpacity`. |
| **Spot Lines:** | Botón de alternancia | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactive durante concursos para reducir el desorden visual. Se persiste como `IsSpotsLinesEnabled`. |
| **Total Spots:** | Indicador | Conteo en vivo de spots actualmente rastreados en todas las fuentes. |
| DXCC Coloring (sección) | Indicador | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor. |
| **DXCC Colors:** | Botón de alternancia | Colorea los spots por estado de DXCC trabajado/confirmado/necesitado. Se persiste como `IsDxccColoringEnabled`. |
| **Log File (ADIF):** | Botón pulsador | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. Se persiste como `DxccAdifFilePath`. |
| **Imported:** (estadísticas DXCC) | Indicador | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: `<N> QSOs / <M> entities`. |
| Muestras de color DXCC (New DXCC / New Band
