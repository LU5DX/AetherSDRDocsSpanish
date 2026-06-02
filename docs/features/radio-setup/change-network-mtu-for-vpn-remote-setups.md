# Diálogo de configuración de la radio

El diálogo de configuración de la radio es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, teléfono/CW, RX, antenas, filtros, XVTR, cables USB, periféricos, serie/FlexControl y temas.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

## Comportamiento general del diálogo

- La geometría del diálogo se conserva entre sesiones usando `PersistentDialog`.
- Los cambios realizados en algunas pestañas se aplican inmediatamente; otras requieren hacer clic en un botón Aplicar o Conectar.
- Si borra un campo IP en la pestaña **Peripherals** y cierra el diálogo sin hacer clic en Connect/Disconnect, la IP y el puerto manuales guardados se eliminan automáticamente y el dispositivo se desconecta.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, datos de licencia y controles de actualización de firmware.

| Control | Descripción | Notas |
|---|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). | Haga clic en el botón de copiar para copiar el número de serie al portapapeles. |
| **Region** | Región normativa de la radio (solo lectura). | |
| **HW Version** | Versión del hardware (solo lectura). | Haga clic en el botón de copiar para copiar la cadena de versión al portapapeles. |
| **Remote On** | Habilita el encendido remoto / remote-on. | |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). | |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). | |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). | |
| **Model** | Modelo de la radio (solo lectura). | |
| **Nickname** | Apodo descriptivo de la radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Usa el nombre del SO si está vacío. | Almacenado en AppSettings como `StationName`. Enviado a la radio como "client station \<nombre\>". |
| **License Info** | Muestra los detalles de licencia de la radio: suscripción, vencimiento, ID de radio y versión licenciada. | |
| **Check for Update** | Consulta si hay actualizaciones de firmware. | |
| **Browse .ssdr...** | Selecciona un archivo de imagen de firmware. | |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. | |

### Valores copiables (pestaña Radio)

Los campos Radio SN y HW Version muestran un pequeño botón de copiar al pasar el ratón o al enfocarlos. Al hacer clic en el botón, se copia el valor mostrado al portapapeles del sistema y aparece un breve mensaje "¡Copiado!" cerca del botón.

### Actualización de firmware (pestaña Radio)

AetherSDR no descarga firmware automáticamente cuando se detecta una actualización. Descargue el instalador de SmartSDR desde flexradio.com usted mismo, luego prepárelo manualmente.

#### Preparar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, un mensaje de estado le indica la versión disponible y le dirige a descargar el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — Instalador WiX (FlexRadio SmartSDR v4.2 y posteriores)
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
5. Haga clic en **Browse .ssdr...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
6. Cuando el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso sigue la carga.
   - No cierre el diálogo ni se desconecte de la radio mientras la carga esté en progreso.

#### Mensajes de estado del firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com, luego haga clic en **Browse .ssdr...**. |
| Firmware is up to date (v*x.y.z*) | No se requiere acción. |
| (texto de error en rojo) | La carga falló. Verifique que el archivo sea un archivo de firmware SmartSDR válido e intente de nuevo. |

## Pestaña Network

La pestaña Network muestra la información de red de la radio y permite configurar opciones de red avanzadas.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. | — |
| **Enforce Private IP Connections:** | Rechaza pares que no sean RFC1918. | — |
| **Network MTU:** | Establece el tamaño máximo del paquete VITA-49 UDP saliente en bytes. Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Almacenado en AppSettings como `NetworkMtu`. | 1450 |
| **DHCP / Static** | Cambia entre modos DHCP e IP estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración de IP estática. | — |
| **Apply** | Aplica la configuración de red a la radio. | — |

### Cambiar el MTU de red

El ajuste Network MTU controla el tamaño máximo de paquete que la radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce el MTU de ruta disponible.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de número **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS y la latitud, longitud, altitud, hora e información de satélites en vivo.

| Control | Descripción |
|---|---|
| **GPS status** | Muestra la presencia de GPS y los datos de posición en vivo. |

## Pestaña TX

La pestaña TX controla los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y configuración de banda de TX.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | — |
| **Timings (in ms)** | Tiempos de colgado/retardo de TX. | — |
| **ACC TX:** | Retardo de ACC TX en milisegundos. | — |
| **TX Delay:** | Retardo de TX en milisegundos. | — |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento en segundos (se muestra en segundos, se almacena en la radio en milisegundos). | — |
| **TX2 Delay:** | Retardo de TX2 en milisegundos. | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y accessory. | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0–100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante la operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |

### Campos de temporización TX

