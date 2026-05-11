# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Se abre desde `Settings > Radio Setup...` y requiere una conexión activa con la radio.

## Diseño del Diálogo

La ventana del diálogo tiene una barra de título personalizada en modo sin bordes (habilitado por defecto cuando la configuración `FramelessWindow` es `True`). La barra de título muestra "Radio Setup" e incluye los controles de ventana estándar. El área de contenido principal contiene una interfaz de pestañas con las siguientes pestañas:

- **Radio** — Información de la radio, identificación, información de licencia y actualización de firmware
- **Network** — Información de red de la radio y opciones de red avanzadas
- **GPS** — Presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites
- **TX** — Temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y acceso directo a configuración de banda TX
- **Phone/CW** — Micrófono, manipulador CW, valores predeterminados de RTTY
- **RX** — Calibración de desplazamiento de frecuencia GPSDO y fuente de referencia de 10 MHz
- **Audio** — Salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y contenedor NVIDIA BNR
- **Filters** — Opciones de filtro de baja latencia/nítido por ancho de banda
- **XVTR** — Configuración por transvertidor
- **USB Cables** — Asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT
- **Peripherals** — Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius, ShackSwitch)
- **APD** — Configuración del muestreador de Predistorsión Adaptativa Externa (solo FLEX-8x00 con SmartSDR 4.2.18+)
- **Themes** — Personalización de la interfaz de usuario, incluidos los colores de los slices

La geometría del diálogo (posición y tamaño) se guarda automáticamente al cerrar el diálogo y se restaura la próxima vez que se abre.

## Modo de Ventana Sin Bordes

El diálogo admite el modo sin bordes controlado por la configuración `FramelessWindow` (valor predeterminado `True`). En modo sin bordes, se muestra una barra de título personalizada. Cuando está deshabilitado, se utiliza el marco de ventana del sistema operativo.

- **FramelessWindow** — Clave de configuración: `FramelessWindow`. Valor predeterminado: `True`. Cuando está habilitado, el diálogo usa una barra de título personalizada; cuando está deshabilitado, usa las decoraciones de ventana nativas del sistema operativo.

---

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, detalles de licencia y controles de actualización de firmware.

### Información de la Radio

Los siguientes indicadores son de solo lectura y muestran información recuperada de la radio conectada:

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región regulatoria de la radio (p. ej., USA) |
| **HW Version** | Cadena de versión del hardware |
| **Model** | Modelo de la radio |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de la suscripción, fecha de vencimiento, ID de la radio y versión licenciada |

### Campos de Configuración del Usuario

| Control | Qué hace | Clave de Configuración |
|---|---|---|
| **Nickname** | Apodo amigable de la radio | — |
| **Callsign** | Indicativo de la estación | — |
| **Station Name** | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Si está vacío, se usa el nombre del host del sistema operativo. | `StationName` |
| **Remote On** | Habilita el encendido remoto / activación remota | — |

### Actualización de Firmware

