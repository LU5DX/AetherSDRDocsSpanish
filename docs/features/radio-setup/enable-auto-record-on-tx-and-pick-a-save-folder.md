# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Se abre desde `Settings > Radio Setup...` y requiere una conexión de radio activa.

## Diseño del Diálogo

La ventana del diálogo utiliza el marco de diálogo persistente, guardando y restaurando su geometría automáticamente entre sesiones. El área de contenido principal contiene una interfaz de pestañas con las siguientes pestañas:

- **Radio** — Información de la radio, identificación, información de licencia y actualización de firmware
- **Network** — Información de red de la radio y opciones de red avanzadas
- **GPS** — Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites
- **TX** — Temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y acceso directo a configuración de banda TX
- **Phone/CW** — Micrófono, manipulador CW, valores predeterminados de RTTY
- **RX** — Calibración de desplazamiento de frecuencia GPSDO y fuente de referencia de 10 MHz
- **Antennas** — Configuración de nombres de antenas
- **Filters** — Opciones de filtro de baja latencia / nítido por ancho de banda
- **XVTR** — Configuración por transvertidor
- **USB Cables** — Asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT
- **Peripherals** — Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius, ShackSwitch)
- **APD** — Configuración del muestreador de predistorsión adaptativa externa (solo FLEX-8x00 con SmartSDR 4.2.18+)
- **Themes** — Personalización de la interfaz de usuario, incluidos colores de slices

La geometría del diálogo (posición y tamaño) se guarda automáticamente al cerrar el diálogo y se restaura al abrirlo nuevamente. El diálogo hereda de `PersistentDialog`, que maneja la persistencia de geometría bajo la clave `RadioSetupDialogGeometry`.

---

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, detalles de licencia y controles de actualización de firmware.

### Información de la Radio

Los siguientes indicadores son de solo lectura y muestran información recuperada de la radio conectada:

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región regulatoria de la radio (ej., USA) |
| **HW Version** | Cadena de versión de hardware |
| **Model** | Modelo de la radio |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de vencimiento, ID de radio y versión licenciada |

### Campos de Configuración de Usuario

| Control | Qué hace | Clave de Configuración |
|---|---|---|
| **Nickname** | Apodo de radio fácil de usar | — |
| **Callsign** | Indicativo de la estación | — |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si está vacío. | `StationName` |
| **Remote On** | Habilita el encendido remoto / remote-on | — |

### Actualización de Firmware

