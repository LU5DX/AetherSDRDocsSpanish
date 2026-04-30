# Cambiar la radio entre DHCP e IP estática

Use esta página para cambiar cómo la FLEX-8600 obtiene su dirección de red — automáticamente vía DHCP o con una IP estática fija, máscara de subred y puerta de enlace que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión activa a la radio.
- Si está cambiando a IP estática, tenga listos la dirección IP, la máscara de subred y los valores de puerta de enlace antes de comenzar.
- Cambiar la configuración de red hará que la radio se mueva a una nueva dirección. Deberá reconectarse después de aplicar.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Observe la **IP Address**, **Mask** y **MAC Address** actuales que se muestran como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo. El botón refleja el modo actual; al hacer clic se cambia al otro.
5. Si seleccionó modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:** con los valores de su red.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Reconéctese a la radio en su nueva dirección usando `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestra las direcciones de red actuales de la radio. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática a asignar a la radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo estático. |
| **Apply** | Botón de presión | Envía la configuración de red a la radio. |
| **TX Follows Active Slice** | Botón de presión | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. |
| **Active Slice Follows TX** | Botón de presión | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Voice / CW / Digital filter sharpness sliders** | Deslizadores (0–3) | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón de presión | Abre/cierra conexión TCP directa a la TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente a la TGXL en lugar de la ruta del lado de la radio que se rompió en firmware 4.2. La TGXL controla PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita manipulación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto la TGXL, la IP descubierta se completa previamente. |
| **Connect / Disconnect (PGXL)** | Botón de presión | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón de presión | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |
| **Select Installer...** | Botón de presión | Abre un selector de archivos que acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | Pestaña | Configuración del muestreador de Pre-Distorsión Adaptativa externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; la serie 6000 y radios pre-4.2.18 mantienen la pestaña invisible. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando controle un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón de presión | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (tab)** | Pestaña | Pestaña de personalización de interfaz — actualmente alberga la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de radio | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Slice A–H color buttons** | Botones de presión | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter e insignias de canal CAT. Los botones se deshabilitan cuando está seleccionado **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón de presión | Reinicia todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles para verificar actualizaciones de firmware y preparar un archivo de firmware para carga.

### Cómo actualizar firmware en v0.9.3

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualización de FlexRadio. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e instruye descargar el instalador SmartSDR desde flexradio.com.
2. Descargue el instalador SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones más antiguas).
3. Haga clic en **Select Installer...** para abrir el selector de archivos. Seleccione el instalador que descargó o un archivo `.ssdr` preextraído si ya tiene uno. El preparador detecta el formato de archivo automáticamente y extrae el firmware sin herramientas externas. La etiqueta de estado se actualiza para mostrar el progreso de preparación.
4. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y etiqueta de estado rastrean la carga.

> **Nota:** En v0.9.3 el botón anteriormente etiquetado **Browse .ssdr...** fue renombrado a **Select Installer...** y el selector de archivos ahora acepta archivos `.msi`, `.exe` y `.ssdr`. El botón **Check for Update** ya no cambia a un botón de descarga cuando se encuentra una actualización; descarga el instalador manualmente desde flexradio.com y lo prepara localmente.

### Controles de la pestaña Firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador (solo lectura) | Número de serie del chasis. |
| **Model** | Indicador (solo lectura) | Modelo de radio. |
| **HW Version** | Indicador (solo lectura) | Cadena de versión de hardware. |
| **Region** | Indicador (solo lectura) | Región regulatoria de la radio. |
| **Options** | Indicador (solo lectura) | Muestra opciones de radio licenciadas. |
| **FlexControl** | Indicador (solo lectura) | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador (solo lectura) | Estado habilitado de multiFLEX. |
| **Nickname** | Campo de texto | Apodo amigable de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto (`StationName`) | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Por defecto el nombre de host del SO si se deja vacío. Enviado a la radio como `client station <name>`. |
| **License Info** | Indicador (solo lectura) | Muestra suscripción, vencimiento, ID de radio y versión licenciada de la radio. |
| **Remote On** | Botón de presión | Habilita activación remota / remote-on. |
| **Check for Update** | Botón de presión | Consulta el servidor de actualización de FlexRadio para firmware disponible. Si hay una actualización disponible, la etiqueta de estado muestra la versión y dirige a descargar el instalador manualmente. |
| **Select Installer...** | Botón de presión | Abre un selector de archivos que acepta archivos `.msi`, `.exe` o `.ssdr`. El preparador detecta automáticamente el formato y extrae el firmware. |
| **Upload Firmware** | Botón de presión | Inicia la carga de firmware a la radio con barra de progreso y etiqueta de estado. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz. En v0.9.2.1 los controles de calibración siempre se muestran independientemente de si está instalado un GPSDO. Una etiqueta de estado en la parte superior del grupo indica el estado del GPSDO:

- **GPSDO installed** — etiqueta mostrada en verde: *GPSDO installed. Manual frequency offset calibration available.*
- **No GPSDO** — etiqueta mostrada en ámbar: *Manual frequency offset calibration available.*

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de número / campo de texto | Frecuencia usada para calibración. No debe estar vacío antes de comenzar. |
| **Start** | Botón de presión | Inicia la secuencia de calibración de frecuencia. Establece `cal_freq`, reinicia `freq_error_ppb` a 0, luego dispara la calibración PLL de la radio. El botón se deshabilita y muestra **Busy** mientras la calibración se está ejecutando. Una etiqueta de estado junto al botón reporta progreso (Starting… / running / result). |
| **Freq Offset (ppb):** | Cuadro de número | Desplazamiento manual de frecuencia en partes por mil millones. Se establece automáticamente a 0 al inicio de una ejecución de calibración. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona fuente de referencia de oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo en vivo (Locked / Unlocked) se muestra junto al cuadro combinado. |

### Cómo funciona la calibración en v0.9.2.1

1. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
2. Haga clic en **Start**. AetherSDR envía `radio set cal_freq=<value>` y `radio set freq_error_ppb=0` a la radio, luego emite `radio pll_start` para comenzar el barrido.
3. El botón **Start** se deshabilita y se etiqueta **Busy** hasta que la secuencia se completa o falla.
4. La etiqueta de estado junto al botón se actualiza en tiempo real. Cuando la calibración finaliza el botón se vuelve a habilitar y la etiqueta muestra el resultado.

Si el campo **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra *Enter cal frequency* en ámbar y la calibración no comienza.

> **Nota:** Antes de v0.9.2.1, los controles de calibración se ocultaban cuando se detectaba un GPSDO. Ahora siempre están disponibles.

## Consejos

- Los indicadores **IP Address / Mask / MAC Address** muestran lo que la radio está usando actualmente. Anote
