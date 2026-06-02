# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Se abre desde `Settings > Radio Setup...` y requiere una conexión activa con la radio.

## Diseño del Diálogo

La ventana del diálogo utiliza el marco de diálogo persistente, guardando y restaurando su geometría automáticamente entre sesiones. El área de contenido principal contiene una interfaz de pestañas con las siguientes pestañas:

- **Radio** — Información de la radio, identificación, información de licencia y actualización de firmware
- **Network** — Información de red de la radio y opciones de red avanzadas
- **GPS** — Presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites
- **TX** — Temporizaciones de transmisión, enclavamientos, potencia máxima, modo de sintonía, waterfall, seguimiento slice/TX y acceso directo a configuración de banda de TX
- **Phone/CW** — Micrófono, manipulador CW, valores predeterminados RTTY
- **RX** — Calibración de desviación de frecuencia GPSDO y fuente de referencia de 10 MHz
- **Antennas** — Configuración de nombres de antenas
- **Filters** — Opciones de filtro de baja latencia / nítido por ancho de banda
- **XVTR** — Configuración por transverter
- **USB Cables** — Asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT
- **Peripherals** — Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius)
- **APD** — Configuración de muestreador de predistorsión adaptativa externa (solo FLEX-8x00 con SmartSDR 4.2.18+)
- **Themes** — Personalización de la interfaz de usuario, incluidos colores de slice
- **SmartLink** — Gestión de certificados TLS fijados de SmartLink
- **Serial** — Configuración del puerto serie FlexControl y mapeo de paletas/botones

La geometría del diálogo (posición y tamaño) se guarda automáticamente al cerrar el diálogo y se restaura al abrirlo nuevamente. El diálogo hereda de `PersistentDialog`, que maneja la persistencia de la geometría bajo la clave `RadioSetupDialogGeometry`.

---

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, detalles de licencia y controles de actualización de firmware.

### Información de la Radio

Los siguientes indicadores son de solo lectura y muestran información recuperada de la radio conectada:

| Control | Lo que muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región regulatoria de la radio (ej., USA) |
| **HW Version** | Cadena de versión del hardware |
| **Model** | Modelo de la radio |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de vencimiento, ID de la radio y versión licenciada |

Cada campo de solo lectura tiene un botón de copia (icono de portapapeles) que aparece al pasar el cursor o al enfocar. Haga clic en el botón de copia para copiar el valor de ese campo al portapapeles del sistema. Una breve ventana emergente confirma la acción de copia.

### Campos de Configuración del Usuario

| Control | Lo que hace | Clave de Configuración |
|---|---|---|
| **Nickname** | Apodo amigable de la radio | — |
| **Callsign** | Indicativo de la estación | — |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto, usa el nombre de host del SO si está vacío. | `StationName` |
| **Remote On** | Habilita el encendido remoto / remote-on | — |

### Actualización de Firmware

