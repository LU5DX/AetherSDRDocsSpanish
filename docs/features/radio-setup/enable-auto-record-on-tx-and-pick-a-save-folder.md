# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Se abre desde `Settings > Radio Setup...` y requiere una conexión de radio activa.

## Diseño del Diálogo

La ventana del diálogo utiliza el marco de diálogos persistentes, guardando y restaurando su geometría automáticamente entre sesiones. El área de contenido principal contiene una interfaz de pestañas con las siguientes pestañas:

- **Radio** — Información de la radio, identificación, información de licencia y actualización de firmware
- **Network** — Información de red de la radio y opciones avanzadas de red
- **GPS** — Presencia de GPS e información en vivo de lat/lon/alt/hora/satélites
- **TX** — Temporizaciones de TX, interbloqueos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y acceso directo a Configuración de Banda TX
- **Phone/CW** — Micrófono, manipulador CW, valores predeterminados de RTTY
- **RX** — Calibración de compensación de frecuencia GPSDO y fuente de referencia de 10 MHz
- **Calibration** — Calibración manual de frecuencia del lado del host (HL2 y otros backends que no pueden auto-calibrarse; oculto para radios con capacidad `hostFrequencyCalibration`)
- **Antennas** — Configuración de nombres de antenas
- **Audio** — Salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y contenedor NVIDIA BNR
- **Filters** — Opciones de filtro de baja latencia / nítido por ancho de banda
- **XVTR** — Configuración por transvertidor
- **USB Cables** — Asigna adaptadores seriales USB a tipos de cable CAT, BCD, bit y PTT
- **Peripherals** — Conexión IP manual de dispositivos externos (TGXL, PGXL, Antenna Genius)
- **APD** — Configuración del muestreador de Pre-Distorsión Adaptativa externa (solo FLEX-8x00 con SmartSDR 4.2.18+)
- **Themes** — Personalización de la interfaz de usuario, incluidos los colores de slices
- **SmartLink** — Gestión de certificados TLS fijados de SmartLink
- **Serial** — Configuración del puerto serial FlexControl y asignación de paletas/botones
- **KiwiSDR** — Configuración del receptor KiwiSDR, apodo personalizado y gestión de receptores públicos/privados

Varias pestañas (Radio, Themes, Audio, Filters, Peripherals) están envueltas en un área de desplazamiento para que su contenido permanezca accesible en pantallas pequeñas o de alto DPI. La barra de desplazamiento aparece automáticamente cuando el contenido excede la altura visible del diálogo; se oculta cuando todo el contenido cabe sin desplazamiento.

La geometría del diálogo (posición y tamaño) se guarda automáticamente al cerrar el diálogo y se restaura en la siguiente apertura. El diálogo hereda de `PersistentDialog`, que maneja la persistencia de geometría bajo la clave `RadioSetupDialogGeometry`.

---

## Pestaña Radio

La pestaña **Radio** muestra información de la radio, identificación, detalles de licencia y controles de actualización de firmware.

### Información de la Radio

Los siguientes indicadores son de solo lectura y muestran información recuperada de la radio conectada:

| Control | Qué muestra |
|---|---|
| **Radio SN** | Número de serie del chasis |
| **Region** | Región regulatoria de la radio (p. ej., USA) |
| **HW Version** | Cadena de versión de hardware |
| **Model** | Modelo de la radio |
| **Options** | Opciones de radio licenciadas |
| **FlexControl** | Estado detectado del hardware FlexControl |
| **multiFLEX** | Estado habilitado de multiFLEX |
| **License Info** | Estado de suscripción, fecha de expiración, ID de radio y versión licenciada |

Cada campo de solo lectura tiene un botón de copiar (icono de portapapeles) que aparece al pasar el cursor o al enfocar. Haga clic en el botón de copiar para copiar el valor de ese campo al portapapeles del sistema. Una breve ventana emergente confirma la acción de copiado.

