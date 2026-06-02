# Configurar la Configuración del Radio

El diálogo **Configuración del Radio** (`Settings > Radio Setup...`) proporciona la configuración maestra por radio, con secciones de pestañas para información del radio, red, GPS, TX, Phone/CW, RX, audio, filtros, transverters, cables USB, periféricos, predistorsión adaptativa, temas, certificados anclados de SmartLink y configuraciones de puerto serie.

## Antes de comenzar

- El radio debe estar conectado antes de que la mayoría de las pestañas muestren información en vivo.
- Algunas pestañas (APD, Themes, SmartLink, Serial) se crean de forma diferida y solo aparecen al hacer clic en ellas por primera vez.
- AetherSDR utiliza una clase base `PersistentDialog` que guarda y restaura la geometría de la ventana automáticamente.

## Pasos para abrir

1. Haga clic en **Settings > Radio Setup...** en el menú principal.
2. El diálogo se abre mostrando la pestaña **Radio** de forma predeterminada.
3. Haga clic en cualquier pestaña para acceder a su configuración.

---

## Pestaña Radio

La pestaña **Radio** muestra la identificación del radio, la información de licencia y los controles de actualización de firmware.

### Lectura de la información del radio

- **Radio SN** — Número de serie del chasis (solo lectura). Muestra el serial del chasis si está disponible; de lo contrario, el serial del radio.
- **Region** — Región regulatoria del radio (solo lectura).
- **HW Version** — Cadena de versión del hardware (solo lectura).
- **Model** — Modelo del radio (solo lectura).
- **Options** — Opciones del radio bajo licencia (solo lectura). Muestra la lista de opciones del radio, o un valor predeterminado como "GPS, PGXL" si se detecta un amplificador.
- **FlexControl** — Estado detectado del hardware FlexControl (solo lectura).
- **multiFLEX** — Estado de habilitación de multiFLEX (solo lectura).
- **License Info** — Muestra la suscripción, la fecha de vencimiento, el ID del radio y la versión bajo licencia (solo lectura).

### Copia de la información del radio

Cada valor de solo lectura tiene un pequeño botón de copia a su lado. Haga clic en el botón de copia para copiar el valor al portapapeles. Aparece una breve ventana emergente "¡Copiado!" cerca del botón. El botón de copia está deshabilitado cuando el valor está vacío o muestra "—".

### Configuración de identificación

| Control | Qué hace | Notas |
|---|---|---|
| **Nickname** | Apodo del radio fácil de usar (editable). | — |
| **Callsign** | Indicativo de la estación (editable). | — |
| **Station Name** | Identifica este cliente de AetherSDR para otras estaciones multiFLEX. Se almacena en AppSettings. | Su valor predeterminado es el nombre de host del SO si está vacío. Se envía al radio como 'estación cliente <nombre>'. |

### Actualización de firmware

1. Haga clic en **Check for Update** para consultar las actualizaciones de firmware disponibles. El resultado aparece en la etiqueta de estado. Si hay una actualización disponible, la etiqueta le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Haga clic en **Select Installer...** para abrir un selector de archivos. Seleccione uno de:
   - `.msi` — Instalador de SmartSDR basado en WiX para firmware 4.2+.
   - `.exe` — Instalador de SmartSDR autoextraíble más antiguo.
   - `.ssdr` — Archivo de firmware preextraído.
3. El gestor de firmware detecta el formato del archivo automáticamente y extrae la carga útil `.ssdr`. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción.
4. Una vez completada la extracción, haga clic en **Upload Firmware** para iniciar la carga. Una barra de progreso y una etiqueta de estado muestran el progreso de la carga.

| Control | Qué hace | Notas |
|---|---|---|
| **Check for Update** | Consulta las actualizaciones de firmware disponibles. | Cuando se encuentra una actualización, la etiqueta le indica que descargue el instalador desde flexradio.com. |
| **Select Installer...** | Abre un selector de archivos para archivos `.msi`, `.exe` o `.ssdr`. | Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Inicia la carga del firmware con barra de progreso y estado. | Habilitado solo después de que se completa la extracción. |

### Remote On

Haga clic en **Remote On** para habilitar la funcionalidad de activación remota / encendido remoto en el radio.

---

## Pestaña Network

La pestaña **Network** muestra la información de red del radio y las opciones de red avanzadas.

### Lectura de la información de red

- **IP Address / Mask / MAC Address** — Direcciones de red de solo lectura.

