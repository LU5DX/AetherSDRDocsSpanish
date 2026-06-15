# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información del radio, ajustes de red, GPS, configuración de transmisión, ajustes de Phone/CW, calibración de recepción, audio, antenas, filtros, transverters, cables USB, periféricos, Predistorsión Adaptativa (APD), temas, gestión de certificados SmartLink y configuración de puerto serie para FlexControl.

## Antes de comenzar

- AetherSDR debe estar conectado al radio para acceder a las pestañas que se comunican con el mismo.
- Algunas pestañas (APD, Temas, SmartLink, Serie) se construyen de forma diferida al hacer clic por primera vez.
- La pestaña APD solo es visible en radios de la serie FLEX-8x00 con firmware SmartSDR 4.2.18 o posterior.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo de Configuración de Radio.

## Comportamiento general del diálogo

- El diálogo recuerda su tamaño y posición entre sesiones.
- Orden de pestañas de izquierda a derecha: Radio, Network, GPS, TX, Phone/CW, RX, Antennas, Audio, Filters, XVTR, USB Cables, Peripherals, APD, Themes, SmartLink, Serial.
- Las pestañas cuyo contenido puede exceder la altura del diálogo (Themes, Audio, Filters, Peripherals en pantallas pequeñas o de alta densidad de píxeles) están envueltas en un área de desplazamiento para que el diálogo nunca supere el borde de la pantalla.
- Haga clic en **Close** para cerrar el diálogo.

## Pestaña Radio

Muestra la identificación del radio, información de licencia y controles de actualización de firmware. Incluye un botón **Reboot Radio**.

### Pasos

1. Haga clic en la pestaña **Radio**.
2. Vea los indicadores de solo lectura para **Radio SN**, **Region**, **HW Version**, **Model**, **Options**, **FlexControl**, **multiFLEX** y **License Info** (Subscription, Expiration, Radio ID, Licensed version). Cada indicador de solo lectura incluye un botón de copia al portapapeles junto a la etiqueta — haga clic para copiar el valor al portapapeles.
3. Opcionalmente, establezca un **Nickname**, **Callsign** o **Station Name** en los campos de texto. El **Station Name** identifica a este cliente de AetherSDR ante otras estaciones multiFLEX; por defecto es el nombre de host del SO si está vacío. Se almacena en AppSettings como `StationName`.
4. Haga clic en **Remote On** para habilitar el encendido/activación remota.
5. Para reiniciar el radio:
   - Haga clic en **Reboot Radio**. Aparece un diálogo de confirmación.
   - En conexiones LAN, AetherSDR se reconecta automáticamente una vez que el radio termina de iniciar.
   - En conexiones SmartLink/WAN, debe reconectarse manualmente después de que el radio inicie.
   - El botón está deshabilitado cuando el radio está desconectado; se rehabilita automáticamente cuando el radio se reconecta.
6. Para actualizar el firmware:
   - Haga clic en **Check for Update** para consultar el servidor de actualizaciones de FlexRadio.
   - Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
   - Haga clic en **Select Installer...** para abrir un selector de archivos. Seleccione el instalador o un archivo `.ssdr` preextraído.
   - Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware al radio.

### Notas sobre la actualización de firmware

- La etiqueta del botón **Select Installer...** cambió desde **Browse .ssdr...** en v26.5.3.
- El botón acepta archivos `.msi`, `.exe` y `.ssdr`.
- El preparador detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas.
- Una barra de progreso y una etiqueta de estado rastrean la carga.

## Pestaña Network

Configure cómo el radio obtiene su dirección de red y opciones de red avanzadas.

### Pasos