La pestaña **Radio** incluye controles de actualización de firmware. Para más detalles, consulte la sección [Actualización de Firmware](#actualización-de-firmware-pestaña-radio) a continuación.

---

## Pestaña Network

La pestaña **Network** muestra información de red y permite configurar los ajustes de red de la radio.

### Información de Red

Los siguientes indicadores son de solo lectura:

| Control | Qué muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura |

### Configuración de Red

| Control | Qué hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **DHCP / Static** | Cambia entre modos DHCP e IP estática | — | — | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática | — | — | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918 | — | — | — |
| **Network MTU:** | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes | 1450 | 576-9000 bytes | `NetworkMtu` |
| **Apply** | Envía la configuración de red a la radio | — | — | — |

> **Nota:** El MTU predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Esta configuración se almacena en AppSettings.

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo cuando hay un receptor GPS instalado.

| Control | Qué muestra |
|---|---|
| **GPS** | Información en vivo de latitud/longitud/altitud/hora/satélites |

---

## Pestaña TX

La pestaña **TX** configura las temporizaciones de transmisión, enclavamientos, potencia, modo de sintonía y comportamiento de seguimiento slice/TX.

### Configuración de Banda TX

| Control | Qué hace |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda |

### Configuración de TX

| Control | Qué hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **Timings (in ms)** | Temporizaciones de retención/retardo de TX | — | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y de accesorio | — | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | — | 0-100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall | — | — |

### Seguimiento Slice/TX

| Control | Qué hace | Valor Predeterminado | Clave de Configuración |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. | False | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | False | `ActiveFollowsTxSlice` |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Qué hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel del micrófono incluso en RX | — | — | — |
| **Iambic:** | Habilita o deshabilita el manipulador iambic en la radio | — | Enabled / Disabled | — |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A | A / B | — |
| **Swap:** | Intercambia punto/raya | — | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW | — | LSB / USB | — |
| **CWX:** | Habilita la activación de macros CWX | — | — | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter | True | — | `CwDecodeOverlay` |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada | — | — | — |

> **Nota:** En v0.9.1, se agregaron los botones Mode A y Mode B junto al interruptor Iambic Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el manipulador iambic de software local (IambicKeyer) que refleja el estado iambic de la radio para un tono lateral de menos de 5 ms.

---

## Pestaña RX

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia y selección de la fuente de referencia de 10 MHz.

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Controles de Calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<valor>` al terminar de editar el campo. |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en ejecución. Una etiqueta de estado junto al botón informa el progreso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. |

### Fuente de Referencia de 10 MHz

| Control | Qué hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/External). El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. | Auto | Auto / TCXO / GPSDO / External |

La etiqueta de estado de bloqueo junto a **10 MHz Reference Source:** muestra información más detallada. El texto y el color de la etiqueta se actualizan en vivo a medida que la radio informa cambios en el estado del oscilador.

**Formato del texto de la etiqueta:**

| Condición | Ejemplo de texto |
|---|---|
| Modo Auto resolviendo a una fuente | `Auto -> GPSDO Locked` |
| Configuración anulada por la radio | `TCXO -> GPSDO Locked` |
| Fuente coincide con la configuración | `GPSDO Locked` |
| External seleccionado pero no detectado | `External 10 MHz Unlocked (not detected)` |
| Esperando el primer informe de estado | `Waiting for oscillator status` |

**Color de la etiqueta:**

| Estado | Color |
|---|---|
| Locked | Verde |
| Unlocked | Rojo |
| Aún no se ha recibido estado | Gris/azul |

El cuadro combinado **10 MHz Reference Source:** se completa dinámicamente según el hardware que la radio informa como presente, la configuración actual y el estado activo del oscilador. La entrada **External** está etiquetada como **External 10 MHz**. Si la radio envía el valor `ext`, se trata como equivalente a `external`.

### Inicio de una Calibración

1. Haga clic en la pestaña **RX** en Configuración de la Radio.
2. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para ver el progreso y el resultado.
4. Cuando la calibración se complete, el botón se volverá a habilitar.

---

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de Audio de la Radio

| Control | Qué hace |
|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea |
| **Mute (Line Out)** | Silencia la salida de línea |
| **Headphone:** | Deslizador de ganancia de auriculares |
| **Mute (Headphone)** | Silencia los auriculares |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo) |

### Compresión de Audio

| Control | Qué hace | Valor Predeterminado | Clave de Configuración |
|---|---|---|---|
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN | Auto | `AudioCompression` |

### Configuración de Audio del PC

| Control | Qué hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Prevent system sleep while connected** | Mantiene el sistema operativo activo mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad | False | — | `InhibitSleepWhileConnected` |
| **PC Audio Devices: Input: / Output:** | Elige los dispositivos de audio de entrada/salida del host | — | — | — |
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente | — | — | `AudioBoost` |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para compensar la fluctuación de VPN/SmartLink | 200 | 50-1000 ms | `AudioBufferMs` |

### Grabación

La sección **Recording** controla la captura de audio.

| Control | Qué hace | Valor Predeterminado | Clave de Configuración |
|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en la radio o en este PC | Radio Side | `RecordingMode` |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. Valor predeterminado: Documents/AetherSDR/Recordings. | — | `QsoRecordingDir` |
| **...** | Abre un explorador de carpetas para seleccionar la ubicación de guardado | — | — |
| **Auto-record on TX** | Cuando está marcado, la grabación comienza automáticamente en cada transmisión y se detiene después de que expire el tiempo de espera de inactividad | False | `QsoRecordingAutoRecord` |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga después de que finalice la TX | 120 | 10-3600 seg | `QsoRecordingIdleTimeout` |

**Para habilitar la grabación automática en TX:**

1. Haga clic en la pestaña **Audio**.
2. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio.
3. En el campo **Save to:**, escriba la ruta completa a su carpeta de grabaciones, o haga clic en **...** para explorar.
4. Marque la casilla **Auto-record on TX**.
5. Establezca **Idle timeout:** al valor deseado.
6. Cierre el diálogo. Las configuraciones surten efecto de inmediato.

### NVIDIA BNR

| Control | Qué hace |
|---|---|
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. Un punto de estado de color indica Running/Stopped/Unknown. |

---

## Pestaña Filters

La pestaña **Filters** configura opciones de filtro de baja latencia y nítido por ancho de banda.

| Control | Qué hace | Rango |