### Configuración de red

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Enforce Private IP Connections:** | Alterne para rechazar pares que no sean RFC1918. | — | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. | 1450 | Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings. |
| **DHCP / Static** | Alterne entre los modos DHCP e IP estática. | — | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — | Habilitado cuando se selecciona el modo Static. |
| **Apply** | Envía la configuración de red al radio. | — | — |

---

## Pestaña GPS

La pestaña **GPS** muestra la presencia de GPS e información en vivo de posición/satélites cuando un receptor GPS está activo.

- Latitud, longitud, altitud, hora y cantidad de satélites (solo lectura).
- Indicador de estado de bloqueo GPS.

---

## Pestaña TX

La pestaña **TX** configura los tiempos de transmisión, los interbloqueos, la potencia máxima, el modo de sintonía, la visualización en waterfall, el seguimiento slice/TX y la Configuración de Banda de TX.

### Configuración de Banda de TX

Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonía por banda.

### Tiempos

Use los cuadros de número en la sección **Timings (in ms)** para establecer los tiempos de retención y retardo de TX.

### Interbloqueos

Alterne **TX REQ: RCA** y **TX REQ: Accessory** para habilitar las entradas de interbloqueo RCA y de accesorio.

### Potencia Máxima

Establezca el límite de potencia de TX a nivel del radio usando el cuadro de número **Max Power:** (0–100%).

### Modo de Sintonía

Seleccione el comportamiento del botón de sintonía en el cuadro combinado **Tune Mode:**.

### Waterfall

Alterne **Show TX in Waterfall:** para dibujar la señal de TX en el waterfall.

### Seguimiento Slice/TX

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **TX Follows Active Slice** | TX sigue el slice activo. | False | Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). | False | Mutuamente excluyente con **TX Follows Active Slice**. |

---

## Pestaña Phone/CW

La pestaña **Phone/CW** configura el micrófono, el manipulador de CW y los valores predeterminados de RTTY.

### Medidor de Nivel

Alterne **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel del micrófono incluso durante la recepción.

### Manipulador de CW

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Iambic:** | Habilita o deshabilita el manipulador iambic en el radio. | — | En v0.9.1, se agregaron los botones Mode A y Mode B junto a la alternancia de habilitación. Mode A = Curtis A; Mode B = Curtis B. |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para el radio como para el manipulador de software local. | A | Par mutuamente excluyente agregado en v0.9.1. |
| **Swap:** | Intercambia dit/dah. | — | — |
| **Sideband:** | Selecciona la banda lateral del tono de CW. | — | Opciones: LSB / USB. |
| **CWX:** | Habilita el tecleo por macros CWX. | — | — |
| **Decode:** | Habilita la superposición de decodificación de CW en el panadapter. | True | Se almacena como `CwDecodeOverlay`. |

### RTTY

Establezca la frecuencia de marca predeterminada de RTTY usando el cuadro de número **RTTY Mark Default:**.

---

## Pestaña RX

La pestaña **RX** proporciona la calibración de compensación de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

### Calibración de frecuencia

La sección de calibración siempre está visible, independientemente de si hay un GPSDO instalado.

- **GPSDO instalado** — se muestra en verde: *GPSDO instalado. Calibración manual de compensación de frecuencia disponible.*
- **Sin GPSDO** — se muestra en ámbar: *Calibración manual de compensación de frecuencia disponible.*

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | Siempre se muestra. |
| **Start** | Inicia el barrido de calibración de frecuencia. | Deshabilitado y etiquetado como **Busy** mientras está activo. Valida que se haya ingresado una frecuencia de calibración. Restablece el error de frecuencia almacenado a cero antes de comenzar. |
| **Freq Offset (ppb):** | Compensación de frecuencia manual en partes por mil millones. | Se restablece a 0 al hacer clic en **Start**. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** se completa dinámicamente según el hardware detectado y el estado del oscilador en vivo.

| Control | Qué hace | Notas |
|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Envía `radio oscillator <valor>` al radio cuando se cambia. | **Auto** siempre está presente. Entradas adicionales: **TCXO**, **GPSDO**, **External 10 MHz**. Las opciones dependen del hardware detectado y del estado del oscilador en vivo. |
| Etiqueta de estado de bloqueo | Muestra la fuente activa, la resolución de Auto y el estado de bloqueo. Se actualiza en vivo. | Verde = Bloqueado; Rojo = Desbloqueado; Gris-azul = esperando estado. Agrega *(no detectado)* cuando External 10 MHz está activa pero no hay señal de referencia externa presente. |