1. Haga clic en la pestaña **Network**.
2. Observe la **IP Address**, **Mask** y **MAC Address** de solo lectura. Cada una incluye un botón de copia al portapapeles.
3. Alterne **Enforce Private IP Connections:** para rechazar pares que no sean RFC1918.
4. Establezca **Network MTU:** como un valor de cuadro de giro (576-9000 bytes, predeterminado 1450). Esto establece el tamaño máximo de paquete UDP VITA-49 saliente. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`.
5. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo.
6. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:**.
7. Haga clic en **Apply** para enviar la configuración de red al radio.
8. Reconéctese al radio en su nueva dirección utilizando `Settings > Connect to Radio...`.

## Pestaña GPS

Muestra información GPS del radio.

- Muestra el estado de presencia del GPS.
- Muestra latitud, longitud, altitud, hora y recuento de satélites en vivo.
- Indicadores de solo lectura.

## Pestaña TX

Configure la temporización de transmisión, enclavamientos, límites de potencia y comportamiento.

### Pasos

1. Haga clic en la pestaña **TX**.
2. Ajuste los cuadros de giro **Timings** para ACC TX, TX Delay, RCA TX1, Timeout y retrasos TX2 en milisegundos.
   - **Timeout (sec):** Se muestra en segundos enteros; el radio lo almacena internamente en milisegundos.
3. Alterne **Interlocks - TX REQ: RCA / Accessory** para habilitar las entradas de enclavamiento.
4. Establezca **Max Power:** como un porcentaje (0-100%).
5. Seleccione **Tune Mode:** del cuadro combinado.
6. Alterne **Show TX in Waterfall:** para mostrar la señal TX en el waterfall.
7. Configure el seguimiento de slice:
   - **TX Follows Active Slice:** Botón pulsador (predeterminado Falso). Se almacena como `TxFollowsActiveSlice`. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split.
   - **Active Slice Follows TX:** Botón pulsador (predeterminado Falso). Se almacena como `ActiveFollowsTxSlice`. Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT).
8. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonización por banda.

## Pestaña Phone/CW

Configure el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Pasos

1. Haga clic en la pestaña **Phone/CW**.
2. Alterne **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel de micrófono incluso en RX.
3. Configure los ajustes de CW:
   - **Iambic:** Alterne para habilitar o deshabilitar el manipulador iambic en el radio. Mutuamente excluyente con el manipulador iambic del lado del radio; también impulsa el manipulador iambic de software local para tono lateral inferior a 5 ms.
   - **Iambic Mode: A / B:** Seleccione el modo iambic Curtis A o B. Se aplica tanto al radio como al manipulador de software local.
   - **Swap:** Alterne para intercambiar dit/dah.
   - **Sideband:** Seleccione LSB o USB para el tono CW.
   - **CWX:** Alterne para habilitar la manipulación de macros CWX.
   - **Decode:** Alterne (predeterminado Verdadero) para habilitar la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`.
4. Establezca **RTTY Mark Default:** cuadro de giro para la frecuencia de marca RTTY predeterminada.

## Pestaña RX

Configure la calibración de desviación de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

### Pasos