### Campos de Configuración de Usuario

| Control | Qué hace | Clave de Configuración |
|---|---|---|
| **Nickname** | Apodo de radio fácil de usar | — |
| **Callsign** | Indicativo de la estación | — |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Si está vacío, usa el nombre de host del sistema operativo. | `StationName` |
| **Remote On** | Habilita el encendido remoto / remote-on | — |

### Reiniciar Radio

| Control | Qué hace |
|---|---|
| **Reboot Radio** | Envía un comando de reinicio a la radio conectada. Aparece un diálogo de confirmación antes de reiniciar. El botón está deshabilitado cuando la radio está desconectada. |

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación:

- Para conexiones LAN: "AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciar."
- Para conexiones SmartLink/WAN: "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy — deberá reconectarse manualmente una vez que la radio termine de iniciar."

Haga clic en **OK** para confirmar. El diálogo se cierra y la radio se reinicia.

El botón está habilitado solo cuando la radio está conectada y el backend admite un reinicio del cliente. Por ejemplo, HL2 es solo RX, por lo que el botón está deshabilitado. Se deshabilita automáticamente al desconectarse y se vuelve a habilitar al reconectarse.

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
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes | 1450 | 576-9000 bytes | `NetworkMtu` |
| **Apply** | Envía la configuración de red a la radio | — | — | — |

> **Nota:** El MTU predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Esta configuración se almacena en AppSettings.

### Puente de Automatización (MCP)