La etiqueta de estado de bloqueo muestra:
- *Esperando estado del oscilador* cuando el estado aún no se ha recibido.
- *Auto -> <fuente resuelta>* cuando Auto está seleccionado y el radio ha resuelto a una fuente específica.
- *<configuración> -> <estado activo>* cuando la configuración y el estado activo difieren.
- Solo el nombre de la fuente activa cuando coinciden.

El estado de bloqueo (*Bloqueado* o *Desbloqueado*) siempre se agrega.

---

## Pestaña Audio

La pestaña **Audio** configura las salidas de audio del radio, la compresión, los dispositivos de PC, el refuerzo, el búfer, la grabación y el contenedor NVIDIA BNR.

### Salidas de audio del radio

| Control | Qué hace | Notas |
|---|---|---|
| **Line Out:** | Control deslizante de ganancia de salida de línea. | — |
| **Mute (Line Out)** | Silencia la salida de línea. | — |
| **Headphone:** | Control deslizante de ganancia de auriculares. | — |
| **Mute (Headphone)** | Silencia los auriculares. | — |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | — |

### Compresión de Audio

Seleccione el códec de audio para SmartLink/LAN usando los botones **Audio Compression (SmartLink):**: **Auto**, **Uncompressed** u **Opus** (predeterminado: Auto). Se almacena como `AudioCompression`.

### Suspensión del sistema

Marque **Prevent system sleep while connected** para mantener el SO despierto mientras el radio está conectado (predeterminado: False). Se almacena como `InhibitSleepWhileConnected`.

### Dispositivos de Audio de PC

Seleccione los dispositivos de entrada y salida de audio del host usando los cuadros combinados **Input:** y **Output:**.

### Refuerzo de Audio

Alterne **Audio Boost:** para habilitar ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`.

### Búfer de Audio

Establezca el campo de texto **Audio Buffer:** para aumentar el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Predeterminado: 200, rango 50–1000 ms. Se almacena como `AudioBufferMs`.

### Grabación

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Recording: Radio Side / Client Side** | Elige la grabación del lado del radio o del lado del cliente. | Radio Side | Se almacena como `RecordingMode`. |
| **Save to:** | Carpeta para grabaciones guardadas (solo del lado del cliente). | Documents/AetherSDR/Recordings | Se almacena como `QsoRecordingDir`. |
| **...** | Navega para buscar la carpeta de grabación. | — | — |
| **Auto-record on TX** | Graba automáticamente mientras se transmite. | False | Se almacena como `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Segundos de silencio antes de que se detenga la grabación. | 120 | Rango 10–3600 seg. Se almacena como `QsoRecordingIdleTimeout`. |

### NVIDIA BNR

Use los controles **NVIDIA BNR** para administrar el contenedor de eliminación de ruido NVIDIA Broadcast:
- **Autostart Container** — Habilita el inicio automático.
- **Start / Stop** — Inicia o detiene el contenedor manualmente.
- **Check Status** — Muestra el estado del contenedor (Running/Stopped/Unknown) con un indicador de punto de color.

---

## Pestaña Filters

La pestaña **Filters** configura opciones de filtro de baja latencia o nítidas por ancho de banda.

### Nitidez del filtro

Para los modos Voice, CW y Digital, use los **controles deslizantes de nitidez de filtro Voice / CW / Digital** para establecer la nitidez del filtro (0 = latencia más baja a 3 = más nítido). El control deslizante está deshabilitado cuando **Auto** está habilitado para ese modo.

### Selección automática de filtro

Alterne **Auto (Voice / CW / Digital)** para habilitar la selección automática del nivel de filtro para ese modo. Cuando está habilitado, el control deslizante de nitidez manual está deshabilitado.

### Baja latencia para modos digitales

Marque **Use Low Latency Filters for Digital Modes** para forzar el uso de filtros de baja latencia en DIGU/DIGL.

---

## Pestaña XVTR

La pestaña **XVTR** administra la configuración por transverter.

### Lista de transverters

La pestaña contiene pestañas anidadas, una por transverter, más una pestaña **'+'** para crear nuevas entradas.

### Controles por transverter

| Control | Qué hace | Notas |
|---|---|---|
| **RX Only:** | Fuerza solo RX en ese transverter. |
