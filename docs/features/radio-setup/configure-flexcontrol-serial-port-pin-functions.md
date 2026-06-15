# Configurar Configuración de Radio

El diálogo **Configuración de Radio** (`Settings > Radio Setup...`) proporciona la configuración maestra por radio con secciones con pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, audio, filtros, transverters, cables USB, periféricos, predistorsión adaptativa, temas, certificados fijados de SmartLink y configuración de puertos serie.

## Antes de comenzar

- La radio debe estar conectada para que la mayoría de las pestañas muestren información en vivo.
- Algunas pestañas (APD, Themes, SmartLink, Serial) se crean de forma diferida y solo aparecen al hacer clic en ellas por primera vez.
- AetherSDR utiliza una clase base `PersistentDialog` que guarda y restaura la geometría de la ventana automáticamente.

## Pasos para abrir

1. Haga clic en **Settings > Radio Setup...** en el menú principal.
2. El diálogo se abre mostrando la pestaña **Radio** de forma predeterminada.
3. Haga clic en cualquier pestaña para acceder a su configuración.

---

## Pestaña Radio

La pestaña **Radio** muestra la identificación de la radio, la información de licencia y los controles de actualización de firmware.

### Lectura de información de la radio

- **Radio SN** — Número de serie del chasis (solo lectura). Muestra el número de serie del chasis si está disponible; de lo contrario, el número de serie de la radio. Incluye un botón de copia al portapapeles junto al valor.
- **Region** — Región regulatoria de la radio (solo lectura).
- **HW Version** — Versión del hardware (solo lectura). Incluye un botón de copia al portapapeles junto al valor.
- **Model** — Modelo de la radio (solo lectura). Incluye un botón de copia al portapapeles junto al valor.
- **Options** — Opciones de radio licenciadas (solo lectura). Muestra la lista de opciones de la radio, o un valor predeterminado como "GPS, PGXL" si se detecta un amplificador. Incluye un botón de copia al portapapeles junto al valor.
- **FlexControl** — Estado detectado del hardware FlexControl (solo lectura).
- **multiFLEX** — Estado habilitado de multiFLEX (solo lectura).
- **License Info** — Muestra suscripción, vencimiento, ID de radio y versión licenciada (solo lectura). Cada campo incluye un botón de copia al portapapeles junto al valor.

### Copiar información de la radio

Cada valor de solo lectura tiene un pequeño botón de copia junto a él. Haga clic en el botón de copia para copiar el valor a su portapapeles. Aparece una breve ventana emergente "¡Copiado!" cerca del botón. El botón de copia está deshabilitado cuando el valor está vacío o muestra "—".

### Configuración de identificación

| Control | Qué hace | Notas |
|---|---|---|
| **Nickname** | Apodo de la radio fácil de usar (editable). | — |
| **Callsign** | Indicativo de la estación (editable). | — |
| **Station Name** | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Almacenado en AppSettings. | Usa el nombre de host del sistema operativo si está vacío. Se envía a la radio como 'client station <name>'. |

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar las actualizaciones de firmware disponibles. El resultado aparece en la etiqueta de estado. Si hay una actualización disponible, la etiqueta le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Haga clic en **Select Installer...** para abrir un selector de archivos. Seleccione uno de:
   - `.msi` — Instalador de SmartSDR basado en WiX para firmware 4.2+.
   - `.exe` — Instalador de SmartSDR autoextraíble antiguo.
   - `.ssdr` — Archivo de firmware preextraído.
3. El gestor de firmware detecta el formato del archivo automáticamente y extrae la carga útil `.ssdr`. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción.
4. Una vez completada la extracción, haga clic en **Upload Firmware** para iniciar la subida. Una barra de progreso y una etiqueta de estado muestran el progreso de la subida.