La pestaña **Network** incluye controles para el puente de automatización dentro de la aplicación que permite a un asistente de codificación de IA (a través del servidor MCP) inspeccionar y controlar la aplicación en ejecución.

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **Agent Automation (MCP):** | Habilita el puente de automatización dentro de la aplicación | Deshabilitado | Nuevo en v26.8.4 (#3646). Se persiste mediante AutomationBridgeSettings. La variable de entorno de lanzamiento `AETHER_AUTOMATION` fuerza la habilitación del puente independientemente de este interruptor y deshabilita el control en la interfaz de usuario. El accionamiento de transmisión permanece bloqueado a menos que se establezca `AETHER_AUTOMATION_ALLOW_TX`. |
| **Access Token:** | Visualización de solo lectura del token de acceso MCP; péguelo en la variable de entorno `AETHER_MCP_TOKEN` del asistente. Se almacena en el almacén secreto del sistema operativo. | (ninguno) | Nuevo en v26.8.4. Genera automáticamente un token hexadecimal de 128 bits cuando el puente se habilita sin uno. Marcador '(loading…)' hasta que se complete la lectura del llavero. |
| **Copy (Access Token)** | Copia el token de acceso al portapapeles | — | Nuevo en v26.8.4. |
| **Rotate (Access Token)** | Genera un nuevo token y lo aplica inmediatamente, bloqueando a cualquier cliente que aún use el anterior | — | Nuevo en v26.8.4. |
| **Allow TX via MCP: Enable transmit control** | Permite que un cliente MCP accione el transmisor (MOX/PTT/TUNE/ATU/CWX) | False | Nuevo en v26.8.4. Se aplica en el puente; ningún cliente puede cambiarlo. Es anulado por `AETHER_AUTOMATION_ALLOW_TX` (forzado a activado) y `AETHER_AUTOMATION_NO_TX` (fijado en desactivado). Un vigilante de desactivación forzada limita la TX originada por el puente. |
| **Observe only: Read-only (block all driving)** | Hace que el puente sea de solo observación: los clientes MCP pueden leer el estado, pero cada verbo de mutación (set/invoke/connect/tune/capture) es rechazado | False | Nuevo en v26.8.4 (#4188). Se aplica en la aplicación, por lo que un cliente no puede omitirlo. La variable de lanzamiento `AETHER_AUTOMATION_READONLY` lo fija en activado para ejecuciones headless/CI. |

### Búfer de Recepción VITA-49

| Control | Qué hace | Predeterminado | Rango | Notas |
|---|---|---|---|---|
| **VITA-49 RX buffer:** | Deslizador con ajuste a valores preestablecidos que establece el búfer de recepción del kernel (SO_RCVBUF) para el socket de flujo VITA-49; un valor mayor absorbe ráfagas de panadapter/waterfall para que no se pierdan paquetes | 4 MB | 0.25-4 MB (preestablecidos) | Nuevo en v26.8.4 (#3810). Preestablecidos de 256 KB a 4 MB. El sistema limita la concesión a `net.core.rmem_max`; una etiqueta en vivo 'granted: <size>' muestra lo que el kernel realmente concedió. |
| **granted: (VITA-49 RX buffer)** | Muestra el tamaño del búfer que el kernel realmente concedió (en comparación con el valor preestablecido solicitado) | — | — | Nuevo en v26.8.4. Muestra '(applies on connect)' cuando no hay una conexión activa. |

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo cuando hay un receptor GPS instalado.

| Control | Qué muestra |
|---|---|
| **GPS** | Información en vivo de lat/lon/alt/hora/satélites |

---

## Pestaña TX

La pestaña **TX** configura temporizaciones de transmisión, interbloqueos, potencia, modo de sintonía y comportamiento de seguimiento slice/TX.

### Configuración de Banda TX

| Control | Qué hace |
|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda |

### Configuración de TX

| Control | Qué hace | Predeterminado | Rango |
|---|---|---|---|
| **Timings** | Temporizaciones de retención / retardo de TX. Incluye campos ACC TX, TX Delay, RCA TX1 y Timeout. | — | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de interbloqueo RCA y de accesorio | — | — |
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
| **Timeout (sec):** | Tiempo de espera de interbloqueo mostrado en segundos. La radio almacena internamente este valor en milisegundos. | Ingrese el valor en segundos; el diálogo lo convierte a milisegundos antes de enviarlo a la radio. |

> **Nota:** El campo Timeout anteriormente mostraba minutos, pero ahora muestra segundos para una resolución más fina en configuraciones TOT de ciclo corto.

### Seguimiento Slice/TX

| Control | Qué hace | Predeterminado | Clave de Configuración |
|---|---|---|---|
| **TX Follows Active Slice** | La TX sigue a la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. | False | `TxFollowsActiveSlice` |
| **Active Slice Follows TX** | Cambia la slice activa cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | False | `ActiveFollowsTxSlice` |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Qué hace | Predeterminado | Rango | Clave de Configuración |
|---|---|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX | — | — | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio | — | Enabled / Disabled | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A | A / B | — |
| **Swap:** | Intercambia dit/dah | — | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW | — | LSB / USB | — |
| **CWX:** | Habilita el accionamiento de macros CWX | — | — | — |
| **Decode: RX** | Habilita la superposición de decodificación CW en el panadapter para CW recibido | True | — | `CwDecoder` (JSON anidado, campo `rx`) |
| **Decode: TX** | Decodifica el manipulador CW del propio operador mediante el sonido lateral del lado del cliente, útil como herramienta de autoentrenamiento para la sincronización de paleta/bug | False | — | `CwDecoder` (JSON anidado, campo `tx`) |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada | — | — | — |

> **Nota:** Los botones Mode A y Mode B están disponibles junto al interruptor Iambic Enabled. Mode A = Curtis A; Mode B = Curtis B. Estos también controlan el manipulador iámbico de software local (IambicKeyer), que refleja el estado iámbico de la radio para el sonido lateral de menos de 5 ms.

> **Nota:** Los interruptores **Decode: RX** y **Decode: TX** se separaron de un único interruptor `CwDecodeOverlay` en v26.5.3. Se persisten como un blob JSON anidado bajo `CwDecoder` con campos `rx` y `tx`. El `CwDecode