La pestaña **Radio** incluye controles de actualización de firmware. Para más detalles, consulte la sección [Actualización de Firmware](#actualizacion-de-firmware-pestaña-radio) a continuación.

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
| **Enforce Private IP Connections:** | Rechaza pares no RFC1918 | — | — | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes | 1450 | 576-9000 bytes | `NetworkMtu` |
| **Apply** | Envía la configuración de red a la radio | — | — | — |

> **Nota:** El MTU predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Este ajuste se almacena en AppSettings.

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo cuando hay un receptor GPS instalado.

| Control | Qué muestra |
|---|---|
| **GPS** | Información en vivo de lat/lon/alt/hora/satélites |

---

## Pestaña TX

La pestaña **TX** configura temporizaciones de transmisión, enclavamientos, potencia, modo de sintonía y comportamiento de seguimiento slice/TX.

### Configuración de Banda TX

| Control | Qué hace |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda |

### Configuración de TX

| Control | Qué hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **Timings** | Temporizaciones de retención/retardo de TX. Incluye campos ACC TX, TX Delay, RCA TX1 y Timeout. | — | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita entradas de enclavamiento RCA y Accessory | — | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | — | 0-100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall | — | — |

### Campos de Temporización

La sección **Timings** incluye cuatro campos:

| Control | Qué hace | Notas |
|---|---|---|
| **ACC TX:** | Retardo de transmisión ACC en milisegundos | — |
| **TX Delay:** | Retardo de transmisión en milisegundos | — |
| **RCA TX1:** | Retardo RCA TX1 en milisegundos | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena internamente este valor en milisegundos. | Ingrese el valor en segundos; el diálogo lo convierte a milisegundos antes de enviarlo a la radio. |

> **Nota:** El campo Timeout anteriormente mostraba minutos, pero ahora muestra segundos para una resolución más fina en configuraciones TOT de ciclo corto.

### Seguimiento Slice/TX

| Control | Qué hace | Valor Predeterminado | Clave de Configuración |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante operación en Split. | Falso | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | Falso | `ActiveFollowsTxSlice` |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Qué hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX | — | — | — |
| **Iambic:** | Habilita o deshabilita el manipulador iambic en la radio | — | Habilitado / Deshabilitado | — |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local de software. Par mutuamente excluyente. | A | A / B | — |
| **Swap:** | Intercambia dit/dah | — | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW | — | LSB / USB | — |
| **CWX:** | Habilita la activación de macros CWX | — | — | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter | Verdadero | — | `CwDecodeOverlay` |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada | — | — | — |

> **Nota:** Los botones Mode A y Mode B están disponibles junto al interruptor Iambic Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el manipulador iambic local de software (IambicKeyer), que refleja el estado iambic de la radio para un tono lateral de menos de 5 ms.

---

## Pestaña RX

La pestaña **RX** proporciona calibración manual del desplazamiento de frecuencia y selección de la fuente de referencia de 10 MHz.

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin un GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Controles de Calibración

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<valor>` cuando termina de editar el campo. | — |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en ejecución. Una etiqueta de estado junto al botón informa el progreso. | — |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. | — |

### Fuente de Referencia de 10 MHz

| Control | Qué hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/External). El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. | Auto | Auto / TCXO / GPSDO / External |

La etiqueta de estado junto a **10 MHz Reference Source:** muestra información más detallada. El texto y color de la etiqueta se actualizan en vivo a medida que la radio informa cambios en el estado del oscilador.

**Formato del texto de la etiqueta:**

| Condición | Texto de ejemplo |
|---|---|
| Modo Auto resolviendo a una fuente | `Auto -> GPSDO Locked` |
| Ajuste anulado por la radio | `TCXO -> GPSDO Locked` |
| Fuente coincide con el ajuste | `GPSDO Locked` |
| External seleccionado pero no detectado | `External 10 MHz Unlocked (not detected)` |
| Esperando el primer informe de estado | `Waiting for oscillator status` |

**Color de la etiqueta:**

| Estado | Color |
|---|---|
| Locked | Verde |
| Unlocked | Rojo |
| Aún no se ha recibido estado | Gris/azul |

El cuadro combinado **10 MHz Reference Source:** se llena dinámicamente según el hardware que la radio informa como presente, el ajuste actual y el estado activo del oscilador. La entrada **External** está etiquetada como **External 10 MHz**. Si la radio envía el valor `ext`, se trata como equivalente a `external`.

### Iniciar una Calibración

1. Haga clic en la pestaña **RX** en Configuración de Radio.
2. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para ver el progreso y el resultado.
4. Cuando la calibración se complete, el botón se volverá a habilitar.

---

## Pestaña Antennas

La pestaña **Antennas** le permite configurar nombres fáciles de usar para cada puerto de antena en la radio, reemplazando las etiquetas de puerto predeterminadas (ANT1, ANT2, XVTA, XVTB, etc.) con identificadores personalizados que aparecen en toda la interfaz de AetherSDR.

| Control | Qué hace |
|---|---|
| **Campos de nombre de antena** | Un campo de texto por puerto de antena. Ingrese un nombre personalizado (ej., "HF Vertical", "6M Yagi", "160M Loop"). Los nombres se envían a la radio y se conservan en la configuración de la radio. |

**Para establecer un nombre de antena:**

1. Haga clic en la pestaña **Antennas** en Configuración de Radio.
2. Para cada puerto de antena, escriba el nombre deseado en el campo de texto correspondiente.
3. Presione Enter o tabule al siguiente campo para confirmar el nombre en la radio.

---

## Pestaña Filters

La pestaña **Filters** configura opciones de filtro de baja latencia y nítido por ancho de banda.

| Control | Qué hace | Rango |
|---|---|---|
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. | 0-3 |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | — |
| **Use Low Latency Filters for Digital Modes** | Fuerza filtros de baja latencia en DIGU/DIGL. | — |

---

## Pestaña XVTR

La pestaña **XVTR** proporciona configuración por transvertidor. Contiene pestañas anidadas, una por transvertidor, más una pestaña '+' para crear nuevos transvertidores.

| Control | Qué hace |
|---|---|
| **RX Only:** | Fuerza solo RX en ese transvertidor |
| **Remove (xvtr)** | Elimina la definición del transvertidor |
| **Create New Transverter** | Agrega una nueva entrada de transvertidor |

---

## Pestaña USB Cables

La pestaña **USB Cables** asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Qué hace |
|---|---|
| **Lista de cables / Estado** | Cables USB detectados por tipo con estado Conectado/Desconectado |
| **Name: / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0-7)** | Parámetros serie y comportamiento por cable |

---

## Pestaña Peripherals

La pestaña **Peripherals** permite la conexión IP manual a dispositivos externos (TGXL, PGXL, Antenna Genius).

| Control | Qué hace | Notas |
|---|---|---|
| **Connect / Disconnect (TGXL)** | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al inicio. | Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune`. |
