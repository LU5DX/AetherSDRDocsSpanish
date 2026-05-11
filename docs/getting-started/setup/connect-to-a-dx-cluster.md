# Conectarse a un clúster DX

El diálogo SpotHub de AetherSDR le permite conectarse a un clúster DX por telnet y mostrar los spots entrantes como superposiciones en el panadaptador. Utilice esta página para realizar su primera conexión y, opcionalmente, reconectarse automáticamente en cada inicio.

## Antes de comenzar

- Conozca el nombre del host (o dirección IP) y el puerto telnet del clúster DX elegido (por ejemplo, `dxc.k0xm.net` en el puerto `7373`).
- Conozca el indicativo que utilizará para iniciar sesión en el clúster.

## Pasos

1. Abra `Settings > SpotHub...`.
2. Haga clic en la pestaña **Cluster**.
3. En el campo **Server:**, escriba el nombre del host o la dirección IP del clúster. Esto se guarda en `ClusterHost`.
4. En el campo **Port:**, establezca el puerto telnet (1–65535). Esto se guarda en `ClusterPort`.
5. En el campo **Callsign:**, escriba su indicativo. Esto se guarda en `ClusterCallsign`.
6. Haga clic en **Connect**.
   - El indicador de estado cambia a **Connected** y la etiqueta del botón cambia a **Disconnect**.
   - El tráfico entrante del clúster aparece en la pantalla de solo lectura **Cluster Console**.
7. Para reconectarse automáticamente cada vez que AetherSDR se inicie, active **Auto-connect on startup**. Esto se guarda en `ClusterAutoConnect`.