| Control | Qué hace | Notas |
|---|---|---|
| **Check for Update** | Consulta las actualizaciones de firmware disponibles. | Cuando se encuentra una actualización, la etiqueta le indica que descargue el instalador desde flexradio.com. |
| **Select Installer...** | Abre un selector de archivos para archivos `.msi`, `.exe` o `.ssdr`. | Renombrado desde **Browse .ssdr...** en v26.5.3. |
| **Upload Firmware** | Inicia la subida de firmware con barra de progreso y estado. | Habilitado solo después de que se completa la extracción. |

### Remote On

Haga clic en **Remote On** para habilitar la funcionalidad de activación remota/encendido remoto en la radio.

### Reboot Radio

Haga clic en **Reboot Radio** para reiniciar la radio conectada. Aparece un diálogo de confirmación:
- **Conexión LAN**: AetherSDR se desconecta y se reconecta automáticamente una vez que la radio termina de iniciar.
- **Conexión SmartLink/WAN**: AetherSDR se desconecta y no se reconecta automáticamente. Debe reconectarse manualmente una vez que la radio termina de iniciar.

El botón está deshabilitado cuando la radio está desconectada. Se vuelve a habilitar automáticamente cuando la radio se reconecta.

---

## Pestaña Network

La pestaña **Network** muestra información de red de la radio y opciones de red avanzadas.

### Lectura de información de red

- **IP Address / Mask / MAC Address** — Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles.

### Configuración de red

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **Enforce Private IP Connections:** | Alternar para rechazar pares que no sean RFC1918. | Habilitado | — |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. | 1450 | Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Almacenado en AppSettings. |
| **DHCP / Static** | Alternar entre modos DHCP e IP estática. | — | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — | Habilitado cuando se selecciona el modo Static. |
| **Apply** | Envía la configuración de red a la radio. | — | — |

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia del GPS y la información de posición/satélites en vivo cuando un receptor GPS está activo.

- Latitud, longitud, altitud, hora y número de satélites (solo lectura).
- Indicador de estado de bloqueo GPS.

---

## Pestaña TX

La pestaña **TX** configura los tiempos de transmisión, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento de slice/TX y configuración de banda de TX.

### Configuración de Banda de TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Tiempos

Use los cuadros de giro en la sección **Timings (in ms)** para establecer los tiempos de espera y retardo de TX.

### Enclavamientos

Active o desactive **TX REQ: RCA** y **TX REQ: Accessory** para habilitar las entradas de enclavamiento de RCA y accesorio.

### Potencia Máxima

Establezca el límite de potencia de TX a nivel de radio usando el cuadro de giro **Max Power:** (0–100%).

### Modo de Sintonía

Seleccione el comportamiento del botón de sintonía desde el cuadro combinado **Tune Mode:** .

### Waterfall

Active **Show TX in Waterfall:** para dibujar la señal de TX en el waterfall.

### Seguimiento Slice/TX

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue el slice activo. | Falso | Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). | Falso | Mutuamente excluyente con **TX Follows Active Slice**. |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Medidor de Nivel

Active **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel de micrófono incluso durante la recepción.

### Manipulador CW

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. | — | En v0.9.1, se agregaron los botones Modo A y Modo B junto al interruptor de habilitación. Modo A = Curtis A; Modo B = Curtis B. |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. | A | Par mutuamente excluyente agregado en v0.9.1. |
| **Swap:** | Intercambia dit/dah. | — | — |
| **Sideband:** | Selecciona la banda lateral del tono CW. | — | Opciones: LSB / USB. |
| **CWX:** | Habilita la activación de macros CWX. | — | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. | Verdadero | Almacenado como `CwDecodeOverlay`. |

### RTTY

Establezca la frecuencia predeterminada de la marca RTTY usando el cuadro de giro **RTTY Mark Default:** .

---

## Pestaña RX

La pestaña **RX** proporciona la calibración de desplazamiento de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

La sección de calibración siempre es visible, independientemente de si hay un GPSDO instalado.

