# Diálogo Radio Setup

Esta página describe todos los controles del diálogo **Radio Setup**
(`Settings > Radio Setup...`). El diálogo tiene una banda de pestañas en la parte superior; cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación del equipo, la información de licencia y los controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Model** | Modelo del equipo (solo lectura). |
| **HW Version** | Cadena de versión de hardware (solo lectura). |
| **Region** | Región regulatoria; predeterminado USA (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado de habilitación de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio con licencia (solo lectura). |
| **License Info** | Muestra la suscripción, fecha de vencimiento, ID de radio y versión con licencia del equipo (solo lectura). |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo descriptivo del equipo. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Se almacena en `StationName`. Si se deja vacío, toma el nombre de host del sistema operativo. Se envía al equipo como `client station <name>`. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita el encendido/activación remota. |
| **Check for Update** | Consulta si hay actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado muestra: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta muestra: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador SmartSDR `.msi` (formato WiX de FlexRadio v4.2+), un instalador autoextraíble `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs. encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` sin herramientas externas. Anteriormente denominado **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Inicia la carga del firmware. Una barra de progreso y una etiqueta de estado muestran el avance. Se habilita únicamente después de que **Select Installer...** haya preparado un archivo válido. |

### Preparación de una actualización de firmware (v0.9.3 y posteriores)

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from \<filename\>...* mientras el preparador extrae la carga útil.
4. Cuando la preparación finaliza, la etiqueta de estado confirma que todo está listo y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware al equipo.

---

## Pestaña Network

Muestra las direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura reportadas por el equipo. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | — | Rechaza conexiones de pares que no sean RFC1918. |
| **Network MTU:** | Spinbox | 1450 | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango: 576–9000 bytes. Se almacena en `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | Alterna entre los modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — | Campos de configuración de IP estática. |
| **Apply** | Botón | — | Envía la configuración de red al equipo. |

---

## Pestaña GPS

Muestra la presencia del GPS y los datos de posición en tiempo real cuando hay un receptor GPS conectado al equipo.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en tiempo real | Muestra latitud, longitud, altitud, hora y número de satélites. Se actualiza en tiempo real. |

---

## Pestaña TX

Controla los tiempos de TX, los enclavamientos, los límites de potencia, el modo de sintonía y el comportamiento de seguimiento de slice.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Spinbox | — | Tiempos de retención y retardo de TX en milisegundos. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y accesorio. |
| **Max Power:** | Spinbox | — | Límite de potencia TX a nivel del equipo (0–100%). |
| **Tune Mode:** | Cuadro combinado | — | Selecciona el comportamiento del botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal TX en el display de cascada (waterfall). |
| **TX Follows Active Slice** | Botón | False | El TX sigue al slice activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón | False | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. Se almacena en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón | — | Abre el diálogo dedicado de potencia y sintonía por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Manipulador iámbico

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Verifique que **Iambic:** muestre **Enabled**. Si muestra **Disabled**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iámbico Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante la recepción. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iámbico del equipo. |
| **Iambic Mode: A / B** | Botón (par mutuamente exclusivo) | A | Selecciona el modo iámbico Curtis A o B tanto para el manipulador de hardware del equipo como para el manipulador por software local. Modo A = Curtis A; Modo B = Curtis B. Añadido en v0.9.1. |
| **Swap:** | Botón de alternancia | — | Intercambia el dit y el dah. |
| **Sideband:** | Cuadro combinado | — | Selecciona la banda lateral del tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita el cierre por macros CWX. |
| **Decode:** | Botón de alternancia | True | Habilita la superposición de decodificación CW en el panadapter. Se almacena en `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | — | Frecuencia de marca RTTY predeterminada. |

**Modo A vs. Modo B:** El modo A (Curtis A) suelta el último elemento cuando ambas paletas se sueltan a mitad de una secuencia. El modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador por software local replica el modo seleccionado y proporciona una respuesta de sidetone inferior a 5 ms, independiente de la latencia de red.

---

## Pestaña RX

Proporciona calibración de desplazamiento de frecuencia GPSDO y selección de la fuente de referencia de 10 MHz.

En v0.9.2.1, los controles de calibración quedaron disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo muestra:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia de precisión conocida en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en curso.
   - La etiqueta de estado informa el progreso (Starting… y estados subsiguientes).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración finaliza, el botón se vuelve a habilitar y la etiqueta de estado se actualiza con el resultado.
6. Si **Cal Frequency (MHz):** está vacío al hacer clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | — | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón | — | Restablece el error de frecuencia a 0 ppb y luego inicia el barrido de calibración. Se deshabilita y se etiqueta como Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Spinbox | — | Desplazamiento de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto a este control y se actualiza en tiempo real. |

---

## Pestaña Audio

Configura las salidas de audio del equipo, los dispositivos de audio del PC, la grabación y el contenedor NVIDIA BNR.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Line Out:** | Control deslizante | — | Ganancia de la salida de línea. |
| **Mute (Line Out)** | Botón | — | Silencia la salida de línea. |
| **Headphone:** | Control deslizante | — | Ganancia de los auriculares. |
| **Mute (Headphone)** | Botón | — | Silencia la salida de auriculares. |
| **Front Speaker: / Mute** | Botón | — | Silencia el altavoz frontal (depende del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón | Auto | Selecciona el códec de audio para conexiones SmartLink/LAN. Se almacena en `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación | False | Mantiene el sistema operativo activo mientras el equipo está conectado, para evitar interrupciones en los flujos de audio/TCP/UDP durante períodos de inactividad. Se almacena en `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | — | Selecciona los dispositivos de entrada y salida de audio del sistema. |
| **Audio Boost:** | Botón de alternancia | — | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en `AudioBoost`. |
| **Audio Buffer:** | Campo de texto | 200 | Tamaño del búfer de audio en milisegundos para la compensación de jitter en VPN/SmartLink. Rango: 50–1000 ms. Se almacena en `AudioBufferMs`. |
| **Recording: Radio Side / Client Side** | Botón | Radio Side | Selecciona la grabación en el lado del equipo o en el lado del cliente. Se almacena en `RecordingMode`. |
| **Save to:** | Campo de texto | — | Carpeta para las grabaciones guardadas (solo modo cliente). Predeterminado: Documents/AetherSDR/Recordings. Se almacena en `QsoRecordingDir`. |
| **...** | Botón | — | Abre un explorador de carpetas para seleccionar el directorio de grabaciones. |
| **Auto-record on TX** | Casilla de verificación | False | Graba automáticamente durante la transmisión. Se almacena en `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Spinbox | 120 | Segundos de silencio antes de que se detenga la grabación. Rango: 10–3600 s. Se almacena en `QsoRecordingIdleTimeout`. |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Botón |
