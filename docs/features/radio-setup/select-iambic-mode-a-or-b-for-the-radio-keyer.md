# Diálogo Radio Setup

Esta página describe todos los controles en el diálogo **Radio Setup**
(`Settings > Radio Setup...`). El diálogo tiene una barra de pestañas en la parte superior; cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra identificación de radio, información de licencia y controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Model** | Modelo de radio (solo lectura). |
| **HW Version** | Cadena de versión de hardware (solo lectura). |
| **Region** | Región regulatoria; por defecto USA (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado de habilitación de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). |
| **License Info** | Muestra suscripción, vencimiento, ID de radio y versión licenciada de la radio (solo lectura). |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo amigable de la radio. |
| **Callsign** | Campo de texto | Indicativo de estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR con otras estaciones multiFLEX. Almacenado en `StationName`. Por defecto es el nombre de host del SO si se deja vacío. Se envía a la radio como `client station <name>`. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita encendido remoto. |
| **Check for Update** | Consulta actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado lee: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta lee: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador SmartSDR `.msi` (formato FlexRadio v4.2+ WiX), un instalador autoejecutable `.exe` (lanzamientos anteriores), o un archivo firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes (magia OLE/MSI vs. encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` sin herramientas externas. Anteriormente etiquetado como **Browse .ssdr...** (cambió en v0.9.3). |
| **Upload Firmware** | Inicia la carga de firmware. Una barra de progreso y etiqueta de estado rastrean el progreso. Se habilita solo después de que un archivo válido ha sido preparado por **Select Installer...**. |

### Preparar una actualización de firmware (v0.9.3 y posterior)

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from \<filename\>...* mientras el preparador extrae la carga útil.
4. Cuando la preparación se completa, la etiqueta de estado confirma la disponibilidad y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

---

## Pestaña Network

Muestra direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red reportadas por la radio (solo lectura). |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | — | Rechaza pares no RFC1918. |
| **Network MTU:** | Cuadro de número | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango: 576–9000 bytes. Almacenado en `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | Cambia entre modos DHCP e IP estático. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — | Campos de configuración de IP estático. |
| **Apply** | Botón de presión | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

Muestra presencia de GPS y datos de posición en tiempo real cuando un receptor GPS está conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y cantidad de satélites. Se actualiza en tiempo real. |

---

## Pestaña TX

Controla tiempos de TX, enclavamientos, límites de potencia, modo de sintonización y comportamiento de seguimiento de slice.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Cuadro de número | — | Tiempos de retardo y permanencia de TX en milisegundos. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y accesorios. |
| **Max Power:** | Cuadro de número | — | Límite de potencia TX a nivel de radio (0–100%). |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en la visualización de cascada. |
| **TX Follows Active Slice** | Botón de presión | False | TX sigue el slice activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. Almacenado en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón de presión | False | Cambia el slice activo cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. Almacenado en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón de presión | — | Abre el diálogo dedicado de potencia y sintonización por banda. |

---

## Pestaña Phone/CW

Configura micrófono, manipulador CW y valores predeterminados de RTTY.

### Manipulador Iambic

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** lee **Enabled**. Si lee **Disabled**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar modo iambic Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Botón de presión (par mutuamente exclusivo) | A | Selecciona modo iambic Curtis A o B para el manipulador de hardware de la radio y el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. Agregado en v0.9.1. |
| **Swap:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Sideband:** | Cuadro combinado | — | Selecciona banda lateral de tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita tecleado de macros CWX. |
| **Decode:** | Botón de alternancia | True | Habilita la superposición de decodificación CW en el panadapter. Almacenado en `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Cuadro de número | — | Frecuencia de marca RTTY predeterminada. |

**Modo A vs. Modo B:** El modo A (Curtis A) libera el último elemento cuando ambas palancas se liberan a mitad de apriete. El modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador de software local refleja cualquier modo que seleccione, proporcionando respuesta de sidetone inferior a 5 ms independientemente de la latencia de red.

---

## Pestaña RX

Proporciona calibración de compensación de frecuencia GPSDO y selección de fuente de referencia de 10 MHz.

En v0.9.2.1, los controles de calibración pasaron a estar disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo lee:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Usar calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - La etiqueta de estado reporta progreso (Starting… y estados posteriores).
   - AetherSDR reinicia el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando se completa la calibración, el botón se rehabilita y la etiqueta de estado se actualiza con el resultado.
6. Si **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de número | — | Frecuencia utilizada para calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Botón de presión | — | Reinicia el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y se etiqueta como Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Cuadro de número | — | Compensación de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador: Auto, TCXO, GPSDO, o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto a él y se actualiza en vivo. |

---

## Pestaña Audio

Configura salidas de audio de radio, dispositivos de audio del PC, grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Line Out:** | Control deslizante | — | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón de presión | — | Silencia salida de línea. |
| **Headphone:** | Control deslizante | — | Ganancia de audífono. |
| **Mute (Headphone)** | Botón de presión | — | Silencia salida de audífono. |
| **Front Speaker: / Mute** | Botón de presión | — | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón de presión | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Almacenado en `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | False | Mantiene el SO despierto mientras la radio está conectada para evitar interrupciones de audio/TCP/UDP durante inactividad. Almacenado en `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | — | Selecciona los dispositivos de entrada y salida de audio del anfitrión. |
| **Audio Boost:** | Botón de alternancia | — | Habilita ganancia extra en la ruta de audio del cliente. Almacenado en `AudioBoost`. |
| **Audio Buffer:** | Campo de texto | 200 | Tamaño del búfer de audio en milisegundos para compensación de fluctuación de VPN/SmartLink. Rango: 50–1000 ms. Almacenado en `AudioBufferMs`. |
| **Recording: Radio Side / Client Side** | Botón de presión | Radio Side | Selecciona grabación del lado de radio o del lado de cliente. Almacenado en `RecordingMode`. |
| **Save to:** | Campo de texto | — | Carpeta para grabaciones guardadas (solo lado de cliente). Por defecto Documents/AetherSDR/Recordings. Almacenado en `QsoRecordingDir`. |
| **...** | Botón de presión | — | Abre un navegador de carpetas para el directorio de grabación. |
| **Auto-record on TX** | Casilla de verificación | False | Graba automáticamente mientras transmite. Almacenado en `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Cuadro de número | 120 | Segundos de silencio antes de que se detenga la grabación. Rango: 10–3600 s. Almacenado en `QsoRecordingIdleTimeout`. |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Botón de presión | — |
