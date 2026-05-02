# Cambiar la radio entre DHCP e IP estática

Use esta página para cambiar la forma en que el FLEX-8600 obtiene su dirección de red: automáticamente mediante DHCP o con una IP estática fija, máscara de subred y puerta de enlace que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión de radio activa.
- Si va a cambiar a IP estática, tenga listos los valores de dirección IP, máscara de subred y puerta de enlace antes de comenzar.
- Cambiar la configuración de red hará que la radio se mueva a una nueva dirección. Deberá reconectarse después de aplicar los cambios.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el cuadro de diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Tome nota de la **IP Address**, **Mask** y **MAC Address** actuales que se muestran como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo. El botón refleja el modo actual; al hacer clic cambia al otro.
5. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:** con los valores correspondientes a su red.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Reconéctese a la radio en su nueva dirección usando `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestra las direcciones de red actuales de la radio. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática que se asignará a la radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo estático. |
| **Apply** | Botón de acción | Envía la configuración de red a la radio. |
| **TX Follows Active Slice** | Botón de acción | TX sigue al slice (canal) activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón de acción | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. |
| **Sliders de nitidez de filtro Voice / CW / Digital** | Controles deslizantes (0–3) | Establece la nitidez del filtro (0 = menor latencia hasta 3 = máxima nitidez) por modo. El control se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón de acción | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE con el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que quedó interrumpida en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de enclavamiento hardware; no se requiere activación desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Botón de acción | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón de acción | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si el dispositivo conectado es un ShackSwitch (no un Antenna Genius estándar). |
| **Connect / Disconnect (ShackSwitch)** | Botón de acción | Abre o cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius estándar (no ShackSwitch). |
| **⚙ Web UI (ShackSwitch)** | Botón de acción | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón de acción | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic frente a PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta fue renombrada desde **Browse .ssdr...** en la versión v0.9.3. |
| **APD (pestaña)** | Pestaña | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Cuadro combinado | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente en el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando use un amplificador lineal externo. Las opciones se obtienen en tiempo real del subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón de acción | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| **Themes (pestaña)** | Pestaña | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Botones de color de Slice A–H** | Botones de acción | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón de acción | Restablece todos los colores personalizados de slice a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles para buscar actualizaciones de firmware y preparar un archivo de firmware para la carga.

### Cómo actualizar el firmware en la versión v0.9.3

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** para abrir el selector de archivos. Seleccione el instalador descargado o un archivo `.ssdr` ya extraído si ya dispone de uno. El preparador detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. La etiqueta de estado se actualiza para mostrar el progreso de la preparación.
4. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y una etiqueta de estado registran la carga.

> **Nota:** En la versión v0.9.3, el botón que antes se llamaba **Browse .ssdr...** pasó a llamarse **Select Installer...** y el selector de archivos ahora acepta archivos `.msi`, `.exe` y `.ssdr`. El botón **Check for Update** ya no cambia a un botón de descarga cuando se encuentra una actualización; usted descarga el instalador manualmente desde flexradio.com y lo prepara localmente.

### Controles de la pestaña de firmware

| Control | Tipo | Comportamiento |
|---|---|---|
| **Radio SN** | Indicador (solo lectura) | Número de serie del chasis. |
| **Model** | Indicador (solo lectura) | Modelo de la radio. |
| **HW Version** | Indicador (solo lectura) | Cadena de versión de hardware. |
| **Region** | Indicador (solo lectura) | Región regulatoria de la radio. |
| **Options** | Indicador (solo lectura) | Muestra las opciones de radio con licencia. |
| **FlexControl** | Indicador (solo lectura) | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador (solo lectura) | Estado habilitado de multiFLEX. |
| **Nickname** | Campo de texto | Nombre descriptivo de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto (`StationName`) | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre de host del sistema operativo de forma predeterminada si se deja vacío. Se envía a la radio como `client station <name>`. |
| **License Info** | Indicador (solo lectura) | Muestra la suscripción, la fecha de vencimiento, el ID de radio y la versión con licencia provenientes de la radio. |
| **Remote On** | Botón de acción | Habilita el encendido remoto. |
| **Check for Update** | Botón de acción | Consulta el servidor de actualizaciones de FlexRadio para ver si hay firmware disponible. Si hay una actualización disponible, la etiqueta de estado muestra la versión y le indica que descargue el instalador manualmente. |
| **Select Installer...** | Botón de acción | Abre un selector de archivos que acepta archivos `.msi`, `.exe` o `.ssdr`. El preparador detecta el formato automáticamente y extrae el firmware. |
| **Upload Firmware** | Botón de acción | Inicia la carga del firmware a la radio con una barra de progreso y una etiqueta de estado. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** ofrece calibración manual de desplazamiento de frecuencia y selección de la fuente de referencia de 10 MHz. En la versión v0.9.2.1, los controles de calibración se muestran siempre, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica el estado del GPSDO:

- **GPSDO instalado** — etiqueta mostrada en verde: *GPSDO installed. Manual frequency offset calibration available.*
- **Sin GPSDO** — etiqueta mostrada en ámbar: *Manual frequency offset calibration available.*

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox / campo de texto | Frecuencia usada para la calibración. No debe estar vacío antes de iniciar. |
| **Start** | Botón de acción | Inicia la secuencia de calibración de frecuencia. Establece `cal_freq`, reinicia `freq_error_ppb` a 0 y luego activa la calibración PLL de la radio. El botón se deshabilita y muestra **Busy** mientras la calibración está en curso. Una etiqueta de estado junto al botón informa el progreso (Starting… / running / result). |
| **Freq Offset (ppb):** | Spinbox | Desplazamiento de frecuencia manual en partes por billón. Se establece automáticamente en 0 al inicio de una ejecución de calibración. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo en tiempo real (Locked / Unlocked) se muestra junto al cuadro combinado. |

### Cómo funciona la calibración en la versión v0.
