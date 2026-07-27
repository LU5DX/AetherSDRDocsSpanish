# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Se abre desde `Settings > Radio Setup...` y requiere una conexión de radio activa.

## Disposición del Diálogo

La ventana del diálogo utiliza el marco de diálogo persistente, guardando y restaurando su geometría automáticamente entre sesiones. El área de contenido principal contiene una interfaz de pestañas con las siguientes pestañas:

- **Radio** — Información de radio, identificación, información de licencia y actualización de firmware
- **Network** — Información de red de la radio y opciones de red avanzadas
- **GPS** — Presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites
- **TX** — Temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y acceso directo a Configuración de Banda TX
- **Phone/CW** — Micrófono, manipulador CW, valores predeterminados de RTTY
- **RX** — Calibración de desviación de frecuencia GPSDO y fuente de referencia de 10 MHz
- **Antennas** — Configuración de nombres de antenas
- **Audio** — Salidas de audio de la radio, compresión, dispositivos de PC, realce, búfer, grabación y contenedor NVIDIA BNR
- **Filters** — Opciones de filtro de baja latencia / nítido por ancho de banda
- **XVTR** — Configuración por transvertidor
- **USB Cables** — Asigna adaptadores USB serie a tipos de cable CAT, BCD, bit y PTT
- **Peripherals** — Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius)
- **APD** — Configuración del muestreador de Pre-Distorsión Adaptativa externa (solo FLEX-8x00 con SmartSDR 4.2.18+)
- **Themes** — Personalización de la interfaz de usuario, incluidos colores de slices
- **SmartLink** — Gestión de certificados TLS de SmartLink anclados
- **Serial** — Configuración del puerto serie de FlexControl y mapeo de paletas/botones
- **KiwiSDR** — Configuración del receptor KiwiSDR, apodo personalizado y gestión de receptor público/privado

Varias pestañas (Radio, Themes, Audio, Filters, Peripherals) están envueltas en un área de desplazamiento para que su contenido permanezca accesible en pantallas pequeñas o de alta densidad de píxeles. La barra de desplazamiento aparece automáticamente cuando el contenido excede la altura visible del diálogo; se oculta cuando todo el contenido cabe sin necesidad de desplazamiento.

La geometría del diálogo (posición y tamaño) se guarda automáticamente al cerrar el diálogo y se restaura en la próxima apertura. El diálogo hereda de `PersistentDialog` que maneja la persistencia de geometría bajo la clave `RadioSetupDialogGeometry`.

---

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, detalles de licencia y controles de actualización de firmware.

### Información de Radio

Los siguientes indicadores son de solo lectura y muestran información recuperada de la radio conectada:

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región regulatoria de la radio (ej., USA) |
| **HW Version** | Cadena de versión de hardware |
| **Model** | Modelo de radio |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de vencimiento, ID de radio y versión licenciada |

Cada campo de solo lectura tiene un botón de copia (icono de portapapeles) que aparece al pasar el ratón o al enfocar. Haga clic en el botón de copia para copiar el valor de ese campo al portapapeles del sistema. Un breve mensaje emergente confirma la acción de copia.

### Campos de Configuración de Usuario

| Control | Qué hace | Clave de Configuración |
|---|---|---|
| **Nickname** | Apodo de radio fácil de usar | — |
| **Callsign** | Indicativo de la estación | — |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto usa el nombre de host del sistema operativo si está vacío. | `StationName` |
| **Remote On** | Habilita el encendido remoto / activación remota | — |

### Reiniciar Radio

| Control | Qué hace |
|---|---|
| **Reboot Radio** | Envía un comando de reinicio a la radio conectada. Aparece un diálogo de confirmación antes de reiniciar. El botón está deshabilitado cuando la radio está desconectada. |

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación:

- Para conexiones LAN: "AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciarse."
- Para conexiones SmartLink/WAN: "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy — deberá reconectarse manualmente una vez que la radio termine de iniciarse."

Haga clic en **OK** para confirmar. El diálogo se cierra y la radio se reinicia.

