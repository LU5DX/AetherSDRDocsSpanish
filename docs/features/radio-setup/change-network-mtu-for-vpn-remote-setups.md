# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, teléfono/CW, RX, antenas, filtros, XVTR, cables USB, periféricos, serie/FlexControl y temas.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre con la pestaña **Radio** seleccionada.

## Comportamiento general del diálogo

- La geometría del diálogo se conserva entre sesiones usando `PersistentDialog`.
- Los cambios realizados en algunas pestañas se aplican inmediatamente; otras requieren hacer clic en un botón Aplicar o Conectar.
- Si borra un campo IP en la pestaña **Peripherals** y cierra el diálogo sin hacer clic en Connect/Disconnect, la IP y puerto manual guardados se eliminan automáticamente y el dispositivo se desconecta.

## Radio (pestaña)

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

| Control | Descripción | Notas |
|---|---|---|
| **Radio SN** | Número de serie del chasis (solo lectura). | |
| **Region** | Región regulatoria de la radio (solo lectura). | |
| **HW Version** | Cadena de versión de hardware (solo lectura). | |
| **Remote On** | Habilita el encendido remoto. | |
| **Options** | Muestra las opciones de radio licenciadas (solo lectura). | |
| **FlexControl** | Estado detectado del hardware FlexControl (solo lectura). | |
| **multiFLEX** | Estado habilitado de multiFLEX (solo lectura). | |
| **Model** | Modelo de radio (solo lectura). | |
| **Nickname** | Apodo descriptivo de la radio. | |
| **Callsign** | Indicativo de la estación. | |
| **Station Name** | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Usa el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como "client station \<nombre\>". | |
| **License Info** | Muestra detalles de la licencia de la radio: suscripción, expiración, ID de radio y versión licenciada. | |
| **Check for Update** | Consulta actualizaciones de firmware. | |
| **Select Installer...** | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. Vea [Actualización de firmware](#actualizacion-de-firmware-pestana-radio) más abajo. | |
| **Upload Firmware** | Inicia la carga de firmware con barra de progreso y estado. | |

### Actualización de firmware (pestaña Radio)

AetherSDR no descarga firmware automáticamente cuando se detecta una actualización. Descargue el instalador de SmartSDR desde flexradio.com usted mismo, luego prepárelo manualmente.

#### Cómo preparar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, un mensaje de estado le indica la versión disponible y le indica descargar el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — Instalador WiX (FlexRadio SmartSDR v4.2 y posteriores)
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
   - AetherSDR lee el archivo, detecta automáticamente su formato desde los primeros 8 bytes y extrae el contenido `.ssdr` si es necesario. Una etiqueta de estado muestra el progreso.
6. Cuando la preparación se complete y el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso rastrea la carga.
   - No cierre el diálogo ni se desconecte de la radio mientras la carga esté en progreso.

#### Mensajes de estado del firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com, luego haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se necesita acción. |
| Preparing firmware from *nombrearchivo*... | El preparador está leyendo y extrayendo el archivo seleccionado. |
| (texto de error en rojo) | La preparación o carga falló. Verifique que el archivo sea un instalador o archivo de firmware SmartSDR válido e intente nuevamente. |

#### Notas

- El botón **Select Installer...** se etiquetaba como **Browse .ssdr...** en versiones anteriores a v0.9.3.
- La preparación se ejecuta completamente en el cliente; no se requieren herramientas externas para desempaquetar instaladores `.msi` o `.exe`.

## Network (pestaña)

La pestaña Network muestra información de red de la radio y permite configurar opciones de red avanzadas.

| Control | Descripción | Predeterminado |
|---|---|---|
| **IP Address / Mask / MAC Address** | Direcciones de red de solo lectura. | — |
| **Enforce Private IP Connections:** | Rechaza pares no RFC1918. | — |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. Rango 576–9000 bytes. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. | 1450 |
| **DHCP / Static** | Cambia entre modos IP DHCP y Estática. | — |
| **IP Address: / Mask: / Gateway:** | Campos de configuración IP estática. | — |
| **Apply** | Aplica la configuración de red a la radio. | — |

### Cambiar el MTU de red

La configuración de Network MTU controla el tamaño máximo de paquete que la radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce el MTU de ruta disponible.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de selección **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## GPS (pestaña)

La pestaña GPS muestra la presencia de GPS y datos en vivo de latitud, longitud, altitud, hora e información satelital.

| Control | Descripción |
|---|---|
| **GPS status** | Muestra la presencia de GPS y datos de posición en vivo. |

## TX (pestaña)

La pestaña TX controla temporizaciones de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y configuraciones de banda de TX.

| Control | Descripción | Predeterminado |
|---|---|---|
| **TX Band Settings** | Abre el diálogo dedicado de potencia/sintonía por banda. | — |
| **Timings (in ms)** | Temporizaciones de retención/retardo de TX. | — |
| **ACC TX:** | Retardo de ACC TX en milisegundos. | — |
| **TX Delay:** | Retardo de TX en milisegundos. | — |
| **RCA TX1:** | Retardo de RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de enclavamiento en segundos (se muestra en segundos, se almacena en la radio en milisegundos). | — |
| **TX2 Delay:** | Retardo de TX2 en milisegundos. | — |
| **Interlocks - TX REQ: RCA / Accessory** | Habilita las entradas de enclavamiento RCA y accesorio. | — |
| **Max Power:** | Establece el límite de potencia de TX a nivel de radio (0–100%). | — |
| **Tune Mode:** | Selecciona cómo se comporta el botón de sintonía. | — |
| **Show TX in Waterfall:** | Dibuja la señal de TX en el waterfall. | — |
| **TX Follows Active Slice** | TX sigue al slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |

### Campos de temporización TX

Los campos de temporización TX controlan retardos y tiempos de espera para operaciones de transmisión. Note que el campo **Timeout** se muestra en segundos para facilitar la lectura, pero la radio almacena y espera este valor en milisegundos internamente.

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Localice la sección **Timings**.
4. Ingrese el valor deseado en cada campo.
   - ACC TX, TX Delay, RCA TX1 y TX2 Delay están en milisegundos.
   - Timeout está en segundos (rango 0–3600 segundos).
5. Presione Enter o mueva el foco fuera del campo para aplicar el cambio.

## Phone/CW (pestaña)

La pestaña Phone/CW configura los valores predeterminados de micrófono, keyer CW y RTTY.

| Control | Descripción | Predeterminado |
|---|---|---|
| **Enable/Disable the Level Meter During Receive** | Muestra el medidor de nivel de micrófono incluso en RX. | — |
| **Iambic:** | Habilita o deshabilita el keyer iambic en la radio. | Enabled |
| **Iambic Mode: A / B** | Selecciona el modo iambic Curtis A o B tanto para la radio como para el keyer local por software. Par mutuamente excluyente. | A |
| **Swap:** | Intercambia dit/dah. | — |
| **Sideband:** | Selecciona la banda lateral del tono CW (LSB o USB). | — |
| **CWX:** | Habilita la activación de macros CWX. | — |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`. | True |
| **RTTY Mark Default:** | Frecuencia de marca RTTY predeterminada. | — |

## RX (pestaña)

La pestaña RX proporciona calibración de offset de frecuencia GPSDO y selección de fuente de referencia de 10 MHz. Todos los controles de calibración son siempre visibles, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

| Control | Descripción |
|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. |
| **Start** | Inicia el barrido de calibración de frecuencia. La etiqueta del botón cambia a **Busy** mientras el barrido se ejecuta. |
| **Freq Offset (ppb):** | Offset de frecuencia manual en ppb. |
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Las opciones dependen del hardware instalado. Vea la tabla a continuación. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** se llena dinámicamente. Solo aparecen las fuentes compatibles con el hardware conectado. Una etiqueta junto al cuadro combinado muestra la fuente resuelta y el estado de bloqueo.

#### Opciones del cuadro combinado

| Opción | Cuándo se muestra |
|---|---|
| Auto | Siempre. |
| TCXO | Cuando el estado del oscilador ha sido recibido, o cuando la radio reporta `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Cuando la radio reporta `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Cuando el estado del oscilador ha sido recibido, o cuando la radio reporta `extPresent`, o cuando la configuración actual o activa es `external`. |

#### Comportamiento de la etiqueta de estado

- Cuando se selecciona **Auto** y la radio ha elegido una fuente específica, la etiqueta muestra `Auto -> <fuente>`.
- Cuando se selecciona una fuente específica y la radio está usando otra diferente, la etiqueta muestra `<seleccionado> -> <activo>`.
- Cuando la configuración y el estado coinciden, solo se muestra la fuente activa.
- El estado de bloqueo se añade: `Locked` (verde) o `Unlocked` (rojo).
- Si **External 10 MHz** está seleccionado o activo pero no se detecta una referencia externa, la etiqueta añade `(not detected)`.
- Mientras la radio no ha reportado el estado del oscilador, la etiqueta muestra `Waiting for oscillator status` en gris.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida como precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido.
   - La radio primero restablece el error de frecuencia a 0 ppb, luego comienza la secuencia de calibración PLL.
5. Cuando la calibración se completa, el botón se rehabilita y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer el offset manualmente, ingrese un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

#### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido ha sido enviado a la radio. |
| Busy | La calibración PLL está en progreso. |
| Enter cal frequency | El campo Cal Frequency estaba vacío cuando se hizo clic en Start. |

## Antennas (pestaña)

La pestaña Antennas le permite asignar nombres descriptivos a cada puerto de antena en la radio. Esto es útil para identificar qué antena está conectada a cada puerto (ANT1, ANT2, XVTA, XVTB).

| Control | Descripción |
|---|---|
| **ANT1 Name:** | Nombre definido por el usuario para el puerto ANT1. |
| **ANT2 Name:** | Nombre definido por el usuario para el puerto ANT2. |
| **XVTA Name:** | Nombre definido por el usuario para el puerto XVTA. |
| **XVTB Name:** | Nombre definido por el usuario para el puerto XVTB. |

### Cómo establecer nombres de antenas

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Antennas**.
3. Ingrese un nombre descriptivo para cada puerto de antena (ej., "HF Vertical", "40m Dipole", "VHF Beam").
4. Los nombres se guardan en AppSettings y aparecen en los controles de selección de antena en toda la aplicación.

## Audio (pestaña)

La pestaña Audio configura las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer y grabación.
