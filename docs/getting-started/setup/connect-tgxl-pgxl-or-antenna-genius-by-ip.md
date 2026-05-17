# Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, antenas, filtros, XVTR, cables USB, periféricos, APD, temas y configuración del puerto serie.

## Abrir el diálogo

1. Abra `Settings > Radio Setup...`.
2. El diálogo se abre como una ventana persistente. Su tamaño y posición se guardan entre sesiones.

---

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador | Número de serie del chasis (solo lectura). |
| Region | Indicador | Región regulatoria de la radio. |
| HW Version | Indicador | Cadena de versión de hardware. |
| Model | Indicador | Modelo de radio. |
| Options | Indicador | Muestra las opciones de radio licenciadas. |
| FlexControl | Indicador | Estado detectado del hardware FlexControl. |
| multiFLEX | Indicador | Estado de multiFLEX habilitado. |
| Nickname | Campo de texto | Apodo descriptivo de la radio. |
| Callsign | Campo de texto | Indicativo de la estación. |
| Station Name | Campo de texto | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto es el nombre del host del SO si está vacío. Se almacena en AppSettings. Se envía a la radio como 'client station \<name\>'. |
| License Info | Indicador | Muestra los detalles de la licencia desde la radio (Suscripción, Vencimiento, ID de Radio, Versión licenciada). |

### Remote On

Haga clic en **Remote On** para habilitar la funcionalidad de encendido/activación remota.

### Actualización de firmware

**Check for Update** consulta a la radio si hay actualizaciones de firmware disponibles. Cuando se encuentra una versión más reciente, AetherSDR muestra un mensaje informativo:

> Actualización disponible: v*X.Y.Z*
> Descargue el instalador de SmartSDR desde flexradio.com,
> luego haga clic en 'Select Installer...' para prepararlo.

**Select Installer...** (renombrado desde Browse .ssdr... en v0.9.3) acepta tres tipos de archivo:

| Tipo de archivo | Extensión | Notas |
|---|---|---|
| Instalador WiX de SmartSDR | .msi | FlexRadio v4.2 y posteriores |
| Instalador autoextraíble de SmartSDR | .exe | Versiones antiguas de SmartSDR |
| Archivo de firmware extraído | .ssdr | Como en versiones anteriores de AetherSDR |

El preparador de firmware detecta el formato automáticamente a partir de los primeros 8 bytes del archivo (cabecera mágica OLE/MSI frente a cabecera PE/COFF MZ) y extrae la carga útil .ssdr sin necesidad de herramientas externas.

#### Para preparar firmware desde un instalador local

1. Descargue el instalador de SmartSDR desde flexradio.com.
2. Abra `Settings > Radio Setup...`.
3. Haga clic en la pestaña **Radio**.
4. Haga clic en **Select Installer...**.
5. En el selector de archivos, seleccione el archivo .msi, .exe o .ssdr.
6. AetherSDR extrae y prepara el firmware. Observe la barra de progreso y la línea de estado para ver el progreso y cualquier error.
7. Cuando la preparación esté completa, haga clic en **Upload Firmware** para enviar el firmware a la radio.

---

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones avanzadas de red.

### Información de red

| Control | Tipo | Comportamiento |
|---|---|---|
| IP Address / Mask / MAC Address | Indicador | Direcciones de red de solo lectura. |

### Configuración de red

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Enforce Private IP Connections | Botón de alternancia | — | — | Rechaza pares que no sean RFC1918. |
| Network MTU | Spinbox | 1450 | 576–9000 bytes | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. |
| DHCP / Static | Botón de alternancia | — | — | Cambia entre modos DHCP e IP estática. |
| IP Address / Mask / Gateway | Campo de texto | — | — | Campos de configuración de IP estática. |
| Apply | Botón pulsador | — | — | Envía la configuración de red a la radio. |

---

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS y la información en vivo de latitud, longitud, altitud, hora y satélites.

---

## Pestaña TX

La pestaña TX contiene temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall, opciones de seguimiento slice/TX y un acceso directo a TX Band Settings.

### TX Band Settings

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Temporizaciones

La sección de temporizaciones de TX incluye campos spinbox para valores en milisegundos.

| Control | Etiqueta mostrada | Valor predeterminado | Comportamiento |
|---|---|---|---|
| ACC TX | ACC TX: | — | Retardo de temporización ACC en ms. |
| TX Delay | TX Delay: | — | Retardo de TX en ms. |
| RCA TX1 | RCA TX1: | — | Retardo de RCA TX1 en ms. |
| Timeout | Timeout (seg): | — | Tiempo de espera del enclavamiento mostrado en segundos. La radio almacena este valor en milisegundos. |

