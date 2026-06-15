# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio (`Settings > Radio Setup...`) es la ventana maestra de configuración por radio. Contiene pestañas para información de la radio, red, GPS, TX, Phone/CW, RX, antenas, audio, filtros, XVTR, cables USB, periféricos, APD (Predistorsión Adaptativa), Temas, SmartLink (certificados anclados) y serie (FlexControl).

## Abrir el diálogo

1. Asegúrese de que AetherSDR esté conectado a la radio.
2. Haga clic en `Settings > Radio Setup...`.
3. Se abre el diálogo. Puede arrastrar la barra de título para mover el diálogo y usar los bordes de la ventana para redimensionarlo. La geometría del diálogo se conserva entre sesiones.

Si una pestaña contiene más controles de los que caben verticalmente (por ejemplo, en pantallas pequeñas o de alta densidad de píxeles), aparece una barra de desplazamiento dentro de esa pestaña. El diálogo en sí no crece más allá del borde de la pantalla.

## Pestaña Radio

La pestaña Radio muestra información de la radio, identificación, información de licencia y controles de actualización de firmware. Cada valor de solo lectura tiene un pequeño botón de copia a su derecha: haga clic para copiar el valor al portapapeles.

### Información de la radio

| Control                                             | Tipo                                                                                                                                                                                        | Comportamiento                                                                                                                                                                              |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Radio SN**                                        | Indicador                                                                                                                                                                                   | Número de serie del chasis (solo lectura).                                                                                                                                                    |
| **Region**                                          | Indicador                                                                                                                                                                                   | Región regulatoria de la radio (ej. USA).                                                                                                                                                  |
| **HW Version**                                      | Indicador                                                                                                                                                                                   | Cadena de versión de hardware.                                                                                                                                                              |
| **Model**                                           | Indicador                                                                                                                                                                                   | Modelo de la radio.                                                                                                                                                                          |
| **Nickname**                                        | Campo de texto                                                                                                                                                                                  | Apodo amigable de la radio.                                                                                                                                                         |
| **Callsign**                                        | Campo de texto                                                                                                                                                                                  | Indicativo de la estación.                                                                                                                                                                     |
| **Station Name**                                    | Campo de texto                                                                                                                                                                                  | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Por defecto toma el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`. Se envía a la radio como `client station <name>`. |
| **Remote On**                                       | Botón                                                                                                                                                                                      | Habilita el encendido remoto.                                                                                                                                                      |
| **Options**                                         | Indicador                                                                                                                                                                                   | Muestra las opciones de radio licenciadas.                                                                                                                                                         |
| **FlexControl**                                     | Indicador                                                                                                                                                                                   | Estado detectado del hardware FlexControl.                                                                                                                                               |
| **multiFLEX**                                       | Indicador                                                                                                                                                                                   | Estado habilitado de multiFLEX.                                                                                                                                                              |
| **License Info**                                    | Indicador                                                                                                                                                                                   | Muestra los detalles de la licencia (Suscripción / Vencimiento / ID de radio / Versión licenciada) desde la radio.                                                                                    |
| **Reboot:**                                         | Botón + confirmación                                                                                                                                                                       | Reinicia la radio conectada. Consulte "Reiniciar la radio" abajo.                                                                                                                         |

#### Reiniciar la radio

1. Haga clic en **Reboot Radio**.
2. Aparece un diálogo de confirmación:
   - **Sesión SmartLink/WAN**: El mensaje dice "AetherSDR se desconectará. Las sesiones SmartLink/WAN no se reconectan automáticamente hoy; deberá reconectarse manualmente una vez que la radio termine de iniciar."
   - **Sesión local**: El mensaje dice "AetherSDR se desconectará y se reconectará automáticamente una vez que la radio termine de iniciar."
3. Haga clic en **OK** para confirmar. El diálogo se cierra y AetherSDR se desconecta. En conexiones locales, la reconexión ocurre automáticamente.
4. El botón está deshabilitado cuando la radio está desconectada.

### Actualización de firmware

| Control                | Tipo      | Comportamiento                                                                                                                                                                                                 |
|------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Check for Update**   | Botón    | Consulta el servidor de actualizaciones de FlexRadio en busca de actualizaciones de firmware.                                                                                                                                                |
| **Select Installer...** | Botón    | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes y extrae el `.ssdr` sin herramientas externas. |
| **Upload Firmware**    | Botón    | Inicia la carga del firmware con barra de progreso y estado.                                                                                                                                                     |
| Estado del firmware        | Indicador | Vacío hasta que comienza una carga de firmware, luego muestra texto de progreso y resultado.                                                                                                                                     |

#### Buscar actualizaciones

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado dice "El firmware está actualizado (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado dice "Actualización disponible: v*x.x.x* — Descargue el instalador de SmartSDR desde flexradio.com, luego haga clic en **Select Installer...** para prepararlo." en ámbar.

#### Preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com si no lo tiene ya localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — Instalador WiX de FlexRadio v4.2+
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El preparador detecta el formato del archivo a partir de los primeros 8 bytes y extrae el contenido `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparando firmware desde *nombre de archivo*..." mientras se realiza la preparación.
4. Cuando la preparación se complete, haga clic en **Upload Firmware**. Una barra de progreso y una etiqueta de estado realizan el seguimiento de la carga.

## Pestaña Network

La pestaña Network muestra información de red de la radio y opciones de red avanzadas.

| Control                              | Tipo      | Comportamiento                                                                                                             |
|--------------------------------------|-----------|----------------------------------------------------------------------------------------------------------------------|
| **IP Address / Mask / MAC Address**  | Indicador | Direcciones de red de solo lectura.                                                                                         |
| **Enforce Private IP Connections:**  | Alternar    | Rechaza pares que no sean RFC1918.                                                                                           |
| **Network MTU:**                     | Spinbox   | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes (576-9000, por defecto 1450). Se almacena en AppSettings como `NetworkMtu`. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. |
| **DHCP / Static**                    | Alternar    | Cambia entre modos DHCP e IP estática.                                                                           |
| **IP Address: / Mask: / Gateway:**   | Campos de texto | Campos de configuración de IP estática (habilitados en modo Static).                                                            |
| **Apply**                            | Botón    | Envía la configuración de red a la radio.                                                                       |

## Pestaña GPS

La pestaña GPS muestra la presencia del GPS e información en vivo de latitud/longitud/altitud/hora/satélites.

| Control           | Tipo      | Comportamiento                                         |
|-------------------|-----------|--------------------------------------------------|
| Información GPS   | Indicador | Datos GPS en vivo cuando hay un módulo GPS instalado y tiene una fijación. |

## Pestaña TX

La pestaña TX controla los tiempos de TX, enclavamientos, potencia máxima, modo de sintonía, visualización en el waterfall, seguimiento de slice/TX y Configuración de Banda TX.

| Control                          | Tipo      | Comportamiento                                                                                                                                                               |
|----------------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX Band Settings**             | Botón    | Abre el diálogo dedicado de potencia/sintonía por banda.                                                                                                                        |
| **Timings**                      | Spinbox   | Tiempos de espera / retardo de TX. Consulte las sutilezas abajo.                                                                                                                         |
| **Interlocks - TX REQ: RCA / Accessory** | Alternar    | Habilita las entradas de enclavamiento RCA y accessory.                                                                                                                            |
| **Max Power:**                   | Spinbox   | Establece el límite de potencia de TX a nivel de radio (0-100%).                                                                                                                                |
| **Tune Mode:**                   | Combo box | Selecciona cómo se comporta el botón de sintonía.                                                                                                                                   |
| **Show TX in Waterfall:**        | Alternar    | Dibuja la señal de TX en el waterfall.                                                                                                                                      |
| **TX Follows Active Slice**      | Botón    | TX sigue al slice activo. Excluyente mutuamente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena en AppSettings como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX**      | Botón    | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Excluyente mutuamente con **TX Follows Active Slice**. Se almacena en AppSettings como `ActiveFollowsTxSlice`. |

### Timings

| Campo          | Unidad mostrada | Unidad de radio          | Comportamiento                                                                 |
|----------------|--------------|---------------------|--------------------------------------------------------------------------|
| **ACC TX:**    | milisegundos | milisegundos        | Retardo después de PTT antes de que comience TX.                                        |
| **TX Delay:**  | milisegundos | milisegundos        | Retardo adicional de mantenimiento de TX.                                                 |
| **RCA TX1:**   | milisegundos | milisegundos        | Retardo de enclavamiento RCA TX1.                                                  |
| **Timeout:**   | segundos      | milisegundos        | Tiempo de espera de enclavamiento. Se muestra en segundos para legibilidad; se almacena en la radio en milisegundos. El valor ingresado se multiplica por 1000 antes de enviar. |
| **TX2:**       | milisegundos | milisegundos        | Segundo retardo de temporización de TX.                                                   |

## Pestaña Phone/CW

La pestaña Phone/CW controla el micrófono, el manipulador CW y los valores predeterminados de RTTY.

| Control                                          | Tipo      | Comportamiento                                                                                                                         |
|--------------------------------------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| **Enable/Disable the Level Meter During Receive** | Alternar    | Muestra el medidor de nivel de micrófono incluso en RX.                                                                                                |
| **Iambic:**                                      | Alternar    | Activa o desactiva el manipulador iambic en la radio.                                                                               |
| **Iambic Mode: A / B**                           | Par de botones | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. Excluyente mutuamente.                          |
| **Swap:**                                        | Alternar    | Intercambia dit/dah.                                                                                                                   |
| **Sideband:**                                    | Combo box | Selecciona la banda lateral del tono CW (LSB \| USB).                                                                                          |
| **CWX:**                                         | Alternar    | Habilita el activación por macros CWX.                                                                                                        |
| **Decode:**                                      | Alternar    | Habilita la superposición de decodificación CW en el panadapter. Se almacena en AppSettings como `CwDecodeOverlay`.                                     |
| **RTTY Mark Default:**                           | Spinbox   | Frecuencia de marca RTTY predeterminada.                                                                                                      |

## Pestaña RX

La pestaña RX controla la calibración del desplazamiento de frecuencia del GPSDO y la selección de la fuente de referencia de 10 MHz.

| Control                         | Tipo      | Comportamiento                                                                                                 |
|---------------------------------|-----------|----------------------------------------------------------------------------------------------------------|
| **Cal Frequency (MHz):**        | Spinbox   | Frecuencia utilizada para la calibración manual.                                                                   |
| **Start**                       | Botón    | Inicia el barrido de calibración de frecuencia.                                                                  |
| **Freq Offset (ppb):**          | Spinbox   | Desplazamiento de frecuencia manual en partes por mil millones.                                                            |
| **10 MHz Reference Source:**    | Combo box | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto y se actualiza en vivo. |

### Calibración de frecuencia

Los controles de calibración de frecuencia están disponibles independientemente de si hay un GPSDO instalado.

Aparece una etiqueta de estado junto a **Start** y proporciona comentarios en línea:

| Texto de estado       | Significado                                                                 |
|-------------------|-------------------------------------------------------------------------|
| Starting...       | AetherSDR ha enviado los comandos de calibración a la radio.               |
| Busy              | El botón **Start** está deshabilitado; la calibración está en progreso.           |
| (texto de error)      | Se informó un problema; verifique el valor en **Cal Frequency (MHz)**.     |

Cuando hay hardware GPSDO presente, la etiqueta en la parte superior del grupo dice "GPSDO instalado. Calibración manual de desplazamiento de frecuencia disponible." (verde). Sin GPSDO, la etiqueta dice "Calibración manual de desplazamiento de frecuencia disponible." (ámbar).

### Fuente de Referencia de 10 MHz

El combobox se completa dinámicamente según lo que informa la radio:

| Entrada                | Se muestra cuando                                                                 |
|----------------------|----------------------------------------------------------------------------|
| Auto                 | Siempre presente.                                                            |
| TCXO                 | La radio informa que hay hardware TCXO presente, o TCXO es la configuración actual o el estado activo. |
| GPSDO                | La radio informa que hay hardware GPSDO presente, o GPSDO es la configuración actual o el estado activo. |
| External 10 MHz      | La radio informa que se detectó una referencia externa, o External es la configuración actual o el estado activo, o se ha recibido el estado del oscilador. |

La etiqueta de estado de bloqueo junto al combobox muestra el estado actual del oscilador:

| Condición                                      | Texto de la etiqueta (ejemplos)               |
|------------------------------------------------|-------------------------------------|
| Aún no se ha recibido ningún estado                         | Esperando estado del oscilador       |
| Modo Auto, la radio se resolvió a una fuente          | Auto -> GPSDO Locked                |
| La configuración difiere del estado activo              | TCXO -> GPSDO Locked                |
| La configuración coincide con el estado activo                   | GPSDO Locked                        |
| Fuente activa desbloqueada                         | GPSDO Unlocked                      |
| External seleccionado, no se detecta señal          | External 10 MHz Unlocked (no detectado) |

El color de la etiqueta es verde cuando está bloqueado, rojo cuando está desbloqueado y azul grisáceo atenuado antes de que llegue el estado.

#### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)** (por ejemplo, una portadora de WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Ingrese frecuencia de calibración" y la calibración no puede comenzar.
5. Haga clic en **Start**. La etiqueta de estado muestra "Starting..." y luego "Busy" mientras se ejecuta el barrido de calibración.
6. Cuando termine, el campo **Freq Offset (ppb)** se actualiza con el desplazamiento calculado.

## Pestaña Antennas

La pestaña Antennas le permite asignar nombres amigables a cada puerto de antena de la radio. Esto es útil para identificar qué antena física está conectada a cada puerto.

| Control                  | Tipo      | Comportamiento                                                                 |
|--------------------------|-----------|--------------------------------------------------------------------------|
