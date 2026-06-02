# Consultar activaciones POTA

AetherSDR puede obtener periódicamente las activaciones actuales de _Parks on the Air_ (POTA) desde `api.pota.app` y mostrarlas como puntos en su panadapter. Esto le permite encontrar operadores POTA activos sin necesidad de un navegador web separado o una fuente de clúster.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar esta función.
- El acceso HTTP saliente a `api.pota.app` no debe estar bloqueado por un cortafuegos.

## Pasos

1. Haga clic en `Settings > SpotHub...` para abrir el diálogo de SpotHub.
2. Haga clic en la pestaña **POTA**.
3. Revise el indicador **Server:**, que muestra `api.pota.app (HTTP polling)`. Este punto final es fijo y no se puede cambiar.
4. Establezca **Poll Interval:** en el número de segundos entre cada consulta. Este valor se guarda como `PotaPollInterval`.
5. Haga clic en **Start** para comenzar la consulta. El indicador de estado cambia a **Polling** cuando está activo. Haga clic en **Stop** para detener la consulta en cualquier momento.
6. Para cambiar el color usado para los puntos POTA en el panadapter, haga clic en **Spot Color:**. Seleccione un color del selector. Esto se guarda como `PotaSpotColor`.
7. Para iniciar la consulta automáticamente cada vez que se lance AetherSDR, active **Auto-start on startup**. Esto se guarda como `PotaAutoStart`.
8. Supervise las activaciones entrantes en la consola **POTA Activations** en la misma pestaña.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Indicador | Muestra el punto fijo de consulta: `api.pota.app (HTTP polling)`. No configurable. |
| **Poll Interval:** | Spinbox | Segundos entre consultas a la API de POTA. Se guarda como `PotaPollInterval`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene la consulta POTA. |
| **Auto-start on startup** | Botón de alternancia | Inicia automáticamente la consulta POTA al lanzar AetherSDR. Se guarda como `PotaAutoStart`. |
| **POTA Activations** | Campo de texto | Consola de solo lectura que muestra el flujo de activaciones. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los puntos POTA en el panadapter. Se guarda como `PotaSpotColor`. |
| Total Spots: | Indicador | Lectura en vivo de cuántos puntos se rastrean actualmente en todas las fuentes. Se actualiza cuando se añaden o borran puntos. Se reinicia a 0 al presionar **Clear All Spots**. |
| **Spot Lines:** | Botón de alternancia | Dibuja líneas verticales desde el espectro hasta cada etiqueta de punto. Habilitado por defecto. Deshabilitar durante concursos para reducir el desorden visual. Se guarda como `IsSpotsLinesEnabled`. Nuevo en v0.9.7. |
| Auto: | Botón de alternancia | Cambia automáticamente el modo de la porción (*slice*) al hacer clic en un punto que incluya información de modo (p.ej., CW, FT8, RTTY). Se guarda como `SpotAutoSwitchMode`. La clave de ajuste cambió de `SpotsAutoMode` en v26.5.1. |
| Signals (Signal History) | Botón de alternancia | Marcadores dorados para señales de ancho de voz detectadas en el panadapter. Se guarda como `SHistoryMarkersEnabled`. Nuevo en v26.5.1 (#2426). El mismo interruptor que View > Signal History Markers. |
| QRM (Signal History) | Botón de alternancia | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Se guarda como `SHistoryQrmEnabled`. Nuevo en v26.5.1 (#2426). El mismo interruptor que View > QRM History Markers. |
| Clear All | Botón pulsador | Borra todos los puntos DX, el feed de memoria, los marcadores de Signal History y los marcadores QRM del espectro. |
| **Levels:** | Deslizador | Número de filas de apilamiento vertical para los puntos. Rango 1-10. Por defecto 3. Se guarda como `SpotsMaxLevel`. |
| **Position:** | Deslizador | Posición vertical en el panadapter. Rango 0-100. Por defecto 50. Se guarda como `SpotsStartingHeightPercentage`. |
| **Font Size:** | Deslizador | Tamaño del texto del punto. Rango 8-32. Por defecto 16. Se guarda como `SpotFontSize`. |
| **Spot Lifetime:** | Deslizador | Segundos antes de que un punto se desvanezca. Pasos no lineales desde 10 seg hasta 24 h. Se guarda como `DxClusterSpotLifetimeSec`. |
| **Override Colors:** | Botón de alternancia | Fuerza un solo color de texto para todos los puntos. Se guarda como `IsSpotsOverrideColorsEnabled`. |
| Selector de color de texto de punto | Botón pulsador | Abre QColorDialog para elegir el color del texto del punto. Por defecto #FFFF00. Se guarda como `SpotsOverrideColor`. |
| **Override Background: Enabled** | Botón de alternancia | Habilita un color de fondo personalizado para los puntos. Se guarda como `IsSpotsOverrideBackgroundColorsEnabled`. |
| **Override Background: Auto** | Botón de alternancia | Selecciona automáticamente el color de fondo para contraste. Se guarda como `IsSpotsOverrideToAutoBackgroundColorEnabled`. |
| Selector de color de fondo de punto | Botón pulsador | Abre QColorDialog para el color de fondo del punto. Por defecto #000000. Se guarda como `SpotsOverrideBgColor`. |
| **Background Opacity:** | Deslizador | Opacidad del color de fondo del punto. Rango 0-100. Por defecto 48. Se guarda como `SpotsBackgroundOpacity`. |
| DXCC Coloring (sección) | Indicador | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor. |
| **DXCC Colors:** | Botón de alternancia | Colorea los puntos por estado trabajado/confirmado/necesario de DXCC. Se guarda como `IsDxccColoringEnabled`. La clave de ajuste cambió de `DxccColoringEnabled` en v26.5.1. |
| **Log File (ADIF):** | Botón pulsador | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Observa automáticamente el archivo en busca de cambios después de la selección. Se guarda como `DxccAdifFilePath`. La clave de ajuste cambió de `DxccAdifPath` en v26.5.1. La recarga automática siempre está habilitada cuando se selecciona un archivo. |
| **Imported:** (estadísticas DXCC) | Indicador | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: '<N> QSOs / <M> entities'. |
| Muestras de color DXCC (New DXCC / New Band / New Mode / Worked) | Botón pulsador | Abre un selector de color para cada categoría de estado DXCC. Se guarda como `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked`. Nuevo en v26.5.1. |
| Signal History (sección) | Indicador | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor. Nuevo en v26.5.1 (#2506). |
| **Marker Lifetime:** | Deslizador | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado. Rango 15-300 s. Por defecto 60 s. Se guarda como `SHistoryLifetimeS`. Nuevo en v26.5.1. |
| **QRM Gate:** | Deslizador | Cuánto tiempo debe persistir una portadora estrecha o una señal de banda ancha antes de clasificarse como QRM. Rango 3-30 s. Por defecto 6 s. Se guarda como `SHistoryQrmGateS`. Nuevo en v26.5.1. |
| **Edge Threshold:** | Deslizador | Umbral por encima del piso de ruido para el recorrido del borde de pendiente que refina el borde del lado de la portadora de S-History. Rango 1.0-10.0 dB. Por defecto 3.0 dB. Se guarda como `SHistorySoftEdgeDb`. Nuevo en v26.5.1. |
| Muestras de color Signal History (Signals / QRM) | Botón pulsador | Abre un selector de color para los marcadores de señal de voz (dorados) y los marcadores QRM (rojos). Por defecto #FFC800 / #FF0000. Se guarda como `SHistoryColorSignals` / `SHistoryColorQrm`. Nuevo en v26.5.1. |
| **Snap to Step:** | Botón de alternancia | Redondea el clic para sintonizar de S-History al múltiplo más cercano del tamaño de paso de la porción activa, ocultando el pequeño desplazamiento de la portadora. Deshabilitado por defecto. Se guarda como `SHistorySnapToStep`. Nuevo en v26.5.1. |

## Controles de la pestaña Cluster

Los siguientes controles aparecen en la pestaña **Cluster** para conexiones telnet a clústeres DX.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Campo de texto | Nombre de host del clúster DX al que conectarse. Se guarda como `ClusterHost`. |
| **Port:** | Spinbox | Puerto telnet en el clúster DX. Rango 1-65535. Se guarda como `ClusterPort`. |
| **Callsign:** | Campo de texto | Indicativo de inicio de sesión enviado al clúster. Se guarda como `ClusterCallsign`. |
| **Connect / Disconnect** | Botón pulsador | Activa o desactiva la conexión telnet al clúster. |
| **Auto-connect on startup** | Botón de alternancia | Conecta automáticamente al clúster al inicio. Se guarda como `ClusterAutoConnect`. |
| **Cluster Console** | Campo de texto | Consola telnet de solo lectura del tráfico bruto del clúster. |
| **Send** | Botón pulsador | Envía un comando escrito al clúster. |
| **Spot Color:** | Botón pulsador | Abre un selector de color para los puntos del clúster. Se guarda como `ClusterSpotColor`. |
| **Startup Commands…** | Botón pulsador | Abre el editor de comandos de inicio. Los comandos se envían automáticamente después de cada inicio de sesión. Un comando por línea. Se guarda como `DxClusterStartupCommands`. Nuevo en v26.5.2.1 (#2683). |

## Controles de la pestaña RBN

Los siguientes controles aparecen en la pestaña **RBN** para conexiones telnet a la Red de Balizas Inversas (_Reverse Beacon Network_).

| Control | Tipo | Comportamiento |
|---|---|---|
| **Server:** | Campo de texto | Nombre de host telnet de RBN. Se guarda como `RbnHost`. |
| **Port:** | Spinbox | Puerto telnet de RBN. Rango 1-65535. Se guarda como `RbnPort`. |
| **Callsign:** | Campo de texto | Indicativo de inicio de sesión para RBN. Se guarda como `RbnCallsign`. |
| **Rate Limit:** | Spinbox | Limita los puntos RBN por segundo. Se guarda como `RbnRateLimit`. |
| **Connect / Disconnect (RBN)** | Botón pulsador | Activa o desactiva la conexión RBN. |
| **Auto-connect on startup (RBN)** | Botón de alternancia | Inicia RBN automáticamente. Se guarda como `RbnAutoConnect`. |
| **RBN Console** | Campo de texto | Consola de solo lectura del tráfico RBN. |
| **Send (RBN)** | Botón pulsador | Envía un comando a RBN. |
| **Spot Color: (RBN)** | Botón pulsador | Selector de color para puntos RBN. Se guarda como `RbnSpotColor`. |
| **Startup Commands…** | Botón pulsador | Abre el editor de comandos de inicio para la instancia RBN. Los comandos se envían automáticamente después de cada inicio de sesión. Un comando por línea. Se guarda como `RbnStartupCommands`. Nuevo en v26.5.2.1 (#2683). |

## Controles de la pestaña WSJT-X

Los siguientes controles aparecen en la pestaña **WSJT-X** para la escucha de mensajes UDP.

| Control | Tipo | Comportamiento |
|---|---|---|
| **Address:** | Campo de texto | Dirección de enlace UDP para mensajes de WSJT-X. Se guarda como `WsjtxAddress`. |
| **Port:** | Spinbox | Puerto UDP para WSJT-X. Rango 1-65535. Se guarda como `WsjtxPort`. |
| **Start / Stop** | Botón pulsador | Inicia o detiene el listener UDP. |
| **Auto-start on startup (WSJT-X)** | Botón de alternancia | Inicia automáticamente el listener al inicio. Se guarda como `WsjtxAutoStart`. |
| **CQ** | Casilla de verificación | Muestra solo llamadas CQ de WSJT-X. Se guarda como `WsjtxFilterCQ`. |
| **CQ POTA** | Casilla de verificación | Muestra llamadas CQ POTA. Se guarda como `WsjtxFilterPOTA`. |
| **Calling Me** | Casilla de verificación | Muestra solo decodificaciones dirigidas a su indicativo. Se guarda como `WsjtxFilterCallingMe`. |
| **CQ color / POTA color / Calling Me color / Default color** | Botón pulsador | Selectores de color para cada categoría de punto WSJT-X. Se guardan como `WsjtxColorCQ`, `WsjtxColorPOTA`, `WsjtxColorCallingMe`, `WsjtxColorDefault`. |
| **WSJT-X Decodes** | Campo de texto | Consola de transmisiones decodificadas. |
| **Spot Life:** | Spinbox | Segundos que los puntos WSJT-X permanecen en el panadapter. Se guarda como `WsjtxSpotLife`. |

## Controles de la pestaña SpotCollector

Los siguientes controles aparecen en la pestaña **SpotCollector** para las transmisiones UDP de SpotCollector de Ham Radio Deluxe.

| Control | Tipo | Comportamiento |
|---|---|---|
| **UDP Port:** | Spinbox | Puerto UDP en el que transmite SpotCollector. Rango 1-65535. Se guarda como `SpotCollectorPort`. |
| **Start / Stop (SpotCollector)** | Botón pulsador | Inicia o detiene el listener UDP. |
| **Auto-start on startup (
