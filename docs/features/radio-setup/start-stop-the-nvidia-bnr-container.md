# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, Phone/CW, RX, antenas, audio, filtros, XVTR, cables USB, periféricos y serial (FlexControl).

## Abriendo el diálogo

1. Asegúrese de que AetherSDR esté conectado a la radio.
2. Haga clic en `Settings > Radio Setup...`.
3. Se abre el diálogo. Puede arrastrar la barra de título para mover el diálogo y usar los bordes de la ventana para redimensionarlo. La geometría del diálogo se conserva entre sesiones.

## Radio (pestaña)

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware.

### Información de radio

| Control                       | Tipo        | Comportamiento                                                                                                                                                                              |
|-------------------------------|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Radio SN**                  | Indicador   | Número de serie del chasis (solo lectura).                                                                                                                                                  |
| **Region**                    | Indicador   | Región regulatoria de la radio (p. ej., USA).                                                                                                                                               |
| **HW Version**                | Indicador   | Cadena de versión del hardware.                                                                                                                                                             |
| **Model**                     | Indicador   | Modelo de la radio.                                                                                                                                                                         |
| **Nickname**                  | Campo de texto | Apodo amigable para la radio.                                                                                                                                                               |
| **Callsign**                  | Campo de texto | Indicativo de la estación.                                                                                                                                                                  |
| **Station Name**              | Campo de texto | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto es el nombre del host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como `client station <name>`. |
| **Remote On**                 | Botón       | Habilita el encendido remoto.                                                                                                                                                               |
| **Options**                   | Indicador   | Muestra las opciones de radio licenciadas.                                                                                                                                                  |
| **FlexControl**               | Indicador   | Estado detectado del hardware FlexControl.                                                                                                                                                  |
| **multiFLEX**                 | Indicador   | Estado de habilitación de multiFLEX.                                                                                                                                                        |
| **License Info**              | Indicador   | Muestra los detalles de la licencia (Suscripción / Expiración / ID de radio / Versión licenciada) desde la radio.                                                                           |

### Actualización de firmware

| Control                | Tipo      | Comportamiento                                                                                                                                                                                                 |
|------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Check for Update**   | Botón     | Consulta al servidor de actualizaciones de FlexRadio para buscar actualizaciones de firmware.                                                                                                                  |
| **Select Installer...** | Botón     | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware**    | Botón     | Inicia la carga del firmware con barra de progreso y estado.                                                                                                                                                   |
| Estado del firmware    | Indicador | Vacío hasta que comienza una carga de firmware; luego muestra el progreso y el texto del resultado.                                                                                                            |

#### Verificando actualizaciones

1. Haga clic en **Check for Update**. AetherSDR consulta al servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado dice "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado dice "Update available: v*x.x.x* — Download the SmartSDR installer from flexradio.com, then click **Select Installer...** to stage it." en ámbar.

#### Preparando y cargando firmware

1. Descargue el instalador de SmartSDR desde flexradio.com si aún no lo tiene localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — Instalador WiX de FlexRadio v4.2+
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El preparador detecta el formato del archivo a partir de los primeros 8 bytes y extrae la carga útil `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparing firmware from *filename*..." mientras la preparación está en curso.
4. Cuando la preparación se complete, haga clic en **Upload Firmware**. Una barra de progreso y una etiqueta de estado siguen el progreso de la carga.

## Network (pestaña)

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

| Control                              | Tipo      | Comportamiento                                                                                                             |
|--------------------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **IP Address / Mask / MAC Address**  | Indicador | Direcciones de red de solo lectura.                                                                                        |
| **Enforce Private IP Connections:**  | Alternar  | Rechaza pares que no sean RFC1918.                                                                                         |
| **Network MTU:**                     | Spinbox   | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes (576-9000, predeterminado 1450). Se almacena en AppSettings como `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static**                    | Alternar  | Cambia entre modos DHCP e IP estática.                                                                                     |
| **IP Address: / Mask: / Gateway:**   | Campos de texto | Campos de configuración de IP estática (habilitados en modo Static).                                                        |
| **Apply**                            | Botón     | Envía la configuración de red a la radio.                                                                                  |

## GPS (pestaña)

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

| Control           | Tipo      | Comportamiento                                         |
|-------------------|-----------|--------------------------------------------------------|
| Información GPS   | Indicador | Datos GPS en vivo cuando hay un módulo GPS instalado y tiene una posición fija. |

## TX (pestaña)

La pestaña TX controla los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall, seguimiento de slice/TX y configuración de banda de TX.

| Control                          | Tipo      | Comportamiento                                                                                                                                                               |
|----------------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX Band Settings**             | Botón     | Abre el diálogo dedicado de potencia/sintonía por banda.                                                                                                                     |
| **Timings**                      | Spinbox   | Temporizaciones de retención/retardo de TX. Consulte los detalles a continuación.                                                                                            |
| **Interlocks - TX REQ: RCA / Accessory** | Alternar  | Habilita las entradas de enclavamiento RCA y de accesorio.                                                                                                                   |
| **Max Power:**                   | Spinbox   | Establece el límite de potencia de TX a nivel de radio (0-100%).                                                                                                             |
| **Tune Mode:**                   | Cuadro combinado | Selecciona cómo se comporta el botón de sintonía.                                                                                                                           |
| **Show TX in Waterfall:**        | Alternar  | Dibuja la señal de TX en el waterfall.                                                                                                                                       |
| **TX Follows Active Slice**      | Botón     | TX sigue la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX**      | Botón     | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |

### Temporizaciones

| Campo          | Unidad de visualización | Unidad de radio | Comportamiento                                                                 |
|----------------|-------------------------|-----------------|--------------------------------------------------------------------------------|
| **ACC TX:**    | milisegundos            | milisegundos    | Retardo después de PTT antes de que comience TX.                               |
| **TX Delay:**  | milisegundos            | milisegundos    | Retardo de retención de TX adicional.                                          |
| **RCA TX1:**   | milisegundos            | milisegundos    | Retardo de enclavamiento RCA TX1.                                              |
| **Timeout:**   | segundos                | milisegundos    | Tiempo de espera de enclavamiento. Se muestra en segundos para facilitar la lectura; se almacena en la radio en milisegundos. El valor ingresado se multiplica por 1000 antes de enviarse. |
| **TX2:**       | milisegundos            | milisegundos    | Segundo retardo de temporización de TX.                                        |

## Phone/CW (pestaña)

La pestaña Phone/CW controla los valores predeterminados del micrófono, el manipulador CW y RTTY.

| Control                                          | Tipo      | Comportamiento                                                                                                                         |
|--------------------------------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------|
| **Enable/Disable the Level Meter During Receive** | Alternar  | Muestra el medidor de nivel de micrófono incluso en RX.                                                                                 |
| **Iambic:**                                      | Alternar  | Habilita o deshabilita el manipulador iámbico en la radio.                                                                             |
| **Iambic Mode: A / B**                           | Par de botones | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Mutuamente excluyentes.        |
| **Swap:**                                        | Alternar  | Intercambia dit/dah.                                                                                                                   |
| **Sideband:**                                    | Cuadro combinado | Selecciona la banda lateral del tono CW (LSB \| USB).                                                                                  |
| **CWX:**                                         | Alternar  | Habilita la activación de macros CWX.                                                                                                  |
| **Decode:**                                      | Alternar  | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`.                    |
| **RTTY Mark Default:**                           | Spinbox   | Frecuencia de marca RTTY predeterminada.                                                                                                |

## RX (pestaña)

La pestaña RX controla la calibración del desplazamiento de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

| Control                         | Tipo      | Comportamiento                                                                                                 |
|---------------------------------|-----------|----------------------------------------------------------------------------------------------------------------|
| **Cal Frequency (MHz):**        | Spinbox   | Frecuencia utilizada para la calibración manual.                                                               |
| **Start**                       | Botón     | Inicia el barrido de calibración de frecuencia.                                                                |
| **Freq Offset (ppb):**          | Spinbox   | Desplazamiento de frecuencia manual en partes por mil millones.                                                |
| **10 MHz Reference Source:**    | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto a la selección y se actualiza en vivo. |

### Calibración de frecuencia

Los controles de calibración de frecuencia están disponibles independientemente de si hay un GPSDO instalado.

Una etiqueta de estado aparece junto a **Start** y proporciona retroalimentación en línea:

| Texto de estado   | Significado                                                             |
|-------------------|-------------------------------------------------------------------------|
| Starting...       | AetherSDR ha enviado los comandos de calibración a la radio.            |
| Busy              | El botón **Start** está deshabilitado; la calibración está en curso.    |
| (texto de error)  | Se informó un problema; verifique el valor en **Cal Frequency (MHz)**.  |

Cuando hay hardware GPSDO presente, la etiqueta en la parte superior del grupo dice "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta dice "Manual frequency offset calibration available." (ámbar).

### 10 MHz Reference Source

El cuadro combinado se completa dinámicamente según lo que informa la radio:

| Entrada              | Se muestra cuando                                                                 |
|----------------------|-----------------------------------------------------------------------------------|
| Auto                 | Siempre presente.                                                                 |
| TCXO                 | La radio informa que hay hardware TCXO presente, o TCXO es la configuración actual o el estado activo. |
| GPSDO                | La radio informa que hay hardware GPSDO presente, o GPSDO es la configuración actual o el estado activo. |
| External 10 MHz      | La radio informa que se detectó una referencia externa, o External es la configuración actual o el estado activo, o se ha recibido el estado del oscilador. |

La etiqueta de estado de bloqueo junto al cuadro muestra el estado actual del oscilador:

| Condición                                      | Texto de la etiqueta (ejemplos)            |
|------------------------------------------------|--------------------------------------------|
| Aún no se ha recibido estado                   | Waiting for oscillator status              |
| Modo Auto, la radio resolvió a una fuente      | Auto -> GPSDO Locked                       |
| La configuración difiere del estado activo      | TCXO -> GPSDO Locked                       |
| La configuración coincide con el estado activo  | GPSDO Locked                               |
| La fuente activa está desbloqueada              | GPSDO Unlocked                             |
| External seleccionado, no se detecta señal      | External 10 MHz Unlocked (not detected)    |

El color de la etiqueta es verde cuando está bloqueada, rojo cuando está desbloqueada y azul grisáceo atenuado antes de que llegue el estado.

#### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)** (por ejemplo, una portadora de WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no puede iniciarse.
5. Haga clic en **Start**. La etiqueta de estado muestra "Starting..." y luego "Busy" mientras se ejecuta el barrido de calibración.
6. Cuando se complete, el campo **Freq Offset (ppb)** se actualiza con el desplazamiento calculado.

## Antennas (pestaña)

La pestaña Antennas le permite asignar nombres amigables a cada puerto de antena de la radio. Esto es útil para identificar qué antena física está conectada a cada puerto.

| Control                  | Tipo      | Comportamiento                                                                 |
|--------------------------|-----------|--------------------------------------------------------------------------------|
| **ANT1 / ANT2 / XVTA / XVTB** | Campo de texto | Asigne un nombre personalizado a cada puerto de antena. El nombre aparece en los controles de selección de antena en toda la aplicación. |

## Audio (pestaña)

La pestaña Audio controla las salidas de audio de la radio, compresión, dispositivos de PC, refuerzo, búfer, grabación y el contenedor NVIDIA BNR.

| Control                                          | Tipo      | Comportamiento                                                                                                                            |
|--------------------------------------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Line Out:**                                    | Deslizador | Ganancia de salida de línea.                                                                                                              |
| **Mute (Line Out)**                              | Botón     | Silencia la salida de línea.                                                                                                              |
| **Headphone:**                                   | Deslizador | Ganancia de auriculares.                                                                                                                  |
| **Mute (Headphone)**                             | Botón     | Silencia los auriculares.                                                                                                                 |
| **Front Speaker: / Mute**                        | Botón     | Silencia el altavoz frontal (específico del modelo).                                                                                      |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón     | Selecciona el códec de audio para SmartLink/LAN. Se almacena en AppSettings como `AudioCompression`.                                      |
| **Prevent system sleep while connected**         | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada para evitar la interrupción de audio/T
