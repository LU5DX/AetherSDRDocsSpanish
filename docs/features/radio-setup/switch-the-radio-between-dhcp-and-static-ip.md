# Cambiar la Radio Entre DHCP e IP Estática

Use esta página para cambiar cómo la FLEX-8600 obtiene su dirección de red, ya sea automáticamente mediante DHCP o con una IP estática, máscara de subred y puerta de enlace fijas que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión activa con la radio.
- Si va a cambiar a IP estática, tenga preparados los valores de dirección IP, máscara de subred y puerta de enlace antes de empezar.
- Cambiar la configuración de red hará que la radio se mueva a una nueva dirección. Necesitará reconectarse después de aplicar los cambios.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Observe la **IP Address**, **Mask** y **MAC Address** actuales mostradas como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo. El botón refleja el modo actual; al hacer clic, cambia al otro.
5. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:** con los valores de su red.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Reconéctese a la radio en su nueva dirección usando `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestra las direcciones de red actuales de la radio. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática para asignar a la radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo estático. |
| **Apply** | Botón pulsador | Envía la configuración de red a la radio. |
| **TX Follows Active Slice** | Botón pulsador | TX sigue la franja activa. Es mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón pulsador | Cambia la franja activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. |
| **Controles deslizantes de nitidez de filtro Voz / CW / Digital** | Controles deslizantes (0–3) | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El control deslizante se desactiva cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voz / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; desactiva el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón pulsador | Abre/cierra conexión TCP directa con el TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL controla PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita activación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón pulsador | Abre/cierra conexión TCP directa con el Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón pulsador | Abre/cierra conexión con el Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (no un Antenna Genius estándar) es el dispositivo conectado. |
| **Connect / Disconnect (ShackSwitch)** | Botón pulsador | Abre/cierra conexión con un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El descubrimiento automático mediante UDP también funciona sin esta fila. La fila se oculta del estado Conectado si un Antenna Genius estándar (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón pulsador | Abre un selector de archivos que acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de preparación detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (pestaña)** | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa: selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Combo de muestreadores ANT1 / ANT2 / XVTA / XVTB (APD)** | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio usa para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón pulsador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (pestaña)** | Pestaña | Pestaña de personalización de la interfaz de usuario: actualmente alberga la sección de Colores de Franja. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de colores de la franja entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por franja. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Botones de color de franja A–H** | Botones pulsadores | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa franja. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones se desactivan cuando se selecciona **Use Aether defaults**. Hasta 8 franjas. |
| **Reset All to Defaults (Themes)** | Botón pulsador | Restablece todos los colores personalizados de franja a la paleta incorporada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles para buscar actualizaciones de firmware y preparar un archivo de firmware para su carga.

### Cómo actualizar el firmware en v0.9.3

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** para abrir el selector de archivos. Seleccione el instalador que descargó, o un archivo `.ssdr` preextraído si ya tiene uno. El gestor de preparación detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. La etiqueta de estado se actualiza para mostrar el progreso de la preparación.
4. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y una etiqueta de estado rastrean la carga.

> **Nota:** En v0.9.3, el botón antes etiquetado como **Browse .ssdr...** se renombró a **Select Installer...** y el selector de archivos ahora acepta archivos `.msi`, `.exe` y `.ssdr`. El botón **Check for Update** ya no cambia a un botón de descarga cuando se encuentra una actualización; usted descarga el instalador manualmente desde flexradio.com y lo prepara localmente.

### Controles de la pestaña Firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador (solo lectura) | Número de serie del chasis. |
| **Model** | Indicador (solo lectura) | Modelo de la radio. |
| **HW Version** | Indicador (solo lectura) | Cadena de versión de hardware. |
| **Region** | Indicador (solo lectura) | Región regulatoria de la radio. |
| **Options** | Indicador (solo lectura) | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Indicador (solo lectura) | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador (solo lectura) | Estado habilitado de multiFLEX. |
| **Nickname** | Campo de texto | Apodo de la radio fácil de usar. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto (`StationName`) | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto, es el nombre de host del SO si se deja vacío. Se envía a la radio como `client station <nombre>`. |
| **License Info** | Indicador (solo lectura) | Muestra suscripción, vencimiento, ID de radio y versión licenciada de la radio. |
| **Remote On** | Botón pulsador | Habilita el encendido remoto/activación remota. |
| **Check for Update** | Botón pulsador | Consulta el servidor de actualizaciones de FlexRadio en busca de firmware disponible. Si hay una actualización disponible, la etiqueta de estado muestra la versión y le indica que descargue el instalador manualmente. |
| **Select Installer...** | Botón pulsador | Abre un selector de archivos que acepta archivos `.msi`, `.exe` o `.ssdr`. El gestor de preparación detecta automáticamente el formato y extrae el firmware. |
| **Upload Firmware** | Botón pulsador | Inicia la carga del firmware a la radio con una barra de progreso y una etiqueta de estado. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de compensación de frecuencia y selección de la fuente de referencia de 10 MHz. En v0.9.2.1, los controles de calibración se muestran siempre, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica el estado del GPSDO:

- **GPSDO instalado** — etiqueta mostrada en verde: *GPSDO installed. Manual frequency offset calibration available.*
- **Sin GPSDO** — etiqueta mostrada en ámbar: *Manual frequency offset calibration available.*

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox / campo de texto | Frecuencia utilizada para la calibración. No debe estar vacía antes de comenzar. |
| **Start** | Botón pulsador | Inicia la secuencia de calibración de frecuencia. Establece `cal_freq`, restablece `freq_error_ppb` a 0 y luego activa la calibración PLL de la radio. El botón se desactiva y muestra **Busy** mientras la calibración está en ejecución. Una etiqueta de estado al lado del botón informa el progreso (Starting… / running / result). |
| **Freq Offset (ppb):** | Spinbox | Compensación de frecuencia manual en partes por mil millones. Se establece automáticamente a 0 al inicio de una ejecución de calibración. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador. El cuadro combinado se completa dinámicamente según el hardware presente y la configuración y estado del oscilador informados por la radio. Las opciones disponibles son: **Auto**, **TCXO** (se muestra cuando el hardware está presente o la radio está usando actualmente TCXO), **GPSDO** (se muestra cuando hay un GPSDO)