### Enclavamientos

Los botones de alternancia **TX REQ: RCA** y **TX REQ: Accessory** habilitan las entradas de enclavamiento RCA y de accesorio.

### Potencia y sintonía

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Max Power | Spinbox | — | 0–100% | Establece el límite de potencia TX a nivel de radio. |
| Tune Mode | Cuadro combinado | — | — | Selecciona cómo se comporta el botón de sintonía. |

### Waterfall y seguimiento de slice

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Show TX in Waterfall | Botón de alternancia | — | — | Dibuja la señal TX en el waterfall. |
| TX Follows Active Slice | Botón pulsador | Falso | `TxFollowsActiveSlice` | TX sigue al slice activo. Es mutuamente excluyente con 'Active Slice Follows TX'. Se deshabilita automáticamente durante una operación de Split. |
| Active Slice Follows TX | Botón pulsador | Falso | `ActiveFollowsTxSlice` | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Es mutuamente excluyente con 'TX Follows Active Slice'. |

---

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Micrófono

**Enable/Disable the Level Meter During Receive** alterna la visualización del medidor de nivel del micrófono incluso en RX.

### Manipulador CW

| Control | Tipo | Valor predeterminado | Rango | Comportamiento |
|---|---|---|---|---|
| Iambic | Botón de alternancia | — | Habilitado / Deshabilitado | Habilita o deshabilita el manipulador iámbico en la radio. |
| Iambic Mode | Botón pulsador | A | A / B | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. |
| Swap | Botón de alternancia | — | — | Intercambia dit/dah. |
| Sideband | Cuadro combinado | — | LSB / USB | Selecciona la banda lateral del tono CW. |
| CWX | Botón de alternancia | — | — | Habilita el keying de macros CWX. |
| Decode | Botón de alternancia | Verdadero | — | Habilita la superposición de decodificación CW en el panadapter. Clave de configuración: `CwDecodeOverlay`. |

### RTTY

**RTTY Mark Default** spinbox establece la frecuencia de marca RTTY predeterminada.

---

## Pestaña RX

La pestaña RX contiene la calibración del desplazamiento de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

| Control | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz) | Spinbox | Frecuencia utilizada para la calibración manual. |
| Start | Botón pulsador | Inicia el barrido de calibración de frecuencia. |
| Freq Offset (ppb) | Spinbox | Desplazamiento de frecuencia manual en ppb. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** lista dinámicamente las fuentes de oscilador disponibles según el hardware presente y el estado del oscilador informado por la radio.

| Etiqueta | Valor interno | Cuándo se muestra |
|---|---|---|
| Auto | auto | Siempre se muestra |
| TCXO | tcxo | Se muestra cuando hay hardware TCXO presente, se ha recibido el estado del oscilador, o la configuración actual o guardada es `tcxo` |
| GPSDO | gpsdo | Se muestra cuando hay hardware GPSDO presente o la configuración actual o guardada es `gpsdo` |
| External 10 MHz | external | Se muestra cuando una referencia externa está presente, se ha recibido el estado del oscilador, o la configuración actual o guardada es `external` |

#### Visualización del estado de bloqueo

La etiqueta de estado de bloqueo junto al cuadro combinado muestra información más detallada que texto plano:

| Situación | Ejemplo de texto mostrado |
|---|---|
| Estado del oscilador aún no recibido | `Waiting for oscillator status` |
| El modo Auto se ha resuelto a una fuente | `Auto -> GPSDO Locked` |
| La configuración guardada difiere del estado activo | `TCXO -> GPSDO Locked` |
| Configuración y estado coinciden | `GPSDO Locked` |
| External seleccionado pero referencia no detectada | `External 10 MHz Unlocked (not detected)` |

El color de la etiqueta se actualiza automáticamente: verde (`#00c040`) cuando está bloqueado, rojo (`#c04040`) cuando está desbloqueado y gris (`#8aa8c0`) mientras espera el estado.

---

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Tipo | Comportamiento |
|---|---|---|
| Line Out | Deslizador | Ganancia de salida de línea. |
| Mute (Line Out) | Botón pulsador | Silencia la salida de línea. |
| Headphone | Deslizador | Ganancia de auriculares. |
| Mute (Headphone) | Botón pulsador | Silencia los auriculares. |
| Front Speaker / Mute | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |

### Compresión de audio