La pestaña **Radio** incluye controles de actualización de firmware. Para más detalles, consulte la sección [Actualización de Firmware](#firmware-update-radio-tab) a continuación.

---

## Pestaña Network

La pestaña **Network** muestra información de red y permite configurar los ajustes de red de la radio.

### Información de Red

Los siguientes indicadores son de solo lectura:

| Control | Lo que muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura |

### Configuración de Red

| Control | Lo que hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **DHCP / Static** | Cambia entre modos DHCP e IP estática | — | — | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática | — | — | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918 | — | — | — |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 de salida en bytes | 1450 | 576-9000 bytes | `NetworkMtu` |
| **Apply** | Envía la configuración de red a la radio | — | — | — |

> **Nota:** El MTU predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Esta configuración se almacena en AppSettings.

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo cuando hay un receptor GPS instalado.

| Control | Lo que muestra |
|---|---|
| **GPS** | Información en vivo de latitud/longitud/altitud/hora/satélites |

---

## Pestaña TX

La pestaña **TX** configura las temporizaciones de transmisión, enclavamientos, potencia, modo de sintonía y comportamiento de seguimiento slice/TX.

### Configuración de Banda de TX

| Control | Lo que hace |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda |

### Configuración de TX

| Control | Lo que hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **Timings** | Temporizaciones de retención/retardo de TX. Incluye campos ACC TX, TX Delay, RCA TX1 y Timeout. | — | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y accesorio | — | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | — | 0-100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall | — | — |

### Campos de Temporización

La sección **Timings** incluye cuatro campos:

| Control | Lo que hace | Notas |
|---|---|---|
| **ACC TX:** | Retardo de transmisión ACC en milisegundos | — |
| **TX Delay:** | Retardo de transmisión en milisegundos | — |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena internamente este valor en milisegundos. | Ingrese el valor en segundos; el diálogo lo convierte a milisegundos antes de enviarlo a la radio. |

> **Nota:** El campo Timeout anteriormente mostraba minutos, pero ahora muestra segundos para una resolución más fina en configuraciones de TOT de ciclo corto.

### Seguimiento Slice/TX

| Control | Lo que hace | Valor Predeterminado | Clave de Configuración |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación en Split. | False | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | False | `ActiveFollowsTxSlice` |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Lo que hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX | — | — | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio | — | Enabled / Disabled | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. | A | A / B | — |
| **Swap:** | Intercambia dit/dah | — | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW | — | LSB / USB | — |
| **CWX:** | Habilita el keying de macros CWX | — | — | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter | True | — | `CwDecodeOverlay` |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada | — | — | — |

> **Nota:** Los botones Mode A y Mode B están disponibles junto al conmutador Iambic Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el manipulador iámbico local por software (IambicKeyer), que refleja el estado iámbico de la radio para un tono de verificación inferior a 5 ms.

---

## Pestaña RX

La pestaña **RX** proporciona calibración manual de desviación de frecuencia y selección de fuente de referencia de 10 MHz.

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Controles de Calibración

| Control | Lo que hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<value>` al terminar de editar el campo. | — |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración se está ejecutando. Una etiqueta de estado junto al botón informa el progreso. | — |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en partes por mil millones. | — |

### Fuente de Referencia de 10 MHz

| Control | Lo que hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/External). El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. | Auto | Auto / TCXO / GPSDO / External |

La etiqueta de estado junto a **10 MHz Reference Source:** muestra información más completa. El texto y el color de la etiqueta se actualizan en vivo a medida que la radio informa cambios en el estado del oscilador.

**Formato del texto de la etiqueta:**

| Condición | Texto de ejemplo |
|---|---|
| Modo Auto resolviendo a una fuente | `Auto -> GPSDO Locked` |
| Configuración anulada por la radio | `TCXO -> GPSDO Locked` |
| La fuente coincide con la configuración | `GPSDO Locked` |
| External seleccionado pero no detectado | `External 10 MHz Unlocked (not detected)` |
| Esperando el primer informe de estado | `Waiting for oscillator status` |

**Color de la etiqueta:**

| Estado | Color |
|---|---|
| Locked | Verde |
| Unlocked | Rojo |
| Aún no se ha recibido estado | Gris/azul |

El cuadro combinado **10 MHz Reference Source:** se rellena dinámicamente según el hardware que la radio informa como presente, la configuración actual y el estado activo del oscilador. La entrada **External** está etiquetada como **External 10 MHz**. Si la radio envía el valor `ext`, se trata como equivalente a `external`.

### Iniciar una Calibración

1. Haga clic en la pestaña **RX** en Configuración de la Radio.
2. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para ver el progreso y el resultado.
4. Cuando la calibración se complete, el botón se volverá a habilitar.

---

## Pestaña Antennas

La pestaña **Antennas** le permite configurar nombres amigables para cada puerto de antena en la radio, reemplazando las etiquetas de puerto predeterminadas (ANT1, ANT2, XVTA, XVTB, etc.) con identificadores personalizados que aparecen en toda la interfaz de AetherSDR.

| Control | Lo que hace |
|---|---|
| **Antenna name fields** | Un campo de texto por puerto de antena. Ingrese un nombre personalizado (ej., "HF Vertical", "6M Yagi", "160M Loop"). Los nombres se envían a la radio y se conservan en la configuración de la radio. |

**Para establecer un nombre de antena:**

1. Haga clic en la pestaña **Antennas** en Configuración de la Radio.
2. Para cada puerto de antena, escriba el nombre deseado en el campo de texto correspondiente.
3. Presione Enter o tabulador para pasar al siguiente campo y enviar el nombre a la radio.

---

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos del PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Lo que hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea | — | — | — |
| **Mute (Line Out)** | Silencia la salida de línea | — | — | — |
| **Headphone:** | Deslizador de ganancia de auriculares | — | — | — |
| **Mute (Headphone)** | Silencia los auriculares | — | — | — |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo) | — | — | — |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN | Auto | — | `AudioCompression` |
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada para evitar cortes en el flujo de audio/TCP/UDP durante la inactividad | False | — | `InhibitSleepWhileConnected` |
| **PC Audio Devices: Input: / Output:** | Selecciona los dispositivos de audio de entrada/salida del host | — | — | — |
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente | — | — | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para compensar la fluctuación de VPN/SmartLink | 200 | 50-1000 ms | `AudioBufferMs` |
| **Recording: Radio Side / Client Side** | Selecciona la grabación del lado de la radio o del lado del cliente | Radio Side | Radio Side / Client Side | `RecordingMode` |
| **Save to:** | Carpeta para grabaciones guardadas (solo lado del cliente) | Documents/AetherSDR/Recordings | — | `QsoRecordingDir` |
| **...** | Navega para seleccionar la carpeta de grabaciones | — | — | — |
| **Auto-record on TX** | Graba automáticamente al transmitir | — | — | — |

(Continuará con el resto de la pestaña Audio y pestañas subs