## Qué hace cada control

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Server:** | Nombre del host o dirección IP del servidor telnet del clúster DX. | `ClusterHost` |
| **Port:** | Puerto telnet. Rango válido: 1–65535. | `ClusterPort` |
| **Callsign:** | Indicativo de inicio de sesión enviado al clúster al conectarse. | `ClusterCallsign` |
| **Connect / Disconnect** | Alterna la conexión telnet. La etiqueta muestra la acción actual. | — |
| **Auto-connect on startup** | Se conecta al clúster automáticamente cuando AetherSDR se inicia. | `ClusterAutoConnect` |
| **Cluster Console** | Pantalla de solo lectura del tráfico telnet en bruto del clúster. | — |
| **Send** (línea de comandos) | Envía un comando escrito al clúster mientras está conectado. | — |
| **Spot Color:** | Abre un selector de color para las superposiciones de spots del clúster en el panadaptador. | `ClusterSpotColor` |
| **Spots:** (pestaña Display) | Activación principal para la superposición de spots DX en el panadaptador. Predeterminado: Activado. | `IsSpotsEnabled` |
| **Memories:** (pestaña Display) | Alterna la superposición de canales de memoria en el panadaptador. Predeterminado: Desactivado. | `IsMemorySpotsEnabled` |
| **Auto:** (pestaña Display) | Cambia automáticamente el modo del slice al hacer clic en un spot que incluya información de modo (p. ej., CW, FT8, RTTY). Predeterminado: Activado. La clave de configuración cambió de `SpotsAutoMode` a `SpotAutoSwitchMode` en v26.5.1. | `SpotAutoSwitchMode` |
| **Signals (Signal History)** (pestaña Display) | Marcadores dorados para señales detectadas de ancho de voz en el panadaptador. Nuevo en v26.5.1 (#2426). La misma activación que View > Signal History Markers. | `SHistoryMarkersEnabled` |
| **QRM (Signal History)** (pestaña Display) | Marcadores rojos para portadoras persistentes e interferencia de banda ancha. Nuevo en v26.5.1 (#2426). La misma activación que View > QRM History Markers. | `SHistoryQrmEnabled` |
| **Clear All** (pestaña Display) | Limpia todos los spots DX, la alimentación de memoria y los marcadores de Signal History y QRM del espectro. | — |
| **Levels:** (pestaña Display) | Número de filas de apilamiento vertical para spots (1–10). Predeterminado: 3. | `SpotsMaxLevel` |
| **Position:** (pestaña Display) | Posición vertical en el panadaptador (0–100). Predeterminado: 50. | `SpotsStartingHeightPercentage` |
| **Font Size:** (pestaña Display) | Tamaño del texto del spot (8–32). Predeterminado: 16. | `SpotFontSize` |
| **Spot Lifetime:** (pestaña Display) | Segundos antes de que un spot se desvanezca (10 seg – 24 horas, pasos no lineales). | `DxClusterSpotLifetimeSec` |
| **Override Colors:** (pestaña Display) | Fuerza un solo color de texto para todos los spots. | `IsSpotsOverrideColorsEnabled` |
| **Selector de color de texto del spot** (pestaña Display) | Abre QColorDialog para elegir el color del texto del spot. Predeterminado: #FFFF00. | `SpotsOverrideColor` |
| **Override Background: Enabled** (pestaña Display) | Activa el color de fondo personalizado del spot. Predeterminado: Activado. | `IsSpotsOverrideBackgroundColorsEnabled` |
| **Override Background: Auto** (pestaña Display) | Selecciona automáticamente el color de fondo para el contraste. Predeterminado: Activado. | `IsSpotsOverrideToAutoBackgroundColorEnabled` |
| **Selector de color de fondo del spot** (pestaña Display) | Abre QColorDialog para el color de fondo del spot. Predeterminado: #000000. | `SpotsOverrideBgColor` |
| **Background Opacity:** (pestaña Display) | Opacidad del color de fondo del spot (0–100). Predeterminado: 48. | `SpotsBackgroundOpacity` |
| **Spot Lines:** (pestaña Display) | Dibuja líneas verticales desde el espectro hasta cada etiqueta de spot. Desactívelo durante concursos para reducir el desorden visual. Predeterminado: Activado. Nuevo en v0.9.7 (#2349). | `IsSpotsLinesEnabled` |
| **Total Spots:** (pestaña Display) | Conteo en vivo de spots actualmente rastreados en todas las fuentes. | — |
| **DXCC Coloring (section)** (pestaña Display) | Encabezado de sección para los controles de coloración DXCC en la columna izquierda debajo del divisor. | — |
| **DXCC Colors:** (pestaña Display) | Colorea los spots según el estado DXCC trabajado/confirmado/necesario. La clave de configuración cambió de `DxccColoringEnabled` a `IsDxccColoringEnabled` en v26.5.1. | `IsDxccColoringEnabled` |
| **Log File (ADIF):** (pestaña Display) | Carga un archivo de registro ADIF para impulsar la coloración DXCC. Vigila automáticamente el archivo en busca de cambios después de la selección. La clave de configuración cambió de `DxccAdifPath` a `DxccAdifFilePath` en v26.5.1. | `DxccAdifFilePath` |
| **Imported: (estadísticas DXCC)** (pestaña Display) | Muestra el recuento de QSO y el recuento de entidades cuando se carga un registro. Formato: '<N> QSOs / <M> entities'. | — |
| **Muestras de color DXCC (New DXCC / New Band / New Mode / Worked)** (pestaña Display) | Abre un selector de color para cada categoría de estado DXCC. Nuevo en v26.5.1 — reemplaza el esquema de color DXCC fijo anterior. | `DxccColorNewEntity`, `DxccColorNewBand`, `DxccColorNewMode`, `DxccColorWorked` |
| **Signal History (section)** (pestaña Display) | Encabezado de sección para los parámetros ajustables de Signal History en la columna derecha debajo del divisor. Nuevo en v26.5.1 (#2506). | — |
| **Marker Lifetime:** (pestaña Display) | Cuánto tiempo persiste un marcador de Signal History inactivo antes de ser eliminado (15–300 s). Predeterminado: 60 s. Nuevo en v26.5.1. | `SHistoryLifetimeS` |
| **QRM Gate:** (pestaña Display) | Cuánto tiempo debe persistir una portadora estrecha o señal de banda ancha antes de ser clasificada como QRM (3–30 s). Predeterminado: 6 s. Nuevo en v26.5.1. | `SHistoryQrmGateS` |
| **Edge Threshold:** (pestaña Display) | Umbral por encima del piso de ruido para la caminata de borde de pendiente que refina el borde lateral de la portadora de S-History (1.0–10.0 dB). Predeterminado: 3.0 dB. Nuevo en v26.5.1. | `SHistorySoftEdgeDb` |
| **Muestras de color de Signal History (Signals / QRM)** (pestaña Display) | Abre un selector de color para los marcadores de señales de voz (dorado) y QRM (rojo). Nuevo en v26.5.1. | `SHistoryColorSignals`, `SHistoryColorQrm` |
| **Snap to Step:** (pestaña Display) | Redondea el clic-para-sintonizar de S-History al múltiplo más cercano del tamaño de paso del slice activo, ocultando el pequeño desplazamiento de portadora. Predeterminado: Desactivado. Nuevo en v26.5.1. | `SHistorySnapToStep` |

## Sintonizar un spot haciendo doble clic

Al hacer doble clic en una fila de la pestaña **Spot List** se sintoniza el slice activo a la frecuencia del spot. A partir de v0.9.7, AetherSDR también reenvía la información de modo extraída del comentario del spot, por lo que el slice cambia al modo apropiado (por ejemplo, CW o SSB) para coincidir con el spot, en lugar de solo cambiar la frecuencia.

## Reportes de FreeDV Reporter

El grupo **Station Reporting** en la pestaña **FreeDV** permite que AetherSDR transmita la actividad de su estación al mapa público FreeDV Reporter en qso.freedv.org mientras el módem RADE esté activo.

### Requisitos

- La pestaña FreeDV y todos los controles de reporte solo están presentes en compilaciones compiladas con `HAVE_WEBSOCKETS`. En Windows, la casilla de verificación **Enable FreeDV Reporter reporting when RADE is active** requiere adicionalmente `HAVE_RADE`.
- Tanto un indicativo como un cuadrado de cuadrícula deben ser resolubles antes de que se pueda habilitar el reporte. Si alguno está en blanco cuando marca **Enable FreeDV Reporter reporting when RADE is active**, AetherSDR muestra un cuadro de diálogo de advertencia y deja la casilla sin marcar.

### Configuración de los reportes

1. Abra `Settings > SpotHub...` y haga clic en la pestaña **FreeDV**.
2. En el grupo **Station Reporting**, confirme o ingrese su indicativo:
   - Si **Use radio** está marcado (predeterminado), el campo **Callsign:** se completa automáticamente desde el indicativo configurado de la radio y es de solo lectura. Desmarque **Use radio** para escribir un indicativo diferente.
3. Confirme o ingrese su cuadrado de cuadrícula:
   - Si **Use GPS** está marcado (predeterminado, solo radios con capacidad GPS), el campo **Grid Square:** se completa desde el GPS de la radio y es de solo lectura. Desmarque **Use GPS** para escribir un cuadrado de cuadrícula manualmente.
4. Opcionalmente, ingrese un mensaje corto en **Station Msg:** para que aparezca junto a su indicativo en el mapa.
5. Marque **Enable FreeDV Reporter reporting when RADE is active**.
   - Si tanto el indicativo como el cuadrado de cuadrícula están presentes, el reporte se habilita y se guarda en `FreeDvAutoReport`.
   - Si falta alguno, aparece un cuadro de diálogo de advertencia y la casilla permanece sin marcar. Complete el campo faltante e intente nuevamente.

### Controles de reporte

| Control | Descripción | Clave de configuración |
|---|---|---|
| **Enable FreeDV Reporter reporting when RADE is active** | Interruptor principal para el reporte en el mapa público. Bloqueado si el indicativo o el cuadrado de cuadrícula están en blanco. | `FreeDvAutoReport` |
| **Callsign:** | Indicativo enviado al mapa de FreeDV Reporter. | `FreeDvMyCallsign` |
| **Use radio** | Copia el indicativo de la radio y bloquea el campo como solo lectura. | `FreeDvUseRadioCallsign` |
| **Grid Square:** | Localizador Maidenhead enviado al mapa de FreeDV Reporter. | `FreeDvMyGrid` |
| **Use GPS** | Copia la cuadrícula del GPS de la radio y bloquea el campo como solo lectura. Visible solo en modelos de radio con capacidad GPS. | `FreeDvUseGpsGrid` |
| **Station Msg:** | Línea de estado opcional de texto libre mostrada en el mapa público. | `FreeDvMyMessage` |

## Pestaña Display: Cambio del modo automático predeterminado

A partir de v0.9.5.1, la activación **Auto:** en la pestaña **Display** tiene como predeterminado **Activado**. En versiones anteriores, el predeterminado era **Desactivado**. `SpotAutoSwitchMode` se guarda como `True` a menos que lo haya configurado previamente de otra manera. Si prefería el comportamiento anterior, abra la pestaña **Display** y desactive **Auto:**.

## Pestaña Display: Líneas de Spot (nuevo en v0.9.7)

La activación **Spot Lines:** en la pestaña **Display** controla si AetherSDR dibuja una línea vertical desde la línea base del espectro hasta cada etiqueta de spot en el panadaptador. La activación tiene como predeterminado **Activado** y se guarda en `IsSpotsLinesEnabled`.

Desactive **Spot Lines:** durante concursos o cuando el panadaptador esté muy poblado de spots para reducir el desorden visual.

## Pestaña Display: Historial de Señales (nuevo en v26.5.1)

La pestaña **Display** ahora incluye una sección **Signal History (section)** en la columna derecha debajo del divisor. Esta sección consolida todos los parámetros ajustables de Signal History:

- Las activaciones **Signals (Signal History)** y **QRM (Signal History)** controlan la visibilidad de los marcadores dorados y rojos.
- El deslizador **Marker Lifetime:** controla cuánto tiempo persisten los marcadores inactivos (15–300 segundos).
- El deslizador **QRM Gate:** establece cuánto tiempo debe persistir una señal antes de ser clasificada como QRM (3–30 segundos).
- El deslizador **Edge Threshold:** establece el umbral en dB para el refinamiento del borde (1.0–10.0 dB).
- La activación **Snap to Step:** redondea el clic-para-sintonizar al tamaño de paso más cercano.
- Las muestras de color le permiten elegir colores personalizados para los marcadores de señales (dorado) y QRM (rojo).

## Pestaña Display: Coloración DXCC (actualizado en v26.5.1)

La pestaña **Display** ahora incluye una sección **DXCC Coloring (section)** en la columna izquierda debajo del divisor. Esta sección reemplaza el esquema de color DXCC fijo anterior con muestras de color personalizables para cada categoría de estado DXCC: New DXCC, New Band, New Mode y Worked.

La activación de coloración DXCC y las claves de configuración del archivo de registro (AD
