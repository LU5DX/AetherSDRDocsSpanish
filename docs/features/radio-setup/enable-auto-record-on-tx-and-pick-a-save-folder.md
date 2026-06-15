# Diálogo de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Se abre desde `Settings > Radio Setup...` y requiere una conexión activa con la radio.

## Disposición del Diálogo

La ventana de diálogo utiliza el marco de diálogo persistente, guardando y restaurando su geometría automáticamente entre sesiones. El área de contenido principal contiene una interfaz de pestañas con las siguientes pestañas:

- **Radio** — Información de la radio, identificación, información de licencia y actualización de firmware
- **Network** — Información de red de la radio y opciones de red avanzadas
- **GPS** — Presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites
- **TX** — Temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, cascada visual, seguimiento slice/TX y acceso directo a Configuración de Banda de TX
- **Phone/CW** — Micrófono, manipulador CW, valores predeterminados de RTTY
- **RX** — Calibración de desviación de frecuencia del GPSDO y fuente de referencia de 10 MHz
- **Antennas** — Configuración de nombres de antenas
- **Audio** — Salidas de audio de la radio, compresión, dispositivos del PC, realce, búfer, grabación y contenedor NVIDIA BNR
- **Filters** — Opciones de filtro de baja latencia / nítido por ancho de banda
- **XVTR** — Configuración por transvertidor
- **USB Cables** — Asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT
- **Peripherals** — Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius)
- **APD** — Configuración del muestreador de Pre-Distorsión Adaptativa externa (solo FLEX-8x00 con SmartSDR 4.2.18+)
- **Themes** — Personalización de la interfaz de usuario, incluidos los colores de los slices
- **SmartLink** — Gestión de certificados TLS de SmartLink fijados
- **Serial** — Configuración del puerto serie de FlexControl y asignación de paletas/botones

Varias pestañas (Radio, Themes, Audio, Filters, Peripherals) están envueltas en un área de desplazamiento para que su contenido permanezca accesible en pantallas pequeñas o de alta densidad de píxeles (DPI). La barra de desplazamiento aparece automáticamente cuando el contenido supera la altura visible del diálogo; se oculta cuando todo el contenido cabe sin necesidad de desplazamiento.

La geometría del diálogo (posición y tamaño) se guarda automáticamente al cerrar el diálogo y se restaura al abrirlo de nuevo. El diálogo hereda de `PersistentDialog`, que gestiona la persistencia de la geometría bajo la clave `RadioSetupDialogGeometry`.

---

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, detalles de licencia y controles de actualización de firmware.

### Información de la Radio

Los siguientes indicadores son de solo lectura y muestran información recuperada de la radio conectada:

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región reglamentaria de la radio (p. ej., USA) |
| **HW Version** | Cadena de versión del hardware |
| **Model** | Modelo de la radio |
| **Options** | Opciones de radio con licencia |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de vencimiento, ID de radio y versión con licencia |

Cada campo de solo lectura tiene un botón de copia (icono de portapapeles) que aparece al pasar el cursor o al enfocarse. Haga clic en el botón de copia para copiar el valor de ese campo al portapapeles del sistema. Una breve ventana emergente confirma la acción de copia.

### Campos de Configuración del Usuario

| Control | Qué hace | Clave de Configuración |
|---|---|---|
| **Nickname** | Apodo de radio fácil de usar para el usuario | — |
| **Callsign** | Indicativo de la estación | — |
| **Station Name** | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Por defecto, usa el nombre de host del sistema operativo si está vacío. | `StationName` |
| **Remote On** | Habilita el encendido remoto / activación remota | — |

### Reiniciar la Radio

| Control | Qué hace |
|---|---|
| **Reboot Radio** | Envía un comando de reinicio a la radio conectada. Aparece un diálogo de confirmación antes de reiniciar. El botón está deshabilitado cuando la radio está desconectada. |

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación:

- Para conexiones LAN: "AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciarse."
- Para conexiones SmartLink/WAN: "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy en día; deberá reconectarse manualmente una vez que la radio termine de iniciarse."

Haga clic en **OK** para confirmar. El diálogo se cierra y la radio se reinicia.

El botón está habilitado solo cuando la radio está conectada. Se deshabilita automáticamente al desconectarse y se rehabilita al reconectarse.

### Actualización de Firmware

La pestaña **Radio** incluye controles de actualización de firmware. Para más detalles, consulte la sección [Actualización de Firmware](#firmware-update-radio-tab) a continuación.

---

## Pestaña Network

La pestaña **Network** muestra información de red y permite la configuración de los ajustes de red de la radio.

### Información de Red

Los siguientes indicadores son de solo lectura:

| Control | Qué muestra |
|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura |

### Configuración de Red

| Control | Qué hace | Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **DHCP / Static** | Cambia entre modos DHCP e IP estática | — | — | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática | — | — | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918 | — | — | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes | 1450 | 576-9000 bytes | `NetworkMtu` |
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

### Configuración de Banda de TX

| Control | Qué hace |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda |

### Configuración de TX

| Control | Qué hace | Predeterminado | Rango |
|---|---|---|---|
| **Timings** | Temporizaciones de retención/retardo de TX. Incluye campos de ACC TX, TX Delay, RCA TX1 y Timeout. | — | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y accesorio | — | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio | — | 0-100 % |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía | — | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en la cascada visual | — | — |

### Campos de Temporización

La sección **Timings** incluye cuatro campos:

| Control | Qué hace | Notas |
|---|---|---|
| **ACC TX:** | Retardo de transmisión de ACC en milisegundos | — |
| **TX Delay:** | Retardo de transmisión en milisegundos | — |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento mostrado en segundos. La radio almacena internamente este valor en milisegundos. | Introduzca el valor en segundos; el diálogo lo convierte a milisegundos antes de enviarlo a la radio. |

> **Nota:** El campo Timeout anteriormente mostraba minutos, pero ahora muestra segundos para una resolución más fina en configuraciones TOT de ciclo corto.

### Seguimiento Slice/TX

| Control | Qué hace | Predeterminado | Clave de Configuración |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue al slice activo. Es mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. | False | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. | False | `ActiveFollowsTxSlice` |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Qué hace | Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX | — | — | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio | — | Habilitado / Deshabilitado | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A | A / B | — |
| **Swap:** | Intercambia dit/dah | — | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW | — | LSB / USB | — |
| **CWX:** | Habilita el tecleo de macros CWX | — | — | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter | True | — | `CwDecodeOverlay` |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY | — | — | — |

> **Nota:** Los botones Mode A y Mode B están disponibles junto al conmutador Iambic Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el manipulador iámbico de software local (IambicKeyer), que refleja el estado iámbico de la radio para un tono de prueba (sidetone) inferior a 5 ms.

---

## Pestaña RX

La pestaña **RX** proporciona calibración manual de desviación de frecuencia y selección de la fuente de referencia de 10 MHz.

Los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Controles de Calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Introduzca la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<value>` cuando termina de editar el campo. |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en ejecución. Una etiqueta de estado junto al botón informa del progreso. |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en partes por mil millones. |

### Fuente de Referencia de 10 MHz

| Control | Qué hace | Predeterminado | Rango |
|---|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO/GPSDO/External). El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. | Auto | Auto / TCXO / GPSDO / External |

La etiqueta de estado de bloqueo junto a **10 MHz Reference Source:** muestra información más detallada. El texto y el color de la etiqueta se actualizan en vivo a medida que la radio informa de los cambios en el estado del oscilador.

**Formato del texto de la etiqueta:**

| Condición | Texto de ejemplo |
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

El cuadro combinado **10 MHz Reference Source:** se llena dinámicamente según el hardware que la radio informa como presente, la configuración actual y el estado activo del oscilador. La entrada **External** está etiquetada como **External 10 MHz**. Si la radio envía el valor `ext`, se trata como equivalente a `external`.

### Iniciar una Calibración

1. Haga clic en la pestaña **RX** en Configuración de la Radio.
2. Introduzca la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para ver el progreso y el resultado.
4. Cuando la calibración finalice, el botón se rehabilita.

---

## Pestaña Antennas

La pestaña **Antennas** le permite configurar nombres fáciles de usar para cada puerto de antena en la radio, reemplazando las etiquetas de puerto predeterminadas (ANT1, ANT2, XVTA, XVTB, etc.) con identificadores personalizados que aparecen en toda la interfaz de AetherSDR.

| Control | Qué hace |
|---|---|
| **Antenna name fields** | Un campo de texto por puerto de antena. Introduzca un nombre personalizado (p. ej., "HF Vertical", "6M Yagi", "160M Loop"). Los nombres se envían a la radio y se conservan en la configuración de la radio. |

**Para establecer un nombre de antena:**

1. Haga clic en la pestaña **Antennas** en Configuración de la Radio.
2. Para cada puerto de antena, escriba el nombre deseado en el campo de texto correspondiente.
3. Presione Enter o tabulador para pasar al siguiente campo y confirmar el nombre en la radio.

---

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos del PC, realce, búfer, grabación y contenedor NVIDIA BNR.

| Control | Qué hace | Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Line Out:** | Control deslizante de ganancia de salida de línea | — | — | — |
| **Mute (Line Out)** | Silencia la salida de línea | — | — | — |
| **Headphone:** | Control deslizante de ganancia de auriculares | — | — | — |
| **Mute (Headphone)** |
