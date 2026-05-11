# Configuración de la Radio

El cuadro de diálogo Configuración de la Radio es la ventana maestra de configuración por radio. Organiza la identificación de la radio, red, GPS, transmisión, teléfono/CW, recepción, audio, filtros, transvertidores, cables USB, periféricos y ajustes de puerto serie en varias pestañas.

## Cómo abrir Configuración de la Radio

1. Abra `Settings > Radio Setup...`.
2. El cuadro de diálogo se abre como una ventana sin marco con una barra de título personalizada. Arrastre la barra de título para mover la ventana.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de la radio

| Control | Tipo | Notas |
|---|---|---|
| **Radio SN** | Indicador | Número de serie del chasis (solo lectura). |
| **Region** | Indicador | Región regulatoria de la radio. |
| **HW Version** | Indicador | Cadena de la versión del hardware. |
| **Model** | Indicador | Modelo de la radio. |
| **Options** | Indicador | Muestra las opciones de radio licenciadas. |
| **FlexControl** | Indicador | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Indicador | Estado de multiFLEX habilitado. |

### Identificación

| Control | Tipo | Notas |
|---|---|---|
| **Nickname** | Campo de texto | Apodo de la radio fácil de usar. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto, usa el nombre del host del SO si está vacío. Se almacena en AppSettings. Se envía a la radio como 'client station <nombre>'. |

### Información de la licencia

El cuadro de diálogo muestra los detalles de la licencia de la radio, incluyendo el estado de la suscripción, la fecha de vencimiento, el ID de la radio y la versión licenciada.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar actualizaciones de firmware.
   - Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
2. Descargue el instalador de SmartSDR desde flexradio.com si hay uno disponible.
3. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo `.ssdr` preextraído.
   - El preparador de firmware detecta el formato del archivo automáticamente y extrae el `.ssdr` sin necesidad de herramientas externas.
   - Mientras el preparador prepara el firmware, se muestra la barra de progreso y la etiqueta de estado dice "Preparing firmware from \<nombre_de_archivo\>...".
4. Una vez que la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio. El progreso y el resultado se muestran en la etiqueta de estado.

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta actualizaciones de firmware disponibles. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. Anteriormente etiquetado como **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Botón | Inicia la carga del firmware. La barra de progreso y la etiqueta de estado se actualizan durante el proceso. |

### Encendido remoto

Haga clic en **Remote On** para habilitar la capacidad de encendido/activación remota.

## Pestaña Network

La pestaña Network muestra la información de red de la radio y ofrece opciones de red avanzadas.

### Información de red

| Control | Tipo | Notas |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicador | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Tipo | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | — | — | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spin box | 1450 | 576–9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | — | Cambia entre modos DHCP y IP estática. |
| **IP Address: / Mask: / Gateway:** | Campo de texto | — | — | Campos de configuración de IP estática. |

### Aplicar configuración de red

Haga clic en **Apply** para enviar la configuración de red a la radio.

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y la información en vivo de latitud, longitud, altitud, hora y satélites.

## Pestaña TX

Use esta página para configurar los ajustes de transmisión, incluyendo temporizaciones, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall y comportamiento de seguimiento de slice/TX.

### Configuración de banda TX

Haga clic en **TX Band Settings** para abrir el cuadro de diálogo dedicado de potencia y sintonía por banda.

### Controles de TX

| Control | Tipo | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Max Power:** | Spin box | — | 0–100 % | Establece el límite de potencia TX a nivel de radio. |
| **Tune Mode:** | Combo box | — | Consulte las opciones del firmware de la radio | Selecciona cómo se comporta el botón de sintonía. |
| **Timings (in ms)** | Spin box | — | — | Temporizaciones de mantenimiento/retardo de TX. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | — | Habilita las entradas de enclavamiento RCA y Accessory. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Enabled / Disabled | Dibuja la señal TX en el waterfall. |
| **TX Follows Active Slice** | Botón | False | — | TX sigue a la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | False | — | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |

## Pestaña Phone/CW

La pestaña Phone/CW configura los valores predeterminados de micrófono, manipulador CW y RTTY.

### Configuración del manipulador CW

| Control | Tipo | Valor predeterminado | Rango válido | Notas |
|---|---|---|---|---|
| **Iambic:** | Botón de alternancia | — | Enabled / Disabled | Habilita o deshabilita el manipulador iámbico en la radio. |
| **Iambic Mode: A / B** | Botón | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. |
| **Swap:** | Botón de alternancia | — | — | Intercambia dit/dah. |
| **Sideband:** | Combo box | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | Botón de alternancia | — | — | Habilita el accionamiento de macros CWX. |
| **Decode:** | Botón de alternancia | True | — | Habilita la superposición de decodificación CW en el panadapter. |

### Otros ajustes de audio

| Control | Tipo | Notas |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | Muestra el medidor de nivel del micrófono incluso en RX. |
| **RTTY Mark Default:** | Spin box | Frecuencia predeterminada de marca RTTY. |

## Pestaña RX

La pestaña RX contiene controles para la calibración manual del desplazamiento de frecuencia y la selección de la fuente de referencia de 10 MHz. Los controles de calibración siempre se muestran, independientemente de si hay un GPSDO instalado.

### Cómo realizar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en ejecución.
   - El campo de estado a la derecha del botón muestra el texto de progreso ("Starting…" y luego el estado en vivo).
   - Antes de comenzar, AetherSDR restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no se realiza.
5. Cuando la calibración se complete, el botón se reactiva y el campo de estado muestra el resultado.
6. Si necesita establecer un desplazamiento manualmente, ingrese un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control | Tipo | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Spin box | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en **Start**. |
| **Start** | Botón | Inicia la calibración. Restablece `freq_error_ppb` a 0, luego emite `radio pll_start`. Se deshabilita mientras está ocupado. |
| **Freq Offset (ppb):** | Spin box | Desplazamiento manual de frecuencia en partes por mil millones. |
| **10 MHz Reference Source:** | Combo box | Valor predeterminado: Auto. Selecciona la referencia del oscilador. Opciones: Auto, TCXO, GPSDO, External. El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. |

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y el contenedor NVIDIA BNR.

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
| **PC Audio Devices: Input: / Output:** | Combo box | Selecciona los dispositivos de audio de entrada/salida del host. |
| **Audio Boost:** | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. |
| **Audio Buffer:** | Campo de texto | Valor predeterminado: 200. Rango válido: 50–1000 ms. Aumenta el búfer de audio para compensar la fluctuación de VPN/SmartLink. |

### Configuración del sistema

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Prevent system sleep while connected** | Casilla de verificación | False | Mantiene el SO activo mientras la radio está conectada. |

### Configuración de grabación

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| **Recording: Radio Side / Client Side** | Botón | Radio Side | Selecciona la grabación del lado de la radio o del lado del cliente. |
| **Save to:** | Campo de texto | — | Carpeta para las grabaciones guardadas (solo del lado del cliente). Valor predeterminado: Documents/AetherSDR/Recordings. |
| **...** | Botón | — | Busca la carpeta de grabación. |
| **Auto-record on TX** | Casilla de verificación | False | Graba automáticamente mientras se transmite. |
| **Idle timeout:** | Spin box | 120 | Rango válido: 10–3600 seg. Segundos de silencio antes de que la grabación se detenga. |

### NVIDIA BNR

| Control | Tipo | Notas |
|---|---|---|
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Botón | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. Un punto de color indica el estado del Contenedor (Running/Stopped/Unknown). |

## Pestaña Filters

La pestaña Filters configura opciones de filtro de baja latencia o pronunciados por ancho de banda.

### Controles de nitidez de filtro

| Control | Tipo | Valor predeterminado | Notas |
|---|---|---|---|
| Deslizadores de nitidez de filtro Voice / CW / Digital | Deslizador | — | Establece la nitidez del filtro (0=mínima latencia a 3=máxima nitidez) por modo. El deslizador se deshabilita cuando Auto está habilitado. |
| Auto (Voice / CW / Digital) | Botón de alternancia | — | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | — | Fuerza filtros de baja latencia en DIGU/DIGL. |

## Pestaña XVTR

La pestaña XVTR proporciona la configuración por transvertidor. Contiene pestañas anidadas, una por transvertidor, y una pestaña '+' para crear nuevos transvertidores.

| Control | Tipo | Notas |
|---|---|---|
| **RX Only:** | Botón de alternancia | Fuerza solo RX en ese transvertidor. |
| **Remove (xvtr)** | Botón | Elimina la definición del transvertidor. |
| **Create New Transverter** | Botón | Agrega una nueva entrada de transvertidor. |

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores de serie USB a tipos de cable CAT, BCD, bit y PTT.

### Configuración de cable

| Control | Tipo | Notas |
|---|---|---|
| Lista de cables / Estado | Indicador | Cables USB detectados por tipo con estado Plugged/Unplugged. |
| Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7) | Combo box | Parámetros de serie y comportamiento por cable. |

## Pestaña Peripherals

La pestaña Peripherals proporciona conexión IP manual para dispositivos externos, incluyendo TGXL, PGXL, Antenna Genius y ShackSwitch.

### Conexión de dispositivos periféricos

Cada dispositivo tiene su propia fila con botones **Connect** / **Disconnect**, campo de dirección IP, campo de puerto e indicador de estado.

#### Comportamiento al borrar el campo IP

- Si borra el campo de dirección IP y hace clic en **Connect** mientras está desconectado, cualquier IP y puerto manual previamente guardados se eliminan de la configuración y el dispositivo deja de conectarse automáticamente al inicio.
- Si borra el campo de dirección IP y cierra el cuadro de diálogo sin hacer clic en **Connect** o **Disconnect**, la IP y el puerto manual guardados también se eliminan y el dispositivo se desconecta si estaba conectado.

#### TGXL

| Control | Valor pred