El botón está habilitado solo cuando la radio está conectada. Se deshabilita automáticamente al desconectarse y se rehabilita al reconectarse.

### Actualización de Firmware

La pestaña **Radio** incluye controles de actualización de firmware. Para más detalles, consulte la sección [Actualización de Firmware](#firmware-update-radio-tab) a continuación.

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
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes | 1450 | 576-9000 bytes | `NetworkMtu` |
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

La pestaña **TX** configura temporizaciones de transmisión, enclavamientos, potencia, modo de sintonía y comportamiento de seguimiento slice/TX.

### Configuración de Banda TX

| Control | Qué hace |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda |

### Configuración de TX

| Control | Qué hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **Timings** | Temporizaciones de retención/retardo de TX. Incluye campos ACC TX, TX Delay, RCA TX1 y Timeout. | — | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y Accessory | — | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | — | 0-100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall | — | — |

### Campos de Temporización

La sección **Timings** incluye cuatro campos:

| Control | Qué hace | Notas |
|---|---|---|
| **ACC TX:** | Retardo de transmisión ACC en milisegundos | — |
| **TX Delay:** | Retardo de transmisión en milisegundos | — |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena internamente este valor en milisegundos. | Ingrese el valor en segundos; el diálogo convierte a milisegundos antes de enviar a la radio. |

> **Nota:** El campo Timeout anteriormente mostraba minutos pero ahora muestra segundos para una resolución más fina en configuraciones de ciclo corto de TOT.

### Seguimiento Slice/TX

| Control | Qué hace | Valor Predeterminado | Clave de Configuración |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. | False | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | False | `ActiveFollowsTxSlice` |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, manipulador CW y valores predeterminados de RTTY.

| Control | Qué hace | Valor Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX | — | — | — |
| **Iambic:** | Habilita o deshabilita el manipulador iambic en la radio | — | Enabled / Disabled | — |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador local por software. Par mutuamente excluyente. | A | A / B | — |
| **Swap:** | Intercambia dit/dah | — | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW | — | LSB / USB | — |
| **CWX:** | Habilita el accionamiento de macros CWX | — | — | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter | True | — | `CwDecodeOverlay` |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada | — | — | — |

> **Nota:** Los botones Mode A y Mode B están disponibles junto al conmutador Iambic Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el manipulador iambic local por software (IambicKeyer) que refleja el estado iambic de la radio para tono lateral de menos de 5 ms.

---

## Pestaña RX

La pestaña **RX** proporciona calibración manual de desviación de frecuencia y selección de fuente de referencia de 10 MHz.

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Controles de Calibración

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<valor>` cuando termina de editar el campo. | |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en ejecución. Una etiqueta de estado junto al botón informa el progreso. | |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en partes por billón. | |

### Fuente de Referencia de 10 MHz

| Control | Qué hace | Valor Predeterminado | Rango |
|---|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/External). El estado de bloqueo (Locked / Unlocked) se muestra junto al combo y se actualiza en vivo. | Auto | Auto / TCXO / GPSDO / External |

La etiqueta de estado de bloqueo junto a **10 MHz Reference Source:** muestra información más detallada. El texto y color de la etiqueta se actualizan en vivo a medida que la radio informa cambios en el estado del oscilador.

**Formato del texto de la etiqueta:**

| Condición | Ejemplo de texto |
|---|---|
| Modo Auto resolviendo a una fuente | `Auto -> GPSDO Locked` |
| Configuración sobrescrita por la radio | `TCXO -> GPSDO Locked` |
| Fuente coincide con la configuración | `GPSDO Locked` |
| External seleccionado pero no detectado | `External 10 MHz Unlocked (not detected)` |
| Esperando el primer informe de estado | `Waiting for oscillator status` |

**Color de la etiqueta:**

| Estado | Color |
|---|---|
| Locked | Verde |
| Unlocked | Rojo |
| No se ha recibido estado aún | Gris/azul |

El cuadro combinado **10 MHz Reference Source:** se completa dinámicamente según el hardware que la radio informa como
