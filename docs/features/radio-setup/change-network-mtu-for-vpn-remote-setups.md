# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, teléfono/CW, RX, audio, filtros, XVTR, cables USB, periféricos, serie/FlexControl y temas.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

## Comportamiento general del diálogo

- El diálogo es una ventana sin marco de forma predeterminada cuando la configuración `FramelessWindow` es `True`. Puede redimensionarlo arrastrando cualquier borde.
- La geometría del diálogo se conserva entre sesiones.
- Los cambios realizados en algunas pestañas se aplican inmediatamente; otros requieren hacer clic en un botón Apply o Connect.
- Si borra un campo IP en la pestaña **Peripherals** y cierra el diálogo sin hacer clic en Connect/Disconnect, la IP manual y el puerto guardados se eliminan automáticamente y el dispositivo se desconecta.

## Radio (pestaña)

La pestaña Radio muestra información del radio, identificación, información de licencia y controles de actualización de firmware.

| Control | Descripción |
|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). |
| **Region** | Región regulatoria del radio (solo lectura). |
| **HW Version** | Cadena de versión de hardware (solo lectura). |
| **Remote On** | Habilita el encendido remoto / activación remota. |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). |
| **Model** | Modelo del radio (solo lectura). |
| **Nickname** | Apodo del radio fácil de usar. |
| **Callsign** | Indicativo de la estación. |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía al radio como "cliente estación \<nombre\>". |
| **License Info** | Muestra los detalles de la licencia del radio: suscripción, vencimiento, ID de radio y versión licenciada. |
| **Check for Update** | Consulta si hay actualizaciones de firmware. |
| **Select Installer...** | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. Consulte [Actualización de firmware](#actualización-de-firmware-pestaña-radio) a continuación. |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. |

### Actualización de firmware (pestaña Radio)

AetherSDR no descarga firmware automáticamente cuando se detecta una actualización. Descargue usted mismo el instalador de SmartSDR desde flexradio.com y luego prepárelo manualmente.

#### Preparación de una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, un mensaje de estado le indica la versión disponible y le indica que descargue el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — instalador WiX (FlexRadio SmartSDR v4.2 y posteriores)
   - `.exe` — instalador autoextraíble antiguo
   - `.ssdr` — archivo de firmware preextraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
   - AetherSDR lee el archivo, detecta automáticamente su formato a partir de los primeros 8 bytes y extrae la carga útil `.ssdr` si es necesario. Una etiqueta de estado muestra el progreso.
6. Cuando la preparación se complete y el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso rastrea la carga.
   - No cierre el diálogo ni se desconecte del radio mientras la carga está en progreso.

#### Mensajes de estado del firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com, luego haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se requiere acción. |
| Preparing firmware from *filename*... | El preparador está leyendo y extrayendo el archivo seleccionado. |
| (texto de error en rojo) | La preparación o carga falló. Verifique que el archivo sea un instalador o archivo de firmware de SmartSDR válido e intente nuevamente. |

#### Notas

- El botón **Select Installer...** se etiquetaba **Browse .ssdr...** en versiones anteriores a la v0.9.3.
- La preparación se ejecuta completamente en el cliente; no se requieren herramientas externas para desempaquetar instaladores `.msi` o `.exe`.

## Network (pestaña)

La pestaña Network muestra la información de red del radio y permite configurar opciones de red avanzadas.

| Control | Descripción | Predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918. | — |
| **Network MTU:** | Establece el tamaño máximo de paquete VITA-49 UDP saliente en bytes. Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Envía la configuración de red al radio. | — |

### Cambiar la MTU de red

La configuración de MTU de red controla el tamaño máximo de paquete que el radio envía a través de la red. Reducirla evita la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce la MTU de ruta disponible.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de giro **Network MTU:**.
4. Establezca el valor para que coincida con la MTU de su ruta de red.
5. Haga clic en **Apply** para enviar la nueva MTU al radio.

## GPS (pestaña)

La pestaña GPS muestra la presencia de GPS y la latitud, longitud, altitud, hora e información de satélites en vivo.

| Control | Descripción |
|---|---|
| **GPS status** | Muestra la presencia de GPS y los datos de posición en vivo. |

## TX (pestaña)

La pestaña TX controla los temporizadores de TX, los enclavamientos, la potencia máxima, el modo de sintonía, la visualización en el waterfall, el seguimiento de slice/TX y la configuración de banda de TX.

| Control | Descripción | Predeterminado |
|---|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | — |
| **Timings (in ms)** | Temporizadores de retención/retardo de TX. | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y Accessory. | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0–100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |
| **TX Follows Active Slice** | TX sigue la slice activa. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación de Split. | False |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |

## Phone/CW (pestaña)

La pestaña Phone/CW configura los valores predeterminados del micrófono, el manipulador CW y RTTY.

| Control | Descripción | Predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en el radio. | Enabled |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para el radio como para el manipulador local por software. Par mutuamente excluyente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW (LSB o USB). | — |
| **CWX:** | Habilita el keying de macros CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. | True |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. | — |

## RX (pestaña)

La pestaña RX proporciona calibración de desviación de frecuencia GPSDO y selección de fuente de referencia de 10 MHz. Todos los controles de calibración están siempre visibles, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

| Control | Descripción |
|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. |
| **Start** | Inicia el barrido de calibración de frecuencia. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido. |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en ppb. |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. Consulte la tabla a continuación. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** se completa dinámicamente. Solo aparecen las fuentes compatibles con el hardware conectado. Una etiqueta junto al cuadro combinado muestra la fuente resuelta y el estado de bloqueo.

#### Opciones del cuadro combinado

| Opción | Cuándo se muestra |
|---|---|
| Auto | Siempre. |
| TCXO | Cuando se ha recibido el estado del oscilador, o cuando el radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Cuando el radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Cuando se ha recibido el estado del oscilador, o cuando el radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

#### Comportamiento de la etiqueta de estado

- Cuando se selecciona **Auto** y el radio ha elegido una fuente específica, la etiqueta muestra `Auto -> <fuente>`.
- Cuando se selecciona una fuente específica y el radio está usando una diferente, la etiqueta muestra `<seleccionada> -> <activa>`.
- Cuando la configuración y el estado coinciden, solo se muestra la fuente activa.
- El estado de bloqueo se añade: `Locked` (verde) o `Unlocked` (rojo).
- Si **External 10 MHz** está seleccionado o activo pero no se detecta ninguna referencia externa, la etiqueta añade `(not detected)`.
- Mientras el radio aún no ha informado el estado del oscilador, la etiqueta muestra `Waiting for oscillator status` en gris.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido.
   - El radio primero restablece el error de frecuencia a 0 ppb, luego comienza la secuencia de calibración PLL.
5. Cuando la calibración se completa, el botón se reactiva y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer la desviación manualmente, ingrese un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

#### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido se ha enviado al radio. |
| Busy | La calibración PLL está en progreso. |
| Enter cal frequency | El campo Cal Frequency estaba vacío cuando se hizo clic en Start. |

## Audio (pestaña)

La pestaña Audio configura las salidas de audio del radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Descripción | Predeterminado |
|---|---|---|
| **Line Out:** | Control deslizante de ganancia de salida de línea. | — |
| **Mute (Line Out)** | Silencia la salida de línea. | — |
| **Headphone:** | Control deslizante de ganancia de auriculares. | — |
| **Mute (Headphone)** | Silencia los auriculares. | — |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | — |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`. | Auto |
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras el radio está conectado para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena en AppSettings como `InhibitSleepWhileConnected`. | False |
| **PC Audio Devices: Input: / Output:** | Selecciona los dispositivos de audio de entrada/salida del host. | — |
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena en AppSettings como `AudioBoost`. | — |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para jitter de VPN/SmartLink. Rango 50–1000 ms. Se almacena en AppSettings como `AudioBufferMs`. | 200 |
| **Recording: Radio Side / Client Side** | Selecciona la grabación del lado del radio o del lado del cliente. Se almacena en AppSettings como `RecordingMode`. | Radio Side |
| **Save to:** | Carpeta para grabaciones guardadas (solo del lado del cliente). Se almacena en AppSettings como `QsoRecordingDir`. Por defecto en Documentos/AetherSDR/Recordings. | — |
| **...** | Navega para buscar la carpeta de grabaciones. | — |
| **Auto-record on TX** | Graba automáticamente mientras transmite. Se almacena en AppSettings como `QsoRecordingAutoRecord`. | False |
| **Idle timeout:** | Segundos de silencio