- **GPSDO instalado** — se muestra en verde: *GPSDO instalado. Calibración manual de desplazamiento de frecuencia disponible.*
- **Sin GPSDO** — se muestra en ámbar: *Calibración manual de desplazamiento de frecuencia disponible.*

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | Siempre se muestra. |
| **Start** | Inicia el barrido de calibración de frecuencia. | Deshabilitado y etiquetado como **Busy** mientras está activo. Valida que se haya ingresado una frecuencia de calibración. Restablece el error de frecuencia almacenado a cero antes de comenzar. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por billón. | Se restablece a 0 cuando se hace clic en **Start**. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** se llena dinámicamente en función del hardware detectado y el estado del oscilador en vivo.

| Control | Qué hace | Notas |
|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Envía `radio oscillator <value>` a la radio cuando se cambia. | **Auto** siempre presente. Entradas adicionales: **TCXO**, **GPSDO**, **External 10 MHz**. Las opciones dependen del hardware detectado y del estado del oscilador en vivo. |
| Etiqueta de estado de bloqueo | Muestra la fuente activa, la resolución de Auto y el estado de bloqueo. Se actualiza en vivo. | Verde = Bloqueado; Rojo = Desbloqueado; Gris-azul = esperando estado. Agrega *(no detectado)* cuando External 10 MHz está activo pero no hay una señal de referencia externa presente. |

La etiqueta de estado de bloqueo muestra:
- *Esperando estado del oscilador* cuando aún no se ha recibido el estado.
- *Auto -> <fuente resuelta>* cuando Auto está seleccionado y la radio ha resuelto a una fuente específica.
- *<configuración> -> <estado activo>* cuando la configuración y el estado activo difieren.
- Solo el nombre de la fuente activa cuando coinciden.

El estado de bloqueo (*Bloqueado* o *Desbloqueado*) siempre se agrega.

---

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

### Salidas de audio de la radio

| Control | Qué hace | Notas |
|---|---|---|
| **Line Out:** | Deslizador de ganancia de salida de línea. | — |
| **Mute (Line Out)** | Silencia la salida de línea. | — |
| **Headphone:** | Deslizador de ganancia de auriculares. | — |
| **Mute (Headphone)** | Silencia los auriculares. | — |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | — |

### Compresión de Audio

Seleccione el códec de audio para SmartLink/LAN usando los botones **Audio Compression (SmartLink):** : **Auto**, **Uncompressed** u **Opus** (predeterminado: Auto). Almacenado como `AudioCompression`.

### Suspensión del sistema

Marque **Prevent system sleep while connected** para mantener el sistema operativo activo mientras la radio está conectada (predeterminado: Falso). Almacenado como `InhibitSleepWhileConnected`.

### Dispositivos de Audio del PC

Seleccione los dispositivos de entrada y salida de audio del host usando los cuadros combinados **Input:** y **Output:** .

### Refuerzo de Audio

Active **Audio Boost:** para habilitar ganancia extra en la ruta de audio del cliente. Almacenado como `AudioBoost`.

### Búfer de Audio

Establezca el campo de texto **Audio Buffer:** para aumentar el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Predeterminado: 200, rango 50–1000 ms. Almacenado como `AudioBufferMs`.

### Grabación

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona la grabación del lado de la radio o del lado del cliente. | Radio Side | Almacenado como `RecordingMode`. |
| **Save to:** | Carpeta para grabaciones guardadas (solo del lado del cliente). | Documents/AetherSDR/Recordings | Almacenado como `QsoRecordingDir`. |
| **...** | Navega a la carpeta de grabación. | — | — |
| **Auto-record on TX** | Graba automáticamente mientras transmite. | Falso | Almacenado como `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga. | 120 | Rango 10–3600 seg. Almacenado como `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

Use los controles **NVIDIA BNR** para gestionar el contenedor de eliminación de ruido NVIDIA Broadcast:
- **Autostart Container** — Habilita el inicio automático.
- **Start / Stop** — Inicia o detiene el contenedor manualmente.
- **Check Status** — Muestra el estado del contenedor (En ejecución/Detenido/Desconocido) con un indicador de punto de color.

---

## Pestaña Filters

La pestaña **Filters** configura opciones de filtro de baja latencia o nítidos por ancho de banda.

### Nitidez del filtro

Para modos Voice, CW y Digital, use los **desliz