**Audio Compression (SmartLink):** alterna entre Auto, Uncompressed y Opus. Clave de configuración: `AudioCompression`.

### Suspensión del sistema

**Prevent system sleep while connected** checkbox mantiene el SO activo mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Valor predeterminado: Falso. Clave de configuración: `InhibitSleepWhileConnected`.

### Dispositivos de audio del PC

**PC Audio Devices: Input:** y **Output:** cuadros combinados para seleccionar los dispositivos de entrada y salida de audio del host.

### Refuerzo de audio

**Audio Boost** botón de alternancia habilita ganancia adicional en la ruta de audio del cliente. Clave de configuración: `AudioBoost`.

### Búfer de audio

**Audio Buffer** campo de texto establece el búfer de audio en milisegundos para fluctuación de VPN/SmartLink. Valor predeterminado: 200. Rango: 50–1000 ms. Clave de configuración: `AudioBufferMs`.

### Grabación

| Control | Tipo | Valor predeterminado | Clave de configuración | Comportamiento |
|---|---|---|---|---|
| Recording | Botón pulsador | Radio Side | `RecordingMode` | Elige grabación del lado de la radio o del lado del cliente. Opciones: Radio Side / Client Side. |
| Save to | Campo de texto | — | `QsoRecordingDir` | Carpeta para grabaciones guardadas (solo lado del cliente). Por defecto: Documentos/AetherSDR/Grabaciones. |
| ... | Botón pulsador | — | — | Examina para seleccionar la carpeta de grabación. |
| Auto-record on TX | Casilla de verificación | Falso | `QsoRecordingAutoRecord` | Graba automáticamente mientras se transmite. |
| Idle timeout | Spinbox | 120 | `QsoRecordingIdleTimeout` | Segundos de silencio antes de que la grabación se detenga. Rango: 10–3600 seg. |

### NVIDIA BNR

Los controles **NVIDIA BNR** (Autostart Container, Start, Stop, Check Status) gestionan el contenedor de eliminación de ruido NVIDIA Broadcast. Un punto de estado indica Running (verde), Stopped (rojo) o Unknown (gris).

---

## Pestaña Antennas

La pestaña Antennas permite nombrar los puertos de antena de la radio para mostrarlos en los paneles del panadapter y del slice. Esta pestaña se construye de forma diferida al hacer clic por primera vez.

---

## Pestaña Filters

La pestaña Filters proporciona opciones de filtro de baja latencia y nítidos por ancho de banda.

### Nitidez del filtro

**Voice / CW / Digital filter sharpness sliders** establecen la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está habilitado.

**Auto (Voice / CW / Digital)** botones de alternancia habilitan la selección automática del nivel de filtro para ese modo, deshabilitando el deslizador de nitidez manual.

### Filtros de modo digital

**Use Low Latency Filters for Digital Modes** casilla de verificación fuerza el uso de filtros de baja latencia en DIGU/DIGL.

---

## Pestaña XVTR

La pestaña XVTR configura ajustes por transvertidor. Contiene pestañas anidadas, una por transvertidor, y una pestaña '+' para crear nuevos transvertidores.

| Control | Tipo | Comportamiento |
|---|---|---|
| RX Only | Botón de alternancia | Fuerza solo RX en ese transvertidor. |
| Remove | Botón pulsador | Elimina la definición del transvertidor. |
| Create New Transverter | Botón pulsador | Agrega una nueva entrada de transvertidor. |

---

## Pestaña USB Cables

La pestaña USB Cables asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT.

| Control | Tipo | Comportamiento |
|---|---|---|
| Cables list / Status | Indicador | Cables USB detectados por tipo con estado Conectado/Desconectado. |
| Name / Enabled / Speed / Data Bits / Parity / Stop Bits / Flow / Source / Auto Report / BCD Type / Polarity / Bit Configuration (0–7) | Cuadro combinado | Parámetros serie y comportamiento por cable. |

---

## Pestaña Peripherals

La pestaña Peripherals habilita la conexión IP manual a dispositivos externos (TGXL, PGXL, Antenna Genius o ShackSwitch) cuando la detección automática no ha encontrado el dispositivo.

### Antes de comenzar

- AetherSDR ya debe estar conectado a una radio FLEX-8600. La pestaña Peripherals solo está disponible cuando hay una conexión de radio activa.
- Tenga lista la dirección IP del dispositivo TGXL, PGXL, Antenna Genius o ShackSwitch.

### Pasos

1. Abra `Settings > Radio Setup...
