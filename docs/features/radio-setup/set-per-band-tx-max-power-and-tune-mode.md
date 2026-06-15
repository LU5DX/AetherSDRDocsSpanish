# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Organiza la identificación de la radio, red, GPS, transmisión, teléfono/CW, recepción, nombres de antenas, filtros, transvertidores, cables USB, periféricos, APD, temas, gestión de certificados SmartLink y configuraciones de puerto serie en varias pestañas.

## Abrir la Configuración de la Radio

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como un diálogo persistente; su geometría se guarda y restaura automáticamente entre sesiones.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de la radio

| Control | Tipo | Notas |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). Haga clic en el icono de copiar junto al valor para copiarlo al portapapeles. |
| **Region** | Indicador | Región normativa de la radio. |
| **HW Version** | Indicador | Cadena de versión de hardware. |
| **Model** | Indicador | Modelo de la radio. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. Haga clic en el icono de copiar para copiar el texto. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de habilitación de multiFLEX. |

### Identificación

| Control | Tipo | Notas |
|---|---|---|
| **Nickname** | Campo de texto | Apodo amigable de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. Haga clic en el icono de copiar junto al valor para copiarlo al portapapeles. |
| **Station Name** | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Usa el nombre del host del SO si está vacío. Almacenado en AppSettings. Enviado a la radio como 'client station <nombre>'. |

### Copiar valores de solo lectura

Cada campo de información de solo lectura en esta pestaña (Radio SN, Callsign, Options, HW Version, Region, Model, IP Address, Mask, MAC Address y campos de información de licencia) muestra un pequeño icono de copiar al pasar el cursor sobre el valor. Haga clic en el icono para copiar el texto al portapapeles. Una breve ventana emergente "Copied" confirma la acción.

### Información de licencia

El diálogo muestra los detalles de licencia de la radio, incluidos el estado de suscripción, fecha de vencimiento, ID de la radio y versión licenciada. Cada campo incluye un botón de copia al portapapeles junto al valor.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar si hay actualizaciones de firmware.
   - Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
2. Descargue el instalador de SmartSDR desde flexradio.com si hay uno disponible.
3. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo `.ssdr` preextraído.
   - El preparador de firmware detecta el formato del archivo automáticamente y extrae el `.ssdr` sin necesidad de herramientas externas.
   - Mientras el preparador prepara el firmware, se muestra la barra de progreso y la etiqueta de estado indica "Preparing firmware from \<nombrearchivo\>...".
4. Una vez completada la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio. El progreso y el resultado se muestran en la etiqueta de estado.

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta si hay actualizaciones de firmware disponibles. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. Anteriormente etiquetado como **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Botón | Inicia la carga del firmware. La barra de progreso y la etiqueta de estado se actualizan durante el proceso. |

### Encendido Remoto

Haga clic en **Remote On** para habilitar la capacidad de activación/encendido remoto.

### Reiniciar Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada.

| Control | Tipo | Notas |
|---|---|---|
| **Reboot Radio** | Botón | Reinicia la radio. Se muestra un diálogo de confirmación antes de reiniciar. El botón se deshabilita cuando la radio no está conectada. Para conexiones LAN, AetherSDR se reconecta automáticamente después de que la radio termina de iniciar. Para conexiones SmartLink/WAN, debe reconectarse manualmente. El diálogo se cierra después de iniciar el reinicio. |

1. Haga clic en **Reboot Radio**.
2. Un diálogo de confirmación explica la diferencia de comportamiento entre conexiones LAN y WAN.
3. Haga clic en **OK** para confirmar. AetherSDR envía el comando de reinicio a la radio y cierra el diálogo de configuración.

## Pestaña Network

La pestaña Network muestra la información de red de la radio y proporciona opciones de red avanzadas.

### Información de red

| Control | Tipo | Notas |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |

### Configuración de red

| Control | Tipo | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | Habilitado | — | Rechaza pares no RFC1918. El botón siempre muestra "Enabled" cuando está marcado. |
| **Network MTU:** | Spin box | 1450 | 576–9000 bytes | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Almacenado en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | — | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | — | — | Campos de configuración de IP estática. |

### Aplicar configuración de red

Haga clic en **Apply** para enviar la configuración de red a la radio.

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS y la información en vivo de latitud, longitud, altitud, hora y satélites.

## Pestaña TX

Use esta página para configurar los ajustes de transmisión, incluyendo temporizaciones, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall y el comportamiento de seguimiento de slice/TX.

### Configuración de banda TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y sintonía por banda.

### Controles TX

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Max Power:** | Spin box | — | Establece el límite de potencia TX a nivel de radio (0–100%). |
| **Tune Mode:** | Combo box | — | Selecciona cómo se comporta el botón de sintonía. |
| **Timings** | Spin box / Campo de texto | — | Temporizaciones de espera/retardo de TX. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y Accessory. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en el waterfall. |
| **TX Follows Active Slice** | Botón | Falso | TX sigue la slice activa. Es mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Falso | Cambia la slice activa cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con 'TX Follows Active Slice'. |

### Campos de temporización TX

| Campo | Etiqueta mostrada | Unidad reportada | Sufijo del comando |
|---|---|---|---|
| ACC TX | ACC TX | ms | `acc_tx_delay` |
| TX Delay | TX Delay | ms | `tx_delay` |
| RCA TX1 | RCA TX1 | ms | `tx1_delay` |
| Timeout (sec) | Timeout (sec) | segundos | `interlock_timeout` (valor multiplicado por 1000 antes de enviar a la radio) |

El campo de tiempo de espera de enclavamiento se muestra en segundos enteros para facilitar la lectura. La radio almacena y espera el valor en milisegundos; AetherSDR multiplica por 1000 antes de enviar el comando a la radio.

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres amigables a cada puerto de antena en la radio.

### Controles de nombre de antena

| Control | Tipo | Notas |
|---|---|---|
| **ANT1 / ANT2 / XVTA / XVTB** | Campo de texto | Etiqueta amigable para cada puerto de antena. Los nombres aparecen en el selector de antena del scope de banda y en el menú desplegable de antena TX. |

1. Haga clic en la pestaña **Antennas**.
2. Ingrese un nombre personalizado para cada puerto de antena (ANT1, ANT2, XVTA, XVTB).
3. Los nombres se almacenan en AppSettings y se envían a la radio.

## Pestaña Phone/CW

La pestaña Phone/CW configura los valores predeterminados del micrófono, el manipulador CW y RTTY.

### Configuración del manipulador CW

| Control | Tipo | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Iambic:** | Botón de alternancia | — | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Botón | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. |
| **Swap:** | Botón de alternancia | — | — | Intercambia dit/dah. |
| **Sideband:** | Combo box | — | LSB / USB | Selecciona la banda lateral de tono CW. |
| **CWX:** | Botón de alternancia | — | — | Habilita la activación por macros CWX. |
| **Decode:** | Botón de alternancia | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. |

### Otros ajustes de audio

| Control | Tipo | Notas |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en recepción. |
| **RTTY Mark Default:** | Spin box | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña RX contiene controles para la calibración manual de compensación de frecuencia y la selección de la fuente de referencia de 10 MHz. Los controles de calibración siempre se muestran independientemente de si hay un GPSDO instalado.

### Cómo ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra el texto de progreso ("Starting…" luego el estado en vivo).
   - Antes de iniciar, AetherSDR restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no continúa.
5. Cuando la calibración se completa, el botón se vuelve a habilitar y el campo de estado muestra el resultado.
6. Si necesita establecer una compensación manualmente, ingrese un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control | Tipo | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Spin box | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en **Start**. |
| **Start** | Botón | Inicia la calibración. Restablece `freq_error_ppb` a 0, luego emite `radio pll_start`. Deshabilitado mientras está ocupado. |
| **Freq Offset (ppb):** | Spin box | Compensación de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Combo box | Predeterminado: Auto. Selecciona la referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Controles de salida de audio

| Control | Tipo | Notas |
|---|---|---|
| **Line Out:** | Deslizador | Ganancia de línea de salida. |
| **Mute (Line Out)** | Botón | Silencia la línea de salida. |
| **Headphone:** | Deslizador | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón | Silencia los auriculares. |
| **Front Speaker: / Mute** | Botón | Silencia el altavoz frontal (específico del modelo). |

### Códec de audio

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón | Auto | Selecciona el códec de audio para SmartLink/LAN. |

### Configuración de audio de PC

| Control | Tipo | Notas |
|---|---|---|
| **PC Audio Devices: Input: / Output:** | Combo box | Elige los dispositivos de audio de entrada/salida del host. |
| **Audio Boost:** | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | Campo de texto | Predeterminado: 200. Rango válido: 50–1000 ms. Aumenta el búfer de audio para fluctuaciones de VPN/SmartLink. |

### Configuración del sistema

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Prevent system sleep while connected** | Casilla de verificación | Falso | Mantiene el SO despierto mientras la radio está conectada. |

### Configuración de grabación

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Recording: Radio Side / Client Side** | Botón | Radio Side | Elige la grabación del lado de la radio o del lado del cliente. |
| **Save to:** | Campo de texto | — | Carpeta para las grabaciones guardadas (solo lado del cliente). Valor predeterminado: Documents/AetherSDR/Recordings. |
| **...** | Botón | — | Examina para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | Casilla de verificación | Falso | Graba automáticamente durante la transmisión. |
| **Idle timeout:** | Spin box | 120 | Rango válido: 10–3600 seg. Segundos de silencio antes de detener la grabación. |

### NVIDIA BNR

| Control | Tipo | Notas |
|---|---|---|
|
