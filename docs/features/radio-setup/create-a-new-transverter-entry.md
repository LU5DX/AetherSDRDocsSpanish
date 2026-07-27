# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona controles para información del radio, red, GPS, TX, antenas, Phone/CW, RX, audio, filtros, XVTR, cables USB, periféricos, serial (FlexControl), APD, temas, gestión de certificados fijados SmartLink, receptor público KiwiSDR, búsqueda de indicativos e integración con amplificador ACOM.

## Abrir el diálogo

1. Seleccione `Settings > Radio Setup...` en el menú principal.
2. El diálogo se abre como una ventana persistente que recuerda su posición y tamaño entre sesiones. Puede arrastrarla por la barra de título.
3. Cierre el diálogo haciendo clic en el botón **X** de la barra de título o presionando `Escape`.

## Pestaña Radio

La pestaña **Radio** muestra la identificación del radio, información de licencia y controles de actualización de firmware. El contenido de la pestaña está envuelto en un área desplazable para que todos los controles sigan siendo accesibles en pantallas pequeñas o de alta densidad.

### Información del radio (solo lectura)

Cada campo de solo lectura incluye un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar. Haga clic en el botón para copiar el valor del campo al portapapeles del sistema. Un breve mensaje emergente "¡Copiado!" confirma la acción.

| Control | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis. Haga clic en el botón de copia para copiar. |
| **Region** | Región regulatoria del radio. |
| **HW Version** | Cadena de versión del hardware. Haga clic en el botón de copia para copiar. |
| **Model** | Modelo del radio. |
| **Options** | Muestra las opciones del radio con licencia. Haga clic en el botón de copia para copiar. |
| **FlexControl** | Estado detectado del hardware FlexControl. |
| **multiFLEX** | Estado de habilitación de multiFLEX. |
| **License Info** | Muestra suscripción, vencimiento, ID de Radio (haga clic en el botón de copia para copiar) y detalles de la versión con licencia. |

### Campos de identificación

| Control | Comportamiento |
|---|---|
| **Nickname** | Apodo del radio fácil de usar. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica a este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto es el nombre de host del SO si está vacío. Se almacena en la configuración `StationName`. Se envía al radio como "client station <nombre>". |

### Remote On

Haga clic en **Remote On** para habilitar la capacidad de encendido remoto / activación remota.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar el radio conectado. Aparece un diálogo de confirmación antes de proceder con el reinicio.

- **En una conexión LAN**: AetherSDR se desconecta y se reconecta automáticamente una vez que el radio termina de arrancar.
- **En una conexión SmartLink/WAN**: AetherSDR se desconecta. Deberá reconectarse manualmente después de que el radio termine de arrancar.

El botón está deshabilitado cuando el radio está desconectado. Se rehabilita automáticamente cuando el radio se reconecta, sin necesidad de volver a abrir el diálogo.

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar al servidor de actualizaciones de FlexRadio las versiones de firmware disponibles.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` preextraído. El preparador detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. Aparece un indicador de progreso mientras se completa la preparación.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado al radio.

## Pestaña Network

La pestaña **Network** muestra la información de red del radio y proporciona opciones de red avanzadas.

### Información de red (solo lectura)

| Control | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. Cada campo incluye un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar. Haga clic en el botón para copiar el valor al portapapeles del sistema. |

### Configuración de red

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Off | - | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | 1450 | 576-9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en la configuración `NetworkMtu`. |
| **DHCP / Static** | DHCP | - | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | - | - | Campos de configuración de IP estática (se muestran cuando se selecciona el modo Estático). |
| **Apply** | - | - | Envía la configuración de red al radio. |

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

## Pestaña TX

La pestaña **TX** controla temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, slice/TX seguimiento y proporciona un acceso directo a la Configuración de Banda TX.

### Configuración de Banda TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones de TX

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | - | - | Temporizaciones de espera / retardo de TX. |

### Otros controles de TX

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Interlocks - TX REQ: RCA / Accessory** | Off | - | Habilita las entradas de enclavamiento RCA y de accesorio. |
| **Max Power:** | - | 0-100 % | Establece el límite de potencia de TX a nivel de radio. |
| **Tune Mode:** | - | - | Selecciona cómo se comporta el botón de sintonía. |
| **Show TX in Waterfall:** | Off | - | Dibuja la señal de TX en el waterfall. |
| **TX Follows Active Slice** | False | - | TX sigue a la slice activa. Es mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante una operación de Split. Se almacena en la configuración `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | False | - | Cambia la slice activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Es mutuamente excluyente con 'TX Follows Active Slice'. Se almacena en la configuración `ActiveFollowsTxSlice`. |

## Pestaña Antennas

La pestaña **Antennas** le permite asignar nombres personalizados a cada puerto de antena en el radio. Esta pestaña se construye de forma diferida cuando se hace clic por primera vez.

### Campos de nombre de antena

| Control | Comportamiento |
|---|---|
| **ANT1 - ANT8** | Campos de texto para asignar nombres fáciles de usar a cada puerto de antena. Los nombres se almacenan en el radio. |

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de audio

| Control | Comportamiento |
|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. |

### Manipulador CW

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Iambic:** | Deshabilitado | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en el radio. |
| **Iambic Mode: A / B** | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para el radio como para el manipulador de software local. Par mutuamente excluyente. |
| **Swap:** | Off | - | Intercambia dit/dah. |
| **Sideband:** | - | LSB / USB | Selecciona la banda lateral del tono CW. |
| **CWX:** | Off | - | Habilita la activación de macros CWX. |
| **Decode:** | True | - | Habilita la superposición de decodificación CW en el panadapter. Se almacena en la configuración `CwDecodeOverlay`. |

### RTTY

| Control | Comportamiento |
|---|---|
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. |

## Pestaña RX

La pestaña **RX** proporciona calibración de compensación de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo dice:
- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y etiqueta como **Busy** mientras un barrido está en progreso. |
| **Freq Offset (ppb):** | Compensación de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de calibración: Iniciando, texto de progreso o error. Se actualiza en vivo durante el barrido. |

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** selecciona qué oscilador utiliza el radio como referencia de frecuencia.

#### Población del cuadro combinado

El cuadro combinado se puebla dinámicamente según lo que informa el radio. Los elementos aparecen de acuerdo con las siguientes reglas:

| Etiqueta del elemento | Cuándo se muestra |
|---|---|
| Auto | Siempre presente. |
| TCXO | Presente cuando el radio ha informado algún estado del oscilador, cuando el radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Presente cuando el radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Presente cuando el radio ha informado algún estado del oscilador, cuando el radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

El cuadro combinado selecciona el elemento que coincide con el `oscSetting` actual del radio. Si ese valor no está en la lista, el cuadro combinado vuelve a la selección actual y luego a **Auto**.

#### Etiqueta de estado de bloqueo

La etiqueta a la derecha del cuadro combinado muestra el estado actual del oscilador y la condición de bloqueo.

| Condición | Texto de la etiqueta | Color |
|---|---|---|
| Aún no se ha recibido estado | Waiting for oscillator status | Gris |
| La configuración es Auto, el radio ha seleccionado una fuente | Auto -> \<fuente\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración difiere del estado activo | \<configuración\> -> \<activo\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración coincide con el estado activo | \<fuente\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| External seleccionado pero no se detecta señal externa | \<texto\> (not detected) añadido | Verde (bloqueado) / Rojo (desbloqueado) |

El radio envía `ext` para la fuente externa en algunas respuestas de firmware. AetherSDR normaliza esto a `external` antes de mostrarlo, por lo que la etiqueta siempre lee **External 10 MHz** en lugar de **Ext**.

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio del radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR. El contenido de la pestaña está envuelto en un área desplazable para que todos los controles sigan siendo accesibles en pantallas pequeñas o de alta densidad.

### Salidas del radio

| Control | Comportamiento |
|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea. |
| **Mute (Line Out)** | Silencia la salida de línea. |
| **Headphone:** | Deslizador de ganancia de auriculares. |
| **Mute (Headphone)** | Silencia los auriculares. |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Auto | Selecciona el códec de audio para SmartLink/LAN. Se almacena en la configuración `AudioCompression`. |

### Gestión de energía

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Prevent system sleep while connected** | False | Mantiene el SO despierto mientras el radio está conectado para evitar caídas de flujo de audio/TCP/UDP durante la inactividad. Se almacena en la configuración `InhibitSleepWhileConnected`. |

### Dispositivos de audio del PC

| Control | Comportamiento |
|---|---|
| **PC Audio Devices: Input: / Output:** | Selecciona los dispositivos de audio de entrada/salida del host. |

### Refuerzo y búfer de audio

| Control | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|
| **Audio Boost:** | Off | - | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en la configuración `AudioBoost`. |
| **Audio Buffer:** | 200 | 50-1000 ms | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Se almacena en la configuración `AudioBufferMs`. |

### Grabación

| Control | Valor predeterminado | Comportamiento |
|---|---|---|
| **Recording: Radio Side / Client Side** | Radio Side | Selecciona la grabación del lado del radio o del lado del cliente. Se almacena en la configuración `RecordingMode`. |
| **Save to:** | Documents/AetherSDR/Recordings | Carpeta para las grabaciones guardadas (solo del lado del cliente). Se almacena en la configuración `QsoRecordingDir`. |
| **...** | - | Busca la carpeta de grabación. |
| **Auto-record on TX** | False | Graba automáticamente mientras transmite. Se almacena en la configuración `QsoRecordingAutoRecord`. |
| **Idle timeout:** | 120 | 10-3600 seg | Segundos de silencio antes de que la grabación se detenga. Se almacena en la configuración `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

| Control | Comportamiento |
|---|---|
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla
