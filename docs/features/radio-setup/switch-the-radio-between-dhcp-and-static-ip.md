# Cambiar la Radio Entre DHCP e IP Estática

Use esta página para cambiar cómo el FLEX-8600 obtiene su dirección de red — automáticamente a través de DHCP o con una IP estática, máscara de subred y puerta de enlace que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión activa a la radio.
- Si está cambiando a IP estática, tenga listos la dirección IP, la máscara de subred y los valores de puerta de enlace antes de comenzar.
- Cambiar la configuración de red hará que la radio se mueva a una nueva dirección. Deberá reconectarse después de aplicar los cambios.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Anote la **IP Address**, **Mask** y **MAC Address** actuales que se muestran como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar modos. El botón refleja el modo actual; hacer clic en él cambia al otro.
5. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:** con los valores de su red.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Reconéctese a la radio en su nueva dirección usando `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestra las direcciones de red actuales de la radio. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática a asignar a la radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo estático. |
| **Apply** | Botón de empuje | Envía la configuración de red a la radio. |
| **TX Follows Active Slice** | Botón de empuje | La transmisión sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. |
| **Active Slice Follows TX** | Botón de empuje | Cambia el slice activo cuando la transmisión se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Voice / CW / Digital filter sharpness sliders** | Deslizadores (0–3) | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón de empuje | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de interlock de hardware; no se necesita teclado en el lado del cliente. Si el campo de IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se pre-rellena. |
| **Connect / Disconnect (PGXL)** | Botón de empuje | Abre/cierra la conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón de empuje | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (no un Antenna Genius estándar) es el dispositivo conectado. |
| **Connect / Disconnect (ShackSwitch)** | Botón de empuje | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento a través de UDP también funciona sin esta fila. La fila se oculta del estado Connected si un Antenna Genius estándar (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Botón de empuje | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, retrocede a `SS_WebPort` o puerto 5000. |
| **Select Installer...** | Botón de empuje | Abre un selector de archivos que acepta instalador WiX de FlexRadio v4.2+ (`.msi`), instalador de extracción automática más antiguo (`.exe`) o archivo de firmware pre-extraído (`.ssdr`). El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | Pestaña | Configuración del muestreo externo de Pre-Distorsión Adaptativa — selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Cuadro combinado | Selecciona la ruta de realimentación que la radio utiliza para muestrear el RF saliente para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando esté accionando un amplificador lineal externo. Las opciones se completan dinámicamente desde el sub-objeto `apd sampler` de la radio. Se revierte a INTERNAL si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón de empuje | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| **Themes (tab)** | Pestaña | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de radio | Cambia el esquema de color de slice entre la paleta AetherSDR integrada y un conjunto totalmente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Slice A–H color buttons** | Botones de empuje | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter e insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón de empuje | Restablece todos los colores de slice personalizados a la paleta AetherSDR integrada. |

## Actualización de firmware (Pestaña Radio)

La pestaña **Radio** incluye controles para verificar actualizaciones de firmware y preparar un archivo de firmware para carga.

### Cómo actualizar firmware en v0.9.3

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualización de FlexRadio. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e instruye que descargue el instalador SmartSDR desde flexradio.com.
2. Descargue el instalador SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones más antiguas).
3. Haga clic en **Select Installer...** para abrir el selector de archivos. Seleccione el instalador que descargó o un archivo `.ssdr` pre-extraído si ya tiene uno. El preparador detecta automáticamente el formato de archivo y extrae el firmware sin herramientas externas. La etiqueta de estado se actualiza para mostrar el progreso de la preparación.
4. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y etiqueta de estado rastrean la carga.

> **Nota:** En v0.9.3 el botón anteriormente etiquetado como **Browse .ssdr...** fue renombrado a **Select Installer...** y el selector de archivos ahora acepta archivos `.msi`, `.exe` y `.ssdr`. El botón **Check for Update** ya no cambia a un botón de descarga cuando se encuentra una actualización; descargue el instalador manualmente desde flexradio.com y prépárelo localmente.

### Controles de la pestaña Firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador (solo lectura) | Número de serie del chasis. |
| **Model** | Indicador (solo lectura) | Modelo de radio. |
| **HW Version** | Indicador (solo lectura) | Cadena de versión de hardware. |
| **Region** | Indicador (solo lectura) | Región reguladora de la radio. |
| **Options** | Indicador (solo lectura) | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Indicador (solo lectura) | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador (solo lectura) | Estado habilitado de multiFLEX. |
| **Nickname** | Campo de texto | Nombre amigable de la radio. |
| **Callsign** | Campo de texto | Indicativo de estación. |
| **Station Name** | Campo de texto (`StationName`) | Identifica este cliente AetherSDR a otras estaciones multiFLEX. Por defecto es el nombre de host del SO si se deja vacío. Se envía a la radio como `client station <name>`. |
| **License Info** | Indicador (solo lectura) | Muestra suscripción, caducidad, Radio ID y versión licenciada desde la radio. |
| **Remote On** | Botón de empuje | Habilita el despertar remoto / encendido remoto. |
| **Check for Update** | Botón de empuje | Consulta el servidor de actualización de FlexRadio para firmware disponible. Si hay una actualización disponible, la etiqueta de estado muestra la versión y dirige a descargar el instalador manualmente. |
| **Select Installer...** | Botón de empuje | Abre un selector de archivos que acepta archivos `.msi`, `.exe` o `.ssdr`. El preparador detecta automáticamente el formato y extrae el firmware. |
| **Upload Firmware** | Botón de empuje | Inicia la carga del firmware a la radio con una barra de progreso y etiqueta de estado. |

## Calibración de frecuencia (Pestaña RX)

La pestaña **RX** proporciona calibración manual de offset de frecuencia y selección de fuente de referencia de 10 MHz. En v0.9.2.1 los controles de calibración se muestran siempre independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica el estado del GPSDO:

- **GPSDO installed** — etiqueta mostrada en verde: *GPSDO installed. Manual frequency offset calibration available.*
- **No GPSDO** — etiqueta mostrada en ámbar: *Manual frequency offset calibration available.*

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox / campo de texto | Frecuencia utilizada para calibración. No debe estar vacía antes de comenzar. |
| **Start** | Botón de empuje | Inicia la secuencia de calibración de frecuencia. Establece `cal_freq`, restablece `freq_error_ppb` a 0, luego dispara la calibración PLL de la radio. El botón se deshabilita y muestra **Busy** mientras se ejecuta la calibración. Una etiqueta de estado junto al botón reporta progreso (Starting… / running / result). |
| **Freq Offset (ppb):** | Spinbox | Offset de frecuencia manual en partes por billón. Se establece en 0 automáticamente al inicio de una ejecución de calibración. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona fuente de referencia de oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo en vivo (Locked / Unlocked) se muestra junto al cuadro combinado. |

### Cómo funciona la calibración en v0.9.2.1

1. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**. Para obtener los mejores resultados, use una estación de emisión estable conocida (por ejemplo, una estación de onda corta de referencia) o un generador
