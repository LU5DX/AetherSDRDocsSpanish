# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Organiza la identificación de la radio, red, GPS, transmisión, teléfono/CW, recepción, nombres de antenas, filtros, transverters, cables USB, periféricos, APD, temas y configuraciones de puerto serie en múltiples pestañas.

## Abrir Configuración de la Radio

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como un diálogo persistente; su geometría se guarda y restaura automáticamente entre sesiones.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de la radio

| Control | Tipo | Notas |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). |
| **Region** | Indicador | Región regulatoria de la radio. |
| **HW Version** | Indicador | Cadena de versión del hardware. |
| **Model** | Indicador | Modelo de la radio. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado habilitado de multiFLEX. |

### Identificación

| Control | Tipo | Notas |
|---|---|---|
| **Nickname** | Campo de texto | Apodo amigable de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto, usa el nombre del host del SO si está vacío. Se almacena en AppSettings. Se envía a la radio como 'client station <nombre>'. |

### Información de licencia

El diálogo muestra los detalles de la licencia desde la radio, incluyendo estado de suscripción, fecha de vencimiento, ID de la radio y versión licenciada.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar actualizaciones de firmware.
   - Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
2. Descargue el instalador de SmartSDR desde flexradio.com si hay uno disponible.
3. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble anterior) o un archivo `.ssdr` preextraído.
   - El preparador de firmware detecta el formato del archivo automáticamente y extrae el `.ssdr` sin necesidad de herramientas externas.
   - Mientras el preparador prepara el firmware, se muestra la barra de progreso y la etiqueta de estado indica "Preparing firmware from <nombre_archivo>...".
4. Una vez completada la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio. El progreso y el resultado se muestran en la etiqueta de estado.

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta actualizaciones de firmware disponibles. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. Anteriormente etiquetado **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Botón | Inicia la carga del firmware. La barra de progreso y la etiqueta de estado se actualizan durante el proceso. |

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de encendido/activación remota.

## Pestaña Network

La pestaña Network muestra información de red de la radio y proporciona opciones de red avanzadas.

### Información de red

| Control | Tipo | Notas |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Tipo | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | — | — | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Cuadro de número | 1450 | 576–9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | — | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | — | — | Campos de configuración de IP estática. |

### Aplicar configuración de red

Haga clic en **Apply** para enviar la configuración de red a la radio.

## Pestaña GPS

La pestaña GPS muestra presencia de GPS e información en vivo de latitud, longitud, altitud, hora y satélites.

## Pestaña TX

Use esta página para configurar los ajustes de transmisión, incluyendo temporizaciones, enclavamientos, potencia máxima, modo de sintonización, visualización en waterfall y comportamiento de seguimiento de slice/TX.

### Configuración de banda TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y sintonización por banda.

### Controles TX

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Max Power:** | Cuadro de número | — | Rango válido: 0-100 %. Establece el límite de potencia TX a nivel de radio. |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón de sintonización. |
| **Timings** | Cuadro de número / Campo de texto | — | Ajustes de retención TX, retardo y tiempo de espera. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y Accessory. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en el waterfall. |
| **TX Follows Active Slice** | Botón | Falso | TX sigue al slice activo. Mutuamente excluyente con 'Active Slice Follows TX'. Se desactiva automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Falso | Cambia el slice activo cuando el TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con 'TX Follows Active Slice'. |

### Campos de temporización TX

| Campo | Etiqueta mostrada | Unidad reportada | Sufijo del comando |
|---|---|---|---|
| ACC TX | ACC TX | ms | `acc_tx_delay` |
| TX Delay | TX Delay | ms | `tx_delay` |
| RCA TX1 | RCA TX1 | ms | `tx1_delay` |
| Timeout (sec) | Timeout (sec) | segundos | `interlock_timeout` (el valor se multiplica por 1000 antes de enviarlo a la radio) |

El campo de tiempo de espera de enclavamiento se muestra en segundos enteros para facilitar la lectura. La radio almacena y espera el valor en milisegundos; AetherSDR multiplica por 1000 antes de enviar el comando a la radio.

## Pestaña Antennas

La pestaña Antennas permite asignar nombres amigables a cada puerto de antena de la radio.

### Controles de nombre de antena

| Control | Tipo | Notas |
|---|---|---|
| **ANT1 / ANT2 / XVTA / XVTB** | Campo de texto | Etiqueta amigable para cada puerto de antena. Los nombres aparecen en el selector de antena del scope de banda y en el menú desplegable de antena TX. |