1. Haga clic en la pestaña **RX**.
2. Establezca **Cal Frequency (MHz):** para calibración manual.
3. Haga clic en **Start** para comenzar el barrido de calibración de frecuencia.
4. Ajuste **Freq Offset (ppb):** manualmente.
5. Seleccione **10 MHz Reference Source:** del cuadro combinado (Auto, TCXO, GPSDO, External). Las opciones dependen del hardware instalado. El estado de bloqueo (Locked/Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo.

## Pestaña Antennas

Configure los nombres y asignaciones de antenas.

- La pestaña etiquetada "Antennas" aparece entre las pestañas RX y Filters.
- Proporciona controles para nombrar y configurar los puertos de antena.

## Pestaña Audio

Configure las salidas de audio del radio, los dispositivos de audio del PC, la grabación y el contenedor NVIDIA BNR.

### Pasos

1. Haga clic en la pestaña **Audio**.
2. Ajuste los deslizadores **Line Out:** y **Headphone:**. Haga clic en los botones **Mute** correspondientes para silenciar.
3. Haga clic en **Front Speaker: / Mute** para silenciar el altavoz frontal (específico del modelo).
4. Seleccione **Audio Compression (SmartLink):** como **Auto**, **Uncompressed** u **Opus**. Se almacena como `AudioCompression`.
5. Alterne **Prevent system sleep while connected** para mantener el SO despierto. Se almacena como `InhibitSleepWhileConnected`.
6. Seleccione **PC Audio Devices: Input:** y **Output:** de los cuadros combinados.
7. Alterne **Audio Boost:** para ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`.
8. Establezca **Audio Buffer:** (50-1000 ms, predeterminado 200) para la fluctuación de VPN/SmartLink. Se almacena como `AudioBufferMs`.
9. Configure la grabación:
   - **Recording: Radio Side / Client Side:** Seleccione el modo de grabación. Se almacena como `RecordingMode`.
   - **Save to:** Campo de texto para la carpeta (solo lado del cliente). Por defecto es Documentos/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`.
   - Haga clic en **...** para buscar una carpeta de grabación.
   - Alterne **Auto-record on TX** para grabar automáticamente mientras transmite. Se almacena como `QsoRecordingAutoRecord`.
   - Establezca **Idle timeout:** (10-3600 seg, predeterminado 120) para los segundos de silencio antes de que la grabación se detenga. Se almacena como `QsoRecordingIdleTimeout`.
10. Controle **NVIDIA BNR:** con los botones Autostart Container, Start, Stop y Check Status. Un punto de color indica el estado del contenedor Running/Stopped/Unknown.

## Pestaña Filters

Configure la nitidez del filtro por modo y las opciones de baja latencia para modos digitales.

### Pasos

1. Haga clic en la pestaña **Filters**.
2. Ajuste los **deslizadores de nitidez del filtro Voice / CW / Digital** (0-3). 0 = latencia más baja, 3 = más nítido. El deslizador está deshabilitado cuando Auto está habilitado.
3. Alterne **Auto (Voice / CW / Digital)** para habilitar la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual.
4. Alterne **Use Low Latency Filters for Digital Modes** para forzar filtros de baja latencia en DIGU/DIGL.

## Pestaña XVTR

Configure los ajustes por transverter.

### Pasos

1. Haga clic en la pestaña **XVTR**.
2. La pestaña contiene pestañas anidadas, una por transverter, más una pestaña '+'.
3. Para cada transverter:
   - Alterne **RX Only:** para forzar solo RX.
   - Haga clic en **Remove** para eliminar la definición del transverter.
4. Haga clic en **Create New Transverter** para agregar una nueva entrada de transverter.

## Pestaña USB Cables

Asigne adaptadores serie USB a tipos de cable.

### Pasos

1. Haga clic en la pestaña **USB Cables**.
2. Vea la **Cables list / Status** detectada con el estado Plugged/Unplugged por tipo de cable.
3. Configure los parámetros por cable: **Name**, **Enabled**, **Speed**, **Data Bits**, **Parity**, **Stop Bits**, **Flow**, **Source**, **Auto Report**, **BCD Type**, **Polarity**, **Bit Configuration (0-7)**.

## Pestaña Peripherals

Configure las conexiones de dispositivos externos (TGXL, PGXL, Antenna Genius).

### Pasos

1. Haga clic en la pestaña **Peripherals**.
2. Para cada periférico, ingrese la dirección IP y el puerto (puertos predeterminados: TGXL=9010, PGXL=9008, Antenna Genius=9007).
3. Haga clic en **Connect** para establecer una conexión TCP directa. La IP y el puerto se guardan al conectar para que AetherSDR se reconecte automáticamente al inicio.
4. Haga clic en **Disconnect** para cerrar la conexión.

### Reconexión automática de periféricos y borrado de IP manual

Cuando ingresa una dirección IP para un periférico y hace clic en **Connect**, la IP y el puerto se guardan en la configuración. En inicios posteriores, AetherSDR intenta automáticamente reconectarse a ese periférico.

Si borra el campo IP y hace clic en **Connect** mientras está desconectado, la IP y el puerto manuales guardados se eliminan de la configuración, evitando la reconexión automática al inicio. Si borra el campo IP y cierra el diálogo **Radio Setup** sin hacer clic en Connect/Disconnect, la configuración guardada también se borra y cualquier conexión activa se desconecta.

### Notas específicas del TGXL

- Requerido para recuperar TUNE en firmware 4.2+.
- Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que está rota en firmware 4.2.
- El TGXL controla el PTT del radio a través de su cable de enclavamiento de hardware; no se necesita manipulación del lado del cliente.
- Si el campo IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se rellena previamente.

## Pestaña APD

Configure los puertos de muestra de Predistorsión Adaptativa por antena TX. La pestaña está oculta a menos que el radio informe `apd configurable=1` (FLEX-8x00 con SmartSDR 4.2.18+).

### Pasos

1. Haga clic en la pestaña **APD** (solo visible en radios compatibles).
2. Para cada antena TX (**ANT1**, **ANT2**, **XVTA**, **XVTB**), seleccione el puerto de muestreo del cuadro combinado (**INTERNAL**, **RX_A**, **RX_B**, **XVTA**, **XVTB**).
   - **INTERNAL** muestrea dentro del radio.
   - Los puertos externos requieren una señal de realimentación acoplada desde la salida del amplificador lineal.
3. Haga clic en **Reset** (APD Equalizer) para borrar todos los datos de entrenamiento APD por antena en el radio.

## Pestaña Themes

Configure la apariencia de la interfaz de usuario, incluyendo
