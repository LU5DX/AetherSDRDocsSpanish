# Diálogo Configuración de radio

Esta página describe cada control en el diálogo **Radio Setup**
(`Settings > Radio Setup...`). El diálogo tiene una tira de pestañas en la parte superior; cada sección siguiente cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación de la radio, información de licencia y controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Model** | Modelo de radio (solo lectura). |
| **HW Version** | Cadena de versión de hardware (solo lectura). |
| **Region** | Región regulatoria; por defecto USA (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado de habilitación de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio con licencia (solo lectura). |
| **License Info** | Muestra suscripción, vencimiento, Radio ID y versión con licencia desde la radio (solo lectura). |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo amigable para la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR a otras estaciones multiFLEX. Se guarda en `StationName`. Por defecto es el nombre de host del SO si se deja vacío. Se envía a la radio como `client station <name>`. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita el encendido remoto / remote-on. |
| **Check for Update** | Consulta las actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado lee: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta lee: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador SmartSDR `.msi` (formato WiX de FlexRadio v4.2+), un instalador autoextraíble `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (número mágico OLE/MSI frente a encabezado MZ de PE/COFF) y extrae la carga `.ssdr` sin herramientas externas. Etiquetado previamente como **Browse .ssdr...** (cambio en v0.9.3). |
| **Upload Firmware** | Inicia la carga del firmware. Una barra de progreso y una etiqueta de estado rastrean el progreso. Se habilita solo después de que un archivo válido haya sido preparado por **Select Installer...**. |

### Preparación de una actualización de firmware (v0.9.3 y posteriores)

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from \<filename\>...* mientras el preparador extrae la carga.
4. Cuando se complete la preparación, la etiqueta de estado confirma la disponibilidad y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

---

## Pestaña Network

Muestra las direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura reportadas por la radio. |

### Controles

| Control | Tipo | Defecto | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | — | Rechaza conexiones de pares no RFC 1918. |
| **Network MTU:** | Cuadro de giro | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango: 576–9000. Se guarda en `NetworkMtu`. El defecto 1450 es seguro para la mayoría de túneles VPN/SD-WAN. |
| **DHCP / Static** | Botón de alternancia | — | Alterna entre direccionamiento IP DHCP y estático. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — | Campos de configuración IP estática. Activos solo cuando se selecciona modo Static. |
| **Apply** | Botón de presión | — | Envía la configuración de red actual a la radio. |

---

## Pestaña GPS

Muestra la presencia de GPS y datos de posición en vivo cuando un receptor GPS está conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos de GPS en vivo | Muestra latitud, longitud, altitud, hora y cantidad de satélites. Se actualiza en tiempo real. |

---

## Pestaña TX

Controla los tiempos de TX, bloqueos, límites de potencia, modo de sintonización y comportamiento de seguimiento de slice.

| Control | Tipo | Defecto | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Cuadro de giro | — | Tiempos de espera y retardo de TX en milisegundos. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de bloqueo RCA y accesorios. |
| **Max Power:** | Cuadro de giro | — | Límite de potencia TX a nivel de radio (0–100%). |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en la pantalla waterfall. |
| **TX Follows Active Slice** | Botón de presión | False | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se guarda en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón de presión | False | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se guarda en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón de presión | — | Abre el diálogo dedicado de potencia y sintonización por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores por defecto de RTTY.

### Manipulador Iambic

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** muestre **Enabled**. Si muestra **Disabled**, haga clic en él una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iambic Curtis.

| Control | Tipo | Defecto | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel del micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Botón de presión (par mutuamente excluyente) | A | Selecciona el modo iambic Curtis A o B tanto para el manipulador de hardware de la radio como para el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. Añadido en v0.9.1. |
| **Swap:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Sideband:** | Cuadro combinado | — | Selecciona la banda lateral de tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita la pulsación de macros CWX. |
| **Decode:** | Botón de alternancia | True | Habilita la superposición de decodificación CW en el panadapter. Se guarda en `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Cuadro de giro | — | Frecuencia de marca RTTY por defecto. |

**Modo A frente a Modo B:** El Modo A (Curtis A) libera el último elemento cuando ambos pulsadores se sueltan a mitad de presión. El Modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador de software local refleja el modo que seleccione, proporcionando respuesta de sidetone inferior a 5 ms independientemente de la latencia de la red.

---

## Pestaña RX

Proporciona calibración de offset de frecuencia GPSDO y selección de fuente de referencia de 10 MHz.

En v0.9.2.1, los controles de calibración se volvieron disponibles independientemente de si un GPSDO está instalado. La etiqueta de estado en la parte superior del grupo lee:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Uso de calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - La etiqueta de estado reporta el progreso (Starting… y estados posteriores).
   - AetherSDR reinicia el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando se completa la calibración, el botón se rehabilita y la etiqueta de estado se actualiza con el resultado.
6. Si **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Defecto | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de giro | — | Frecuencia utilizada para calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón de presión | — | Reinicia el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y se etiqueta como Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Cuadro de giro | — | Offset de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra al lado y se actualiza en vivo. |

---

## Pestaña Audio

Configura las salidas de audio de la radio, dispositivos de audio de PC, grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Defecto | Comportamiento |
|---|---|---|---|
| **Line Out:** | Deslizador | — | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón de presión | — | Silencia la salida de línea. |
| **Headphone:** | Deslizador | — | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón de presión | — | Silencia la salida de auriculares. |
| **Front Speaker: / Mute** | Botón de presión | — | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón de presión | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Se guarda en `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | False | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de audio/flujos TCP/UDP durante inactividad. Se guarda en `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | — | Selecciona los dispositivos de entrada y salida de audio del host. |
| **Audio Boost:** | Botón de alternancia | — | Habilita ganancia adicional en la ruta de audio del cliente. Se guarda en `AudioBoost`. |
| **Audio Buffer:** | Campo de texto | 200 | Tamaño del búfer de audio en milisegundos para compensación de jitter de VPN/SmartLink. Rango: 50–1000 ms. Se guarda en `AudioBufferMs`. |
| **Recording: Radio Side / Client Side** | Botón de presión | Radio Side | Selecciona grabación del lado de la radio o del lado del cliente. Se guarda en `RecordingMode`. |
| **Save to:** | Campo de texto | — | Carpeta para grabaciones guardadas (solo lado del cliente). Por defecto Documents/AetherSDR/Recordings. Se guarda en `QsoRecordingDir`. |
| **...** | Botón de presión | — | Abre un navegador de carpetas para el directorio de grabación. |
| **Auto-record on TX** | Casilla de verificación | False | Registra automáticamente durante la transmisión. Se guarda en `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Cuadro de giro | 120 | Segundos de silencio antes de que se detenga la grabación. Rango: 10–3600 s. Se guarda en `QsoRecording