1. Haga clic en la pestaña **Antennas**.
2. Ingrese un nombre personalizado para cada puerto de antena (ANT1, ANT2, XVTA, XVTB).
3. Los nombres se almacenan en AppSettings y se envían a la radio.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Configuración del manipulador CW

| Control | Tipo | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Iambic:** | Botón de alternancia | — | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Botón | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| **Swap:** | Botón de alternancia | — | — | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | Botón de alternancia | — | — | Habilita la activación de macros CWX. |
| **Decode:** | Botón de alternancia | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. |

### Otros ajustes de audio

| Control | Tipo | Notas |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| **RTTY Mark Default:** | Cuadro de número | Frecuencia predeterminada de marca RTTY. |

## Pestaña RX

La pestaña RX contiene controles para la calibración manual de compensación de frecuencia y selección de la fuente de referencia de 10 MHz. Los controles de calibración siempre se muestran independientemente de si hay un GPSDO instalado.

### Cómo ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se desactiva mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra texto de progreso ("Starting…" luego estado en vivo).
   - Antes de comenzar, AetherSDR restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no procede.
5. Cuando la calibración se completa, el botón se reactiva y el campo de estado muestra el resultado.
6. Si necesita establecer una compensación manualmente, ingrese un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control | Tipo | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de número | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en **Start**. |
| **Start** | Botón | Inicia la calibración. Restablece `freq_error_ppb` a 0, luego emite `radio pll_start`. Desactivado mientras está ocupado. |
| **Freq Offset (ppb):** | Cuadro de número | Compensación de frecuencia manual en partes por billón. |
| **10 MHz Reference Source:** | Cuadro combinado | Predeterminado: Auto. Selecciona la referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Controles de salida de audio

| Control | Tipo | Notas |
|---|---|---|
| **Line Out:** | Deslizador | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón | Silencia la salida de línea. |
| **Headphone:** | Deslizador | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón | Silencia los auriculares. |
| **Front Speaker: / Mute** | Botón | Silencia el altavoz frontal (específico del modelo). |

### Códec de audio

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón | Auto | Selecciona el códec de audio para SmartLink/LAN. |

### Configuración de audio del PC

| Control | Tipo | Notas |
|---|---|---|
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | Selecciona dispositivos de entrada/salida de audio del host. |
| **Audio Boost:** | Botón de alternancia | Habilita ganancia extra en la ruta de audio del cliente. |
| **Audio Buffer:** | Campo de texto | Predeterminado: 200. Rango válido: 50–1000 ms. Aumenta el búfer de audio para compensar la fluctuación de VPN/SmartLink. |

### Configuración del sistema

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Prevent system sleep while connected** | Casilla de verificación | Falso | Mantiene el SO despierto mientras la radio está conectada. |

### Configuración de grabación

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Recording: Radio Side / Client Side** | Botón | Radio Side | Elige grabación del lado de la radio o del lado del cliente. |
| **Save to:** | Campo de texto | — | Carpeta para las grabaciones guardadas (solo lado del cliente). Por defecto, Documents/AetherSDR/Recordings. |
| **...** | Botón | — | Navega para seleccionar la carpeta de grabación. |
| **Auto-record on TX** | Casilla de verificación | Falso | Graba automáticamente mientras transmite. |
| **Idle timeout:** | Cuadro de número | 120 | Rango válido: 10–3600 seg. Segundos de silencio antes de detener la grabación. |

### NVIDIA BNR

| Control | Tipo | Notas |
|---|---|---|
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Botón | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. Un punto de color indica el estado del contenedor (Running/Stopped/Unknown). |

## Pestaña Filters

La pestaña Filters configura opciones de filtro de baja latencia o agudos por ancho de banda.

### Controles de nitidez de filtro

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| Deslizadores de nitidez de filtro Voice / CW / Digital | Deslizador | — | Establece la nitidez del filtro (0=menor latencia a 3=más agudo) por modo. El deslizador se desactiva cuando Auto está habilitado. |
| Auto (Voice / CW / Digital) | Botón de alternancia | — | Habilita la selección automática del nivel de filtro para ese modo; desactiva el deslizador manual de nitidez. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | — | Fuerza filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR proporciona configuración por transverter. Contiene pestañas anidadas, una por transverter, y una pestaña '+' para crear nuevos transverters.

| Control | Tipo | Notas |
|---|---|---|
| **RX Only:** | Botón de alternancia | Fuerza solo RX en ese transverter. |
| **Remove (xvtr)** | Botón | Elimina la definición del transverter. |
| **Create New Transverter** | Botón | Agrega una nueva entrada de transverter. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores
