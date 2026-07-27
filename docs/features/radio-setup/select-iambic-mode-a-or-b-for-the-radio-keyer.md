# Diálogo de Configuración de Radio

Esta página describe todos los controles del diálogo **Radio Setup**  
(`Settings > Radio Setup...`). El diálogo tiene una barra de pestañas en la parte superior; cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. |
| **Model** | Modelo de la radio (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **HW Version** | Cadena de versión de hardware (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **Region** | Región regulatoria; predeterminado EE. UU. (solo lectura). |
| **FlexControl** | Estado de detección del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado de habilitación de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **License Info** | Muestra la suscripción, la fecha de vencimiento, el ID de radio y la versión licenciada desde la radio (solo lectura). Cada campo incluye un botón de copia al portapapeles junto al valor. |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo descriptivo de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Se almacena en `StationName`. Toma como valor predeterminado el nombre de host del SO si se deja vacío. Se envía a la radio como `client station <nombre>`. |

### Botones de copia

Cada indicador de solo lectura en la pestaña Radio ahora tiene un pequeño **botón de copia al portapapeles** (icono de documentos superpuestos) a su derecha. Haga clic en el botón para copiar el valor del indicador al portapapeles del sistema. Aparece una breve etiqueta emergente ("¡Copiado!") cerca del botón tras una copia exitosa. El botón se atenúa visualmente cuando el valor está vacío o es un marcador de posición con guión.

| Indicador con botón de copia | Valor copiado |
|---|---|
| **Radio SN** | El número de serie del chasis, o el número de serie de la radio si el del chasis está vacío. |
| **Model** | La cadena del modelo de la radio. |
| **HW Version** | La cadena de la versión de hardware, con el prefijo "v" si aún no está presente. |
| **Region** | La cadena de la región regulatoria. |
| **FlexControl** | La cadena del estado de detección de FlexControl. |
| **multiFLEX** | La cadena del estado de habilitación de multiFLEX. |
| **Options** | La cadena de opciones licenciadas; si está vacía, muestra "GPS" o "GPS, PGXL" según la presencia del amplificador. |
| **License Info** | La cadena completa de detalles de la licencia tal como se muestra. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita el encendido remoto / activación remota. |
| **Check for Update** | Consulta las actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado dice: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta dice: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador SmartSDR `.msi` (formato FlexRadio v4.2+ WiX), un instalador autoextraíble `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. cabecera MZ PE/COFF) y extrae la carga útil `.ssdr` sin herramientas externas. Anteriormente etiquetado **Browse .ssdr...** (cambiado en v26.5.3). |
| **Upload Firmware** | Inicia la carga del firmware. Una barra de progreso y una etiqueta de estado siguen el progreso. Solo se habilita después de que un archivo válido haya sido preparado por **Select Installer...**. |
| **Reboot Radio** | Solicita confirmación: *Reboot the connected radio now?* El texto de advertencia difiere para conexiones WAN (SmartLink) vs. LAN. En LAN, AetherSDR se reconectará automáticamente después de que la radio arranque. En WAN, debe reconectarse manualmente. Al hacer clic en Aceptar, se envía el comando de reinicio y se cierra el diálogo. Deshabilitado cuando la radio no está conectada. Estilizado con un fondo rojizo para indicar la naturaleza destructiva de la acción. |

### Preparación de una actualización de firmware

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from \<nombrearchivo\>...* mientras el preparador extrae la carga útil.
4. Cuando la preparación se completa, la etiqueta de estado confirma la disponibilidad y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

---

## Pestaña Network

Muestra las direcciones de red y le permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura informadas por la radio. Cada una incluye un botón de copia al portapapeles. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | Habilitado | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spinbox | 1450 | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576–9000. Almacenado en `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static** | Botón de alternancia | — | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — | Campos de configuración de IP estática. |
| **Apply** | Botón pulsador | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

Muestra la presencia de GPS y datos de posición en vivo cuando hay un receptor GPS conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y número de satélites. Actualizado en tiempo real. |

---

## Pestaña TX

Controla los tiempos de TX, límites de potencia, modo de sintonía (Tune) y el comportamiento de seguimiento de slice (receptor virtual).

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Campos Spinbox | — | Tiempos de retención (hang) y retardo (delay) de TX. Campos: ACC TX (ms), TX Delay (ms), RCA TX1 (ms). |
| **Timeout (sec):** | Spinbox | — | Tiempo de espera de interbloqueo en segundos. El valor se envía a la radio en milisegundos (multiplicado por 1000). |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de interbloqueo RCA y de accesorio. |
| **Max Power:** | Spinbox | — | Límite de potencia TX a nivel de radio (0–100%). |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal de TX en la visualización del waterfall. |
| **TX Follows Active Slice** | Botón pulsador | False | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split (dividido). Almacenado en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón pulsador | False | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Almacenado en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón pulsador | — | Abre el diálogo dedicado de potencia y sintonía por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW (keyer) y los valores predeterminados de RTTY.

### Manipador iámbico (Iambic keyer)

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** dice **Enabled**. Si dice **Disabled**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iámbico Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iámbico en la radio. Siempre dice "Enabled" cuando está activado. |
| **Iambic Mode: A / B** | Botón pulsador (par mutuamente excluyente) | A | Selecciona el modo iámbico Curtis A o B tanto para el manipulador de hardware de la radio como para el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. |
| **Swap:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Sideband:** | Cuadro combinado | — | Selecciona la banda lateral del tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita la activación de macros CWX. |
| **Decode:** | Botón de alternancia | True | Habilita la superposición de decodificación CW en el panadapter. Almacenado en `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | — | Frecuencia predeterminada de marca RTTY. |

**Modo A vs. Modo B:** El modo A (Curtis A) suelta el último elemento cuando ambas paletas se sueltan a medio apretar (squeeze). El modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador de software local refleja el modo que seleccione, proporcionando una respuesta de tono sidetone inferior a 5 ms, independiente de la latencia de la red.

---

## Pestaña RX

Proporciona calibración de compensación de frecuencia del GPSDO y selección de la fuente de referencia de 10 MHz.

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo dice:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - La etiqueta de estado informa el progreso (Starting… y estados subsiguientes).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración se completa, el botón se vuelve a habilitar y la etiqueta de estado se actualiza con el resultado.
6. Si **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | — | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón pulsador | — | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y etiqueta como Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Spinbox | — | Compensación de frecuencia manual en partes por billón (ppb). Se aplica directamente sin ejecutar un barrido. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador. El cuadro combinado se completa dinámicamente según el hardware instalado y el estado actual del oscilador: **Auto**, **TCXO**, **GPSDO** y **External 10 MHz** aparecen solo cuando el hardware correspondiente se detecta o se seleccionó previamente. Cuando **Auto** está activo, la etiqueta de estado muestra la fuente resuelta (por ejemplo, *Auto -> GPSDO*). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, *GPSDO -> TCXO*). El estado de bloqueo (**Locked** / **Unlocked**) se añade y se actualiza en vivo; si se selecciona **External 10 MHz** pero no se detecta ninguna señal externa, se añade *(not detected)*. |

---

## Pestaña Antennas

Configura nombres de antena definidos por el usuario para cada puerto de antena TX.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **ANT1 / ANT2 / XVTA / XVTB** | Campos de texto | — | Introduzca un nombre personalizado (hasta 20 caracteres) para cada puerto de antena. Los nombres se envían a la radio y se muestran en los botones de banda (band-stack) y en el selector de antena del slice. |

---

## Pestaña Audio

Configura las salidas de audio de la radio, los dispositivos de audio del PC, la grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Line Out:** | Control deslizante | — | Ganancia de la salida de línea. |
| **Mute (Line Out)** | Botón pulsador | — | Silencia la salida de línea. |
| **Headphone:** | Control deslizante | — | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón pulsador | — | Silencia la salida de auriculares. |
| **Front Speaker: / Mute** | Botón pulsador | — | Silencia el altavoz frontal (según el modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón pulsador | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Almacenado en `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | False | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de fluj
