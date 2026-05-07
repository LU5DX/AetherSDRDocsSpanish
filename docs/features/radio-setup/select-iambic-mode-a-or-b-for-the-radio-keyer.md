# Diálogo de configuración de la radio

Esta página describe todos los controles del diálogo **Radio Setup**
(`Settings > Radio Setup...`). El diálogo tiene una barra de pestañas en la parte superior;
cada sección a continuación cubre una pestaña.

---

## Pestaña Radio

Muestra la identificación de la radio, la información de licencia y los controles de actualización de firmware.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Model** | Modelo de la radio (solo lectura). |
| **HW Version** | Cadena de versión del hardware (solo lectura). |
| **Region** | Región regulatoria; predeterminado USA (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado de habilitación de multiFLEX (solo lectura). |
| **Options** | Muestra las opciones de radio con licencia (solo lectura). |
| **License Info** | Muestra la suscripción, la fecha de vencimiento, el ID de la radio y la versión con licencia de la radio (solo lectura). |

### Campos editables

| Control | Tipo | Comportamiento |
|---|---|---|
| **Nickname** | Campo de texto | Apodo descriptivo de la radio. |
| **Callsign** | Campo de texto | Indicativo de la estación. |
| **Station Name** | Campo de texto | Identifica a este cliente de AetherSDR ante otras estaciones multiFLEX. Se almacena en `StationName`. Si se deja vacío, usa por defecto el nombre del host del sistema operativo. Se envía a la radio como `client station <nombre>`. |

### Botones

| Control | Comportamiento |
|---|---|
| **Remote On** | Habilita el encendido remoto. |
| **Check for Update** | Consulta si hay actualizaciones de firmware disponibles. Cuando se encuentra una actualización, la etiqueta de estado dice: *Update available: vX.Y.Z — Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.* Cuando el firmware está actualizado, la etiqueta dice: *Firmware is up to date (vX.Y.Z).* |
| **Select Installer...** | Abre un selector de archivos. Acepta un instalador `.msi` de SmartSDR (formato WiX de FlexRadio v4.2+), un instalador autoejecutable `.exe` (versiones anteriores) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (código mágico OLE/MSI vs. encabezado MZ de PE/COFF) y extrae el contenido `.ssdr` sin herramientas externas. Anteriormente se llamaba **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Inicia la carga del firmware. Una barra de progreso y una etiqueta de estado muestran el avance. Se habilita solo después de que **Select Installer...** haya preparado un archivo válido. |

### Preparación de una actualización de firmware (v0.9.3 y posteriores)

1. Haga clic en **Check for Update**.
2. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
3. Haga clic en **Select Installer...** y seleccione el archivo `.msi`, `.exe` o `.ssdr` descargado.
   - La etiqueta de estado muestra *Preparing firmware from \<nombrearchivo\>...* mientras el preparador extrae el contenido.
4. Cuando la preparación se completa, la etiqueta de estado confirma que está listo y **Upload Firmware** se activa.
5. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

---

## Pestaña Network

Muestra las direcciones de red y permite ajustar la configuración de red.

### Indicadores

| Indicador | Comportamiento |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura informadas por la radio. |

### Controles

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enforce Private IP Connections:** | Botón de alternancia | — | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spinbox | 1450 | Establece el tamaño máximo de paquete VITA-49 UDP saliente en bytes. Rango: 576–9000 bytes. Se almacena en `NetworkMtu`. |
| **DHCP / Static** | Botón de alternancia | — | Alterna entre los modos DHCP e IP estática. |
| **IP Address: / Mask: / Gateway:** | Campos de texto | — | Campos de configuración de IP estática. |
| **Apply** | Botón pulsador | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

Muestra la presencia del GPS y los datos de posición en vivo cuando hay un receptor GPS conectado a la radio.

| Indicador | Comportamiento |
|---|---|
| Datos GPS en vivo | Muestra latitud, longitud, altitud, hora y cantidad de satélites. Se actualiza en tiempo real. |

---

## Pestaña TX

Controla los tiempos de TX, los enclavamientos, los límites de potencia, el modo de sintonía y el comportamiento de seguimiento de slice.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Timings (in ms)** | Spinbox | — | Tiempos de espera y retardo de TX en milisegundos. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | — | Habilita las entradas de enclavamiento RCA y de accesorio. |
| **Max Power:** | Spinbox | — | Límite de potencia de TX a nivel de radio (0–100%). |
| **Tune Mode:** | Cuadro combinado | — | Selecciona cómo se comporta el botón Tune. |
| **Show TX in Waterfall:** | Botón de alternancia | — | Dibuja la señal de TX en la visualización del waterfall. |
| **TX Follows Active Slice** | Botón pulsador | Falso | TX sigue la slice activa. Es mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante una operación de Split. Se almacena en `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | Botón pulsador | Falso | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. Se almacena en `ActiveFollowsTxSlice`. |
| **TX Band Settings** | Botón pulsador | — | Abre el diálogo dedicado de potencia y sintonía por banda. |

---

## Pestaña Phone/CW

Configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Manipulador iambic

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** dice **Enabled**. Si dice **Disabled**, haga clic una vez para habilitar el manipulador.
4. Haga clic en **A** o **B** para seleccionar el modo iambic Curtis.

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | — | Muestra el medidor de nivel de micrófono durante RX. |
| **Iambic:** | Botón de alternancia | — | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Botón pulsador (par mutuamente excluyente) | A | Selecciona el modo iambic Curtis A o B tanto para el manipulador de hardware de la radio como para el manipulador de software local. Modo A = Curtis A; Modo B = Curtis B. Añadido en v0.9.1. |
| **Swap:** | Botón de alternancia | — | Intercambia dit y dah. |
| **Sideband:** | Cuadro combinado | — | Selecciona la banda lateral del tono CW (LSB o USB). |
| **CWX:** | Botón de alternancia | — | Habilita el accionamiento de macros CWX. |
| **Decode:** | Botón de alternancia | Verdadero | Habilita la superposición de decodificación CW en el panadapter. Se almacena en `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | — | Frecuencia de marca RTTY predeterminada. |

**Modo A vs. Modo B:** El modo A (Curtis A) libera el último elemento cuando se sueltan ambas paletas durante un apretón a medio hacer. El modo B (Curtis B) completa el último elemento antes de detenerse. El manipulador de software local refleja el modo que seleccione, proporcionando una respuesta de tono lateral inferior a 5 ms independiente de la latencia de la red.

---

## Pestaña RX

Proporciona la calibración de desviación de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

En v0.9.2.1, los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior del grupo dice:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - La etiqueta de estado informa el progreso (Starting… y estados posteriores).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración se completa, el botón se vuelve a habilitar y la etiqueta de estado se actualiza con el resultado.
6. Si **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | — | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón pulsador | — | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y se etiqueta como Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Spinbox | — | Desviación de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto | Selecciona la fuente de referencia del oscilador. El cuadro combinado se completa dinámicamente según el hardware instalado y el estado actual del oscilador: **Auto**, **TCXO**, **GPSDO** y **External 10 MHz** aparecen solo cuando se detecta el hardware correspondiente o se seleccionó previamente. Cuando **Auto** está activo, la etiqueta de estado muestra la fuente resuelta (por ejemplo, *Auto -> GPSDO*). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, *GPSDO -> TCXO*). El estado de bloqueo (**Locked** / **Unlocked**) se agrega y se actualiza en vivo; si se selecciona **External 10 MHz** pero no se detecta ninguna señal externa, se agrega *(not detected)*. |

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
| **Prevent system sleep while connected** | Casilla de verificación | Falso | Mantiene el sistema operativo activo mientras la radio está conectada para evitar cortes en los flujos de audio/TCP/UDP durante la inactividad. Se almacena en `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | — | Elige los dispositivos de audio de entrada y salida del host. |
| **Audio Boost:** | Botón de alternancia | — | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en `AudioBoost`. |
| **Audio Buffer:** | Campo de texto | 200 | Tamaño del búfer de audio en milisegundos para la compensación de fluctuación en VPN/SmartLink. Rango: 50–1000 ms. Se almacena en `AudioBufferMs`. |
| **Recording: Radio Side / Client Side** | Botón pulsador | Radio Side | Selecciona la grabación del lado de la radio o del lado del cliente. Se almacena en `RecordingMode`. |
| **Save to:** | Campo de texto | — | Carpeta para las grabaciones guardadas (solo del lado del cliente). Por defecto: Documents/AetherSDR/Recordings. Se almacena en `QsoRecordingDir`. |
| **...** | Botón pulsador | — |