Los campos de temporización TX controlan los retardos y tiempos de espera para las operaciones de transmisión. Tenga en cuenta que el campo **Timeout** se muestra en segundos para facilitar la lectura, pero la radio almacena y espera este valor en milisegundos internamente.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Localice la sección **Timings**.
4. Introduzca el valor deseado en cada campo.
   - ACC TX, TX Delay, RCA TX1 y TX2 Delay están en milisegundos.
   - Timeout está en segundos (rango 0–3600 segundos).
5. Presione Enter o mueva el foco fuera del campo para aplicar el cambio.

## Pestaña Phone/CW

La pestaña Phone/CW configura el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. | Enabled |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador local de software. Par mutuamente excluyente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW (LSB o USB). | — |
| **CWX:** | Habilita el keying de macros CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Almacenado en AppSettings como `CwDecodeOverlay`. | True |
| **RTTY Mark Default:** | Frecuencia predeterminada de marca RTTY. | — |

## Pestaña RX

La pestaña RX proporciona calibración de desplazamiento de frecuencia del GPSDO y selección de fuente de referencia de 10 MHz. Todos los controles de calibración son siempre visibles, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

| Control | Descripción |
|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. |
| **Start** | Inicia el barrido de calibración de frecuencia. La etiqueta del botón cambia a **Busy** mientras se ejecuta el barrido. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en ppb. |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. Consulte la tabla a continuación. |

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** se completa dinámicamente. Solo aparecen las fuentes compatibles con el hardware conectado. Una etiqueta junto al cuadro combinado muestra la fuente resuelta y el estado de bloqueo.

#### Opciones del cuadro combinado

| Opción | Cuándo se muestra |
|---|---|
| Auto | Siempre. |
| TCXO | Cuando se ha recibido el estado del oscilador, o cuando la radio informa `tcxoPresent`, o cuando el ajuste actual o activo es `tcxo`. |
| GPSDO | Cuando la radio informa `gpsdoPresent`, o cuando el ajuste actual o activo es `gpsdo`. |
| External 10 MHz | Cuando se ha recibido el estado del oscilador, o cuando la radio informa `extPresent`, o cuando el ajuste actual o activo es `external`. |

#### Comportamiento de la etiqueta de estado

- Cuando **Auto** está seleccionado y la radio ha elegido una fuente específica, la etiqueta muestra `Auto -> <fuente>`.
- Cuando se selecciona una fuente específica y la radio está usando una diferente, la etiqueta muestra `<seleccionada> -> <activa>`.
- Cuando el ajuste y el estado coinciden, solo se muestra la fuente activa.
- El estado de bloqueo se añade: `Locked` (verde) o `Unlocked` (rojo).
- Si **External 10 MHz** está seleccionado o activo pero no se detecta ninguna referencia externa, la etiqueta añade `(not detected)`.
- Mientras la radio no haya informado el estado del oscilador, la etiqueta muestra `Waiting for oscillator status` en gris.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido.
   - La radio primero restablece el error de frecuencia a 0 ppb, luego comienza la secuencia de calibración PLL.
5. Cuando la calibración se completa, el botón se habilita nuevamente y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer el desplazamiento manualmente, introduzca un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

#### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido se ha enviado a la radio. |
| Busy | La calibración PLL está en progreso. |
| Enter cal frequency | El campo Cal Frequency estaba vacío cuando se hizo clic en Start. |

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres descriptivos a cada puerto de antena de la radio. Esto es útil para identificar qué antena está conectada a cada puerto (ANT1, ANT2, XVTA, XVTB).

| Control | Descripción |
|---|---|
| **ANT1 Name:** | Nombre definido por el usuario para el puerto ANT1. |
| **ANT2 Name:** | Nombre definido por el usuario para el puerto ANT2. |
| **XVTA Name:** | Nombre definido por el usuario para el puerto XVTA. |
| **XVTB Name:** | Nombre definido por el usuario para el puerto XVTB. |

### Configurar nombres de antenas

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Antennas**.
3. Introduzca un nombre descriptivo para cada puerto de antena (p. ej., "HF Vertical", "40m Dipole", "VHF Beam").
4. Los nombres se guardan en AppSettings y aparecen en los controles de selección de antena en toda la aplicación.

## Pestaña Audio

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, ganancia, búfer, grabación y el contenedor NVIDIA BNR.

| Control | Descripción | Valor predeterminado | Notas |
|---|---|---|---|
| **Line Out:** | Ganancia de salida de línea. | — | |
| **Mute (Line Out)** | Silencia la salida de línea. | — | |
| **Headphone:** | Ganancia de auriculares. | — | |
| **Mute (Headphone)** | Silencia los auriculares. | — | |
| **Front Speaker: / Mute** | Silencia el altavoz frontal (específico del modelo). | — | |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink
