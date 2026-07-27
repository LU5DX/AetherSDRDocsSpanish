# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información de radio, red, GPS, TX, Phone/CW, RX, antenas, audio, filtros, XVTR, cables USB, periféricos, APD (Predistorsión Adaptativa), Temas, SmartLink (certificados anclados) y serie (FlexControl).

## Abrir el diálogo

1. Asegúrese de que AetherSDR esté conectado a la radio.
2. Haga clic en `Settings > Radio Setup...`.
3. Se abre el diálogo. Puede arrastrar la barra de título para mover el diálogo y usar los bordes de la ventana para redimensionarlo. La geometría del diálogo se conserva entre sesiones.

Si una pestaña contiene más controles de los que caben verticalmente (por ejemplo, en pantallas pequeñas o de alta densidad de píxeles), aparece una barra de desplazamiento dentro de esa pestaña. El diálogo en sí no crece más allá del borde de la pantalla.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware. Cada valor de solo lectura tiene un pequeño botón de copia a su derecha: haga clic para copiar el valor al portapapeles.

### Información de radio

| Control                                             | Tipo                                                                                                                                                                                        | Comportamiento                                                                                                                                                                              |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Radio SN**                                        | Indicador                                                                                                                                                                                   | Número de serie del chasis (solo lectura).                                                                                                                                                    |
| **Region**                                          | Indicador                                                                                                                                                                                   | Región regulatoria de la radio (ej. USA).                                                                                                                                                  |
| **HW Version**                                      | Indicador                                                                                                                                                                                   | Cadena de versión de hardware.                                                                                                                                                              |
| **Model**                                           | Indicador                                                                                                                                                                                   | Modelo de radio.                                                                                                                                                                          |
| **Nickname**                                        | Campo de texto                                                                                                                                                                                  | Apodo de radio fácil de usar.                                                                                                                                                         |
| **Callsign**                                        | Campo de texto                                                                                                                                                                                  | Indicativo de la estación.                                                                                                                                                                     |
| **Station Name**                                    | Campo de texto                                                                                                                                                                                  | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. Por defecto es el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como `client station <name>`. |
| **Remote On**                                       | Botón                                                                                                                                                                                      | Habilita el encendido remoto / wake remoto.                                                                                                                                                      |
| **Options**                                         | Indicador                                                                                                                                                                                   | Muestra las opciones de radio licenciadas.                                                                                                                                                         |
| **FlexControl**                                     | Indicador                                                                                                                                                                                   | Estado detectado del hardware FlexControl.                                                                                                                                               |
| **multiFLEX**                                       | Indicador                                                                                                                                                                                   | Estado habilitado de multiFLEX.                                                                                                                                                              |
| **License Info**                                    | Indicador                                                                                                                                                                                   | Muestra los detalles de la licencia (Suscripción / Vencimiento / ID de radio / Versión licenciada) desde la radio.                                                                                    |
| **Reboot:**                                         | Botón + confirmación                                                                                                                                                                       | Reinicia la radio conectada. Vea "Reiniciar la radio" más abajo.                                                                                                                         |
| Select Installer...                                 | Abre un diálogo de archivos para un instalador de SmartSDR (.msi, .exe) o un archivo de firmware .ssdr preextraído. Pasa la ruta seleccionada a FirmwareStager que extrae la carga útil .ssdr y emite progreso. | La etiqueta cambió de 'Browse .ssdr...' a 'Select Installer...' en v26.5.3.                                                                                                             |
| SmartLink (pestaña)                                     | Gestión de certificados TLS de SmartLink anclados. Lista cada certificado anclado (host, huella SHA-256, fecha de anclaje) con opciones Forget y Forget All por fila. Nuevo en v26.5.3 (#2951 Phase 2).     | Se construye de forma diferida al hacer clic por primera vez. Fase 2 de GHSA-wfx7-w6p8-4jr2: la discrepancia de anclaje de certificado ahora pausa firmemente el handshake con un diálogo modal.                                                   |
| Pinned SmartLink Certificates (sección)             | Encabezado de sección para la tabla de certificados anclados dentro de la pestaña SmartLink. Lista cada host que este cliente ha anclado en la primera conexión (confianza en el primer uso).                                          | Fase 2 de GHSA-wfx7-w6p8-4jr2. El esquema de anclaje migró de cadenas simples a objetos {fp, pinnedAt}.                                                                                     |
| Host / SHA-256 fingerprint / Pinned (columnas de tabla) | Tabla de solo lectura de 3 columnas: Host (nombre de host), huella SHA-256 (monoespaciada), Anclado (AAAA-MM-DD o '(pre-phase 2)').                                                                         | Respaldado por WanCertCache en WanConnection.cpp.                                                                                                                                          |
| Forget selected                                     | Elimina la huella del certificado anclado del host seleccionado para que la siguiente conexión lo vuelva a anclar silenciosamente.                                                                                                   |                                                                                                                                                                                       |
| Forget all                                          | Limpia todos los certificados anclados (con confirmación). La siguiente conexión a cada radio los vuelve a anclar silenciosamente.                                                                                                  | Muestra QMessageBox::question antes de borrar.                                                                                                                                           |
#### Reiniciar la radio

1. Haga clic en **Reboot Radio**.
2. Aparece un diálogo de confirmación:
   - **Sesión SmartLink/WAN**: El mensaje dice "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente una vez que la radio termine de iniciarse."
   - **Sesión local**: El mensaje dice "AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciarse."
3. Haga clic en **OK** para confirmar. El diálogo se cierra y AetherSDR se desconecta. En conexiones locales, la reconexión ocurre automáticamente.
4. El botón se deshabilita cuando la radio está desconectada.

### Actualización de firmware

| Control                | Tipo      | Comportamiento                                                                                                                                                                                                 |
|------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Check for Update**   | Botón    | Consulta al servidor de actualizaciones de FlexRadio en busca de actualizaciones de firmware.                                                                                                                                                |
| **Select Installer...** | Botón    | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El stagedor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware**    | Botón    | Inicia la carga del firmware con barra de progreso y estado.                                                                                                                                                     |
| Firmware status        | Indicador | Vacío hasta que comienza una carga de firmware, luego muestra progreso y texto de resultado.                                                                                                                                     |

#### Verificar actualizaciones

1. Haga clic en **Check for Update**. AetherSDR consulta al servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra "Update available: v*x.x.x* — Download the SmartSDR installer from flexradio.com, then click **Select Installer...** to stage it." en ámbar.

#### Preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com si aún no lo tiene localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — Instalador WiX de FlexRadio v4.2+
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El stagedor detecta el formato del archivo a partir de los primeros 8 bytes y extrae la carga útil `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparing firmware from *filename*..." mientras la preparación está en curso.
4. Cuando la preparación finalice, haga clic en **Upload Firmware**. Una barra de progreso y una etiqueta de estado siguen la carga.

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

| Control                              | Tipo      | Comportamiento                                                                                                             |
|--------------------------------------|-----------|----------------------------------------------------------------------------------------------------------------------|
| **IP Address / Mask / MAC Address**  | Indicador | Direcciones de red de solo lectura.                                                                                         |
| **Enforce Private IP Connections:**  | Alternar    | Rechaza pares que no sean RFC1918.                                                                                           |
| **Network MTU:**                     | Spinbox   | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes (576-9000, valor predeterminado 1450). Se almacena en AppSettings como `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static**                    | Alternar    | Cambia entre modos de IP DHCP y estática.                                                                           |
| **IP Address: / Mask: / Gateway:**   | Campos de texto | Campos de configuración de IP estática (habilitados en modo Static).                                                            |
| **Apply**                            | Botón    | Envía la configuración de red a la radio.                                                                       |

## Pestaña GPS

La pestaña GPS muestra la presencia de GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

| Control           | Tipo      | Comportamiento                                         |
|-------------------|-----------|--------------------------------------------------|
| GPS information   | Indicador | Datos GPS en vivo cuando un módulo GPS está instalado y tiene una posición fija. |

## Pestaña TX

La pestaña TX controla los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en waterfall, seguimiento slice/TX y Configuración de Banda TX.

| Control                          | Tipo      | Comportamiento                                                                                                                                                               |
|----------------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX Band Settings**             | Botón    | Abre el diálogo dedicado de potencia/sintonía por banda.                                                                                                                        |
| **Timings**                      | Spinbox   | Tiempos de retención/retardo de TX. Vea las sutilezas a continuación.                                                                                                                         |
| **Interlocks - TX REQ: RCA / Accessory** | Alternar    | Habilita las entradas de enclavamiento RCA y accessory.                                                                                                                            |
| **Max Power:**                   | Spinbox   | Establece el límite de potencia de TX a nivel de radio (0-100%).                                                                                                                                |
| **Tune Mode:**                   | Combo box | Selecciona cómo se comporta el botón de sintonía.                                                                                                                                   |
| **Show TX in Waterfall:**        | Alternar    | Dibuja la señal de TX en el waterfall.                                                                                                                                      |
| **TX Follows Active Slice**      | Botón    | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX**      | Botón    | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |

### Tiempos

| Campo          | Unidad de visualización | Unidad de radio          | Comportamiento                                                                 |
|----------------|--------------|---------------------|--------------------------------------------------------------------------|
| **ACC TX:**    | milisegundos | milisegundos        | Retardo después de PTT antes de que comience TX.                                        |
| **TX Delay:**  | milisegundos | milisegundos        | Retardo de retención de TX adicional.                                                 |
| **RCA TX1:**   | milisegundos | milisegundos        | Retardo de enclavamiento RCA TX1.                                                  |
| **Timeout:**   | segundos      | milisegundos        | Tiempo de espera de enclavamiento. Se muestra en segundos para legibilidad; se almacena en la radio en milisegundos. El valor ingresado se multiplica por 1000 antes de enviarlo. |
| **TX2:**       | milisegundos | milisegundos        | Segundo retardo de tiempo de TX.                                                   |

## Pestaña Phone/CW

La pestaña Phone/CW controla los valores predeterminados del micrófono, keyer CW y RTTY.

| Control                                          | Tipo      | Comportamiento                                                                                                                         |
|--------------------------------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| **Enable/Disable the Level Meter During Receive** | Alternar    | Muestra el medidor de nivel de micrófono incluso en RX.                                                                                                |
| **Iambic:**                                      | Alternar    | Habilita o deshabilita el keyer iámbico en la radio.                                                                               |
| **Iambic Mode: A / B**                           | Par de botones | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el keyer de software local. Mutuamente excluyentes.                          |
| **Swap:**                                        | Alternar    | Intercambia dit/dah.                                                                                                                   |
| **Sideband:**                                    | Combo box | Selecciona la banda lateral del tono CW (LSB \| USB).                                                                                          |
| **CWX:**                                         | Alternar    | Habilita el keying de macros CWX.                                                                                                        |
| **Decode:**                                      | Alternar    | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`.                                     |
| **RTTY Mark Default:**                           | Spinbox   | Frecuencia de marca RTTY predeterminada.                                                                                                      |

## Pestaña RX

La pestaña RX controla la calibración del offset de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

| Control                         | Tipo      | Comportamiento                                                                                                 |
|---------------------------------|-----------|----------------------------------------------------------------------------------------------------------|
| **Cal Frequency (MHz):**        | Spinbox   | Frecuencia utilizada para la calibración manual.                                                                   |
| **Start**                       | Botón    | Inicia el barrido de calibración de frecuencia.                                                                  |
| **Freq Offset (ppb):**          | Spinbox   | Offset de frecuencia manual en partes por billón.                                                            |
| **10 MHz Reference Source:**    | Combo box | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto a la opción y se actualiza en vivo. |

### Calibración de frecuencia

Los controles de calibración de frecuencia están disponibles independientemente de si hay un GPSDO instalado.

Una etiqueta de estado aparece junto a **Start** y proporciona retroalimentación en línea:

| Texto de estado       | Significado                                                                 |
|-----------------------|----------------------------------------------------------------------------|
| Starting...           | AetherSDR ha enviado los comandos de calibración a la radio.               |
| Busy                  | El botón **Start** está deshabilitado; la calibración está en curso.           |
| (texto de error)      | Se reportó un problema; verifique el valor en **Cal Frequency (MHz)**.     |

Cuando hay hardware GPSDO presente, la etiqueta en la parte superior del grupo dice "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO la etiqueta dice "Manual frequency offset calibration available." (ámbar).

### 10 MHz Reference Source

El combo box se llena dinámicamente según lo que reporte la radio:

| Entrada                | Se muestra cuando                                                                 |
|------------------------|-----------------------------------------------------------------------------------|
| Auto                   | Siempre presente.                                                            |
| TCXO                   | La radio reporta hardware TCXO presente, o TCXO
