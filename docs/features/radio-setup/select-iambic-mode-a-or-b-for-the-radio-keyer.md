# Diálogo de configuración de la radio

Esta página describe todos los controles en el diálogo **Radio Setup** (`Settings > Radio Setup...`). El diálogo tiene una barra de pestañas en la parte superior; cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Model** | Modelo de la radio (solo lectura). |
| **HW Version** | Cadena de versión de hardware (solo lectura). |
| **Region** | Región regulatoria; predeterminado USA (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). |
| **License Info** | Muestra suscripción, vencimiento, ID de radio y versión licenciada de la radio (solo lectura). |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo descriptivo de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Se almacena en `StationName`. Si se deja vacío, usa el nombre de host del SO. Se envía a la radio como `client station <nombre>`. |

### Botones de copia

Cada indicador de solo lectura en la pestaña Radio tiene ahora un pequeño **botón de copiar al portapapeles** (icono de documentos superpuestos) a su derecha. Haga clic en el botón para copiar el valor del indicador al portapapeles del sistema. Aparece una breve etiqueta emergente ("¡Copiado!") cerca del botón después de una copia exitosa. El botón se muestra atenuado visualmente cuando el valor está vacío o es un marcador de posición con guión.

| Indicador con botón de copiar | Valor copiado |
|---|---|
| **Radio SN** | El número de serie del chasis, o el número de serie de la radio si el del chasis está vacío. |
| **Model** | La cadena del modelo de la radio. |
| **HW Version** | La cadena de versión de hardware, con prefijo "v" si aún no lo tiene. |
| **Region** | La cadena de la región regulatoria. |
| **FlexControl** | La cadena del estado de detección de FlexControl. |
| **multiFLEX** | La cadena del estado habilitado de multiFLEX. |
| **Options** | La cadena de opciones licenciadas; si está vacía, muestra "GPS" o "GPS, PGXL" según la presencia del amplificador. |
| **License Info** | La cadena completa de detalles de licencia tal como se muestra. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita el encendido remoto / remote-on. |
| **Check for Update** | Consulta si hay actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado muestra: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta muestra: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador SmartSDR `.msi` (formato FlexRadio v4.2+ WiX), un instalador autoextraíble `.exe` (versiones antiguas) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato con los primeros 8 bytes (magic OLE/MSI vs. cabecera MZ PE/COFF) y extrae el payload `.ssdr` sin herramientas externas. Anteriormente etiquetado **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Inicia la carga del firmware. Una barra de progreso y una etiqueta de estado siguen el progreso. Se habilita solo después de que un archivo válido haya sido preparado por **Select Installer...**. |

### Preparación de una actualización de firmware (v0.9.3 y posteriores)

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from <nombre_archivo>...* mientras el preparador extrae el payload.
4. Cuando la preparación se completa, la etiqueta de estado confirma que está listo y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

---

## Pestaña Network

Muestra direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura informadas por la radio. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | — | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spinbox | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango: 576–9000. Se almacena en `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | Cambia entre modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — | Campos de configuración de IP estática. |
| **Apply** | Botón pulsador | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

Muestra la presencia de GPS y datos de posición en vivo cuando hay un receptor GPS conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y número de satélites. Se actualiza en tiempo real. |

---

## Pestaña TX

Controla tiempos de TX, enclavamientos, límites de potencia, modo de sintonía y comportamiento de seguimiento de slice.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Campos Spinbox | — | Tiempos de retención y retardo de TX. Campos: ACC TX (ms), TX Delay (ms), RCA TX1 (ms). |
| **Timeout (sec):** | Spinbox | — | Tiempo de espera de enclavamiento en segundos. El valor se envía a la radio en milisegundos (multiplicado por 1000). |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y Accessory. |
| **Max Power:** | Spinbox | — | Límite de potencia TX a nivel de radio (0–100%). |
| **Tune Mode:** | Combo box | — | Selecciona cómo se comporta el botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en el display de waterfall. |
| **TX Follows Active Slice** | Botón pulsador | Falso | TX sigue al slice activo. Es mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación en Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón pulsador | Falso | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. Se almacena en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón pulsador | — | Abre el diálogo dedicado de potencia y sintonía por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Manipulador iambic

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** muestra **Enabled**. Si muestra **Disabled**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iambic Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Botón pulsador (par mutuamente excluyente) | A | Selecciona el modo iambic Curtis A o B tanto para el manipulador de hardware de la radio como para el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. Agregado en v0.9.1. |
| **Swap:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Sideband:** | Combo box | — | Selecciona la banda lateral del tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita el keying de macros CWX. |
| **Decode:** | Botón de alternancia | Verdadero | Habilita la superposición de decodificación CW en el panadapter. Se almacena en `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | — | Frecuencia predeterminada de marca RTTY. |

