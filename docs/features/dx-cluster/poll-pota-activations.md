# SpotHub (Diálogo de DX Cluster)

AetherSDR puede conectarse a múltiples fuentes de spots DX—DX cluster telnet, Reverse Beacon Network (RBN), WSJT-X, SpotCollector, POTA y FreeDV—y mostrar los spots en su panadapter. El diálogo unificado SpotHub centraliza toda la configuración de conexión, filtros, colores y visualización.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar las fuentes de spots.
- Para conexiones DX cluster y RBN, el acceso telnet saliente a los servidores respectivos no debe estar bloqueado por un firewall.
- Para WSJT-X, SpotCollector y FreeDV, las aplicaciones respectivas deben estar en ejecución y configuradas para transmitir en los puertos o endpoint WebSocket esperados.
- Para POTA, el acceso HTTP saliente a `api.pota.app` no debe estar bloqueado por un firewall.

## Abrir SpotHub

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo **SpotHub**.

El diálogo está organizado en pestañas para cada fuente de spots, más una pestaña unificada **Spot List** y una pestaña **Display** para la configuración de visualización en el panadapter.

## Sondeo de activaciones POTA

Esta sección describe cómo configurar la pestaña **POTA** para obtener periódicamente las activaciones actuales de Parks on the Air desde `api.pota.app` y mostrarlas como spots en su panadapter.

### Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo SpotHub.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:**, que muestra `api.pota.app (HTTP polling)`. Este endpoint es fijo y no se puede cambiar.
4. Establezca **Poll Interval:** al número de segundos entre cada sondeo. Este valor se guarda como `PotaPollInterval`.
5. Haga clic en **Start** para comenzar el sondeo. El indicador de estado cambia a **Polling** cuando está activo. Haga clic en **Stop** para detener el sondeo en cualquier momento.
6. Para cambiar el color utilizado para los spots POTA en el panadapter, haga clic en **Spot Color:**. Seleccione un color del selector. Esto se guarda como `PotaSpotColor`.
7. Para iniciar el sondeo automáticamente cada vez que AetherSDR se inicie, haga clic en **Auto-start on startup** para activarlo. Esto se guarda como `PotaAutoStart`.
8. Supervise las activaciones entrantes en la consola **POTA Activations** en la misma pestaña.

### Controles de la pestaña POTA

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Muestra el endpoint de sondeo fijo: `api.pota.app (HTTP polling)`. No configurable. |
| **Poll Interval:** | Spinbox | Segundos entre sondeos a la API de POTA. Se guarda como `PotaPollInterval`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene el sondeo de POTA. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente el sondeo de POTA cuando AetherSDR se inicia. Se guarda como `PotaAutoStart`. |
| **POTA Activations** | Campo de texto | Consola de solo lectura que muestra el flujo de activaciones. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los spots POTA en el panadapter. Se guarda como `PotaSpotColor`. |

## Controles de la pestaña Cluster

Los siguientes controles aparecen en la pestaña **Cluster** para conexiones telnet de DX cluster.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Campo de texto | Nombre de host del DX cluster al que conectarse. Se guarda como `ClusterHost`. |
| **Port:** | Spinbox | Puerto telnet del DX cluster. Rango 1-65535. Se guarda como `ClusterPort`. |
| **Callsign:** | Campo de texto | Indicativo de inicio de sesión enviado al cluster. Se guarda como `ClusterCallsign`. |
| **Connect / Disconnect** | Botón pulsador | Alterna la conexión telnet al cluster. |
| **Auto-connect on startup** | Botón de alternancia | Conecta automáticamente el cluster al iniciar. Se guarda como `ClusterAutoConnect`. |
| **Cluster Console** | Campo de texto | Consola telnet de solo lectura con el tráfico bruto del cluster. |
| **Send** | Botón pulsador | Envía un comando escrito al cluster. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los spots del cluster. Se guarda como `ClusterSpotColor`. |

## Controles de la pestaña RBN