**Modo A vs. Modo B:** El modo A (Curtis A) suelta el último elemento cuando ambas paletas se liberan durante un apriete simultáneo. El modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador de software local refleja el modo que seleccione, proporcionando una respuesta de tono lateral inferior a 5 ms independiente de la latencia de red.

---

## Pestaña RX

Proporciona calibración de offset de frecuencia GPSDO y selección de fuente de referencia de 10 MHz.

En v0.9.2.1, los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo muestra:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración se ejecuta.
   - La etiqueta de estado informa el progreso (Starting… y estados posteriores).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración se completa, el botón se rehabilita y la etiqueta de estado se actualiza con el resultado.
6. Si **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | — | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón pulsador | — | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y etiqueta como Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Spinbox | — | Offset de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| **10 MHz Reference Source:** | Combo box | Auto | Selecciona la fuente de referencia del oscilador. El combo se llena dinámicamente según el hardware instalado y el estado actual del oscilador: **Auto**, **TCXO**, **GPSDO** y **External 10 MHz** aparecen solo cuando el hardware correspondiente se detecta o fue seleccionado previamente. Cuando **Auto** está activo, la etiqueta de estado muestra la fuente resuelta (por ejemplo, *Auto -> GPSDO*). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, *GPSDO -> TCXO*). El estado de bloqueo (**Locked** / **Unlocked**) se agrega y se actualiza en vivo; si **External 10 MHz** está seleccionado pero no se detecta señal externa, se agrega *(not detected)*. |

---

## Pestaña Antennas

Configura nombres de antena definidos por el usuario para cada puerto de antena TX.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **ANT1 / ANT2 / XVTA / XVTB** | Campos de texto | — | Ingrese un nombre personalizado (hasta 20 caracteres) para cada puerto de antena. Los nombres se envían a la radio y se muestran en los botones de band-stack y en el selector de antena de slice. |

---

## Pestaña Audio

Configura las salidas de audio de la radio, los dispositivos de audio del PC, la grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Line Out:** | Deslizador | — | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón pulsador | — | Silencia la salida de línea. |
| **Headphone:** | Deslizador | — | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón pulsador | — | Silencia la salida de auriculares. |
| **Front Speaker: / Mute** | Botón pulsador | — | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón pulsador | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Se almacena en `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | Falso | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en los flujos de audio/TCP/UDP durante inactividad. Se almacena en `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Combo box | — | Elige los dispositivos de audio de entrada y salida del host. |
| **Audio Boost:** | Botón de alternancia | — | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en `AudioBoost`. |
| **Audio Buffer:** | Campo de texto | 200 | Tamaño del búfer de audio en milisegundos para compensación de jitter en VPN/SmartLink. Rango: 50–1000 ms. Se almacena en `AudioBufferMs`. |
| **Recording: Radio Side / Client Side** | Botón pulsador | Radio Side | Selecciona grabación del lado de la radio o del lado del cliente. Se almacena en `RecordingMode`. |
| **Save to:** | Campo de texto | — | Carpeta para grabaciones guardadas (solo lado del cliente). Predeterminado: Documentos/AetherSDR/Recordings. Se almacena en `QsoRecordingDir`. |
| **...** |