Los siguientes controles aparecen en la pestaña **RBN** para conexiones telnet de Reverse Beacon Network.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Campo de texto | Hostname telnet de RBN. Se guarda como `RbnHost`. |
| **Port:** | Spinbox | Puerto telnet de RBN. Rango 1-65535. Se guarda como `RbnPort`. |
| **Callsign:** | Campo de texto | Indicativo de inicio de sesión para RBN. Se guarda como `RbnCallsign`. |
| **Rate Limit:** | Spinbox | Limita los spots RBN por segundo. Se guarda como `RbnRateLimit`. |
| **Connect / Disconnect (RBN)** | Botón pulsador | Alterna la conexión RBN. |
| **Auto-connect on startup (RBN)** | Botón de alternancia | Inicia RBN automáticamente. Se guarda como `RbnAutoConnect`. |
| **RBN Console** | Campo de texto | Consola de solo lectura del tráfico RBN. |
| **Send (RBN)** | Botón pulsador | Envía comandos a RBN. |
| **Spot Color: (RBN)** | Botón pulsador | Selector de color para los spots RBN. Se guarda como `RbnSpotColor`. |

## Controles de la pestaña WSJT-X

Los siguientes controles aparecen en la pestaña **WSJT-X** para la escucha de mensajes UDP.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Address:** | Campo de texto | Dirección de enlace UDP para mensajes WSJT-X. Se guarda como `WsjtxAddress`. |
| **Port:** | Spinbox | Puerto UDP para WSJT-X. Rango 1-65535. Se guarda como `WsjtxPort`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene el receptor UDP. |
| **Auto-start on startup (WSJT-X)** | Botón de alternancia | Inicia automáticamente el receptor al arrancar. Se guarda como `WsjtxAutoStart`. |
| **CQ** | Casilla de verificación | Muestra solo llamadas CQ de WSJT-X. Se guarda como `WsjtxFilterCQ`. |
| **CQ POTA** | Casilla de verificación | Muestra llamadas CQ POTA. Se guarda como `WsjtxFilterPOTA`. |
| **Calling Me** | Casilla de verificación | Muestra solo decodificaciones dirigidas a su indicativo. Se guarda como `WsjtxFilterCallingMe`. |
| **CQ color / POTA color / Calling Me color / Default color** | Botón pulsador | Selectores de color para cada categoría de spot WSJT-X. Se guardan como `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault`. |
| **WSJT-X Decodes** | Campo de texto | Consola de transmisiones decodificadas. |
| **Spot Life:** | Spinbox | Segundos que los spots WSJT-X permanecen en el panadapter. Se guarda como `WsjtxSpotLife`. |

## Controles de la pestaña SpotCollector

Los siguientes controles aparecen en la pestaña **SpotCollector** para la escucha de transmisiones UDP de Ham Radio Deluxe SpotCollector.

| Control | Tipo | Comportamiento |
|---|---|---|
| **UDP Port:** | Spinbox | Puerto UDP en el que SpotCollector transmite. Rango 1-65535. Se guarda como `SpotCollectorPort`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene el receptor UDP. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente el receptor al arrancar. Se guarda como `SpotCollectorAutoStart`. |
| **SpotCollector Spots** | Campo de texto | Consola de solo lectura de los spots recibidos de SpotCollector. |

## Controles de la pestaña FreeDV

Los siguientes controles aparecen en la pestaña **FreeDV** para el flujo WebSocket de spots del reporter de QSO FreeDV. Esta pestaña solo está disponible cuando AetherSDR se compila con soporte WebSocket.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Muestra el endpoint WebSocket fijo: `qso.freedv.org (WebSocket)`. No configurable. |
| **Start / Stop** | Botón pulsador | Conecta o desconecta el WebSocket de FreeDV. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente FreeDV al arrancar. Se guarda como `FreeDvAutoStart`. |
| **FreeDV Spots** | Campo de texto | Consola de solo lectura de la actividad de FreeDV. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los spots FreeDV. Se guarda como `FreeDvSpotColor`. |

## Pestaña Spot List

La pestaña **Spot List** muestra una tabla unificada y buscable de todos los spots en vivo de todas las fuentes conectadas.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Bands:** | Grupo de casillas de verificación | Las casillas de verificación por banda alternan la visibilidad en la tabla. Una casilla por banda (160m, 80m, 60m, 40m, 30m, 20m, 17m, 15m, 12m, 10m, 6m, 2m, etc.). Las casillas usan un diseño de flujo que se envuelve a una nueva fila cuando el espacio horizontal es reducido, manteniendo las etiquetas legibles. |
| **Clear** | Botón pulsador | Vacía la lista de spots actual. |
| **Spot table** | Lista / Tabla | Tabla ordenable de spots. Haga doble clic en una fila para sintonizar la radio a esa frecuencia. Columnas: Time, Freq, DX Call, Comment, Spotter, Band, Mode, Source. La visibilidad de las columnas se puede alternar mediante un menú contextual con clic derecho en el encabezado de la tabla; el menú permanece abierto mientras se alternan varias columnas, lo que permite mostrar u ocultar varias columnas de una sola vez. Tanto la columna **Time** como **Freq** son ordenables; haga clic en el encabezado de cualquiera de ellas para reordenar la tabla. |

## Pestaña Display

La pestaña **Display** controla cómo se visualizan los spots en el panadapter, incluidos los parámetros ajustables de Signal History y el coloreado DXCC. En v26.5.1, la pestaña se reorganizó para tener una fila superior de alternancias, controles deslizantes comunes y luego una sección de dos columnas con DXCC Coloring (izquierda) y Signal History (derecha).

### Controles de la pestaña Display

| Control | Tipo | Comportamiento |
|---|---|---|
| **Spots:** | Botón de alternancia | Alternancia maestra para la superposición de spots DX. Se guarda como `IsSpotsEnabled`. |
| **Memories:** | Botón de alternancia | Alterna la superposición de canales de memoria en el panadapter. Se guarda como `IsMemorySpotsEnabled`. |
| **Auto:** | Botón de alternancia | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). Se guarda como `SpotAutoSwitchMode`. |
| **Signals (Signal History)** | Botón de alternancia | Marcadores dorados para señales detectadas de ancho de voz en el panadapter. Se guarda como `SHistoryMarkersEnabled`. Misma alternancia que View > Signal History Markers. |
| **QRM (Signal History)** | Botón de alternancia | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Se guarda como `SHistoryQrmEnabled`. Misma alternancia que View > QRM History Markers. |
| **Clear All** | Botón pulsador | Borra todos los spots DX, el flujo de memorias, los marcadores de Signal History y los marcadores QRM del espectro. |
| **Levels:** | Control deslizante | Número de filas de apilamiento vertical para los spots. Rango 1-10. Valor predeterminado 3. Se guarda como `SpotsMaxLevel`. |
| **Position:** | Control deslizante | Posición vertical en el panadapter. Rango 0-100. Valor predeterminado 50. Se guarda como `SpotsStartingHeightPercentage`. |
| **Font Size:** | Control deslizante | Tamaño del texto de los spots. Rango 8-32. Valor predeterminado 16. Se guarda como `SpotFontSize`. |
| **Spot Lifetime:** | Control deslizante | Segundos antes de que un spot se desvanezca. Pasos no lineales de 10 segundos a 24 horas. Se guarda como `DxClusterSpotLifetimeSec`. |
| **Override Colors:** | Botón de alternancia | Fuerza un color de texto único para todos los spots. Se guarda como `IsSpotsOverrideColorsEnabled`. |
| Selector de color de texto de spots | Botón pulsador | Abre QColorDialog para elegir el color de texto de los spots. Valor predeterminado #FFFF00. Se guarda como `SpotsOverrideColor`. |
| **Override Background: Enabled** | Botón de alternancia | Habilita un color de fondo personalizado para los spots. Se guarda como `IsSpotsOverrideBackgroundColorsEnabled`. |
| **Override Background: Auto** | Botón de alternancia | Selecciona automáticamente el color de fondo para contraste. Se guarda como `IsSpotsOverrideToAutoBackgroundColorEnabled`. |
| Selector de color de fondo de spots | Botón pulsador | Abre QColorDialog para el color de fondo de los spots. Valor predeterminado #000000. Se guarda como `SpotsOverrideBgColor`. |
| **Background Opacity:** | Control deslizante | Opacidad del color de fondo de los spots. Rango 0-100. Valor predeterminado 48. Se guarda como `SpotsBackgroundOpacity`. |
| **Spot Lines:** | Botón de alternancia | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. Se guarda como `IsSpotsLinesEnabled`. |
| **Total Spots:** | Indicador | Conteo en vivo de spots actualmente rastreados en todas las fuentes. |
| DXCC Coloring (sección) | Indicador | Encabezado de sección para los controles de coloreado DXCC en la columna izquierda debajo del divisor. |
| **DXCC Colors:** | Botón de alternancia | Colorea los spots según el estado DXCC trabajado/confirmado/necesario. Se guarda como `IsDxccColoringEnabled`. |
| **Log File (ADIF):** | Botón pulsador | Carga un archivo de registro ADIF para impulsar el coloreado DXCC. Observa automáticamente el archivo para detectar cambios después de la selección. Se guarda como `DxccAdifFilePath`. |
| **Imported:** (estadísticas DXCC) | Indicador | Muestra el conteo de QSO y el conteo de entidades cuando se carga un registro. Formato:
