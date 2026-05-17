# Diálogo de Configuración de Radio

El diálogo de Configuración de Radio es la ventana maestra de configuración por radio. Proporciona pestañas para información del radio, configuración de red, GPS, configuración de transmisión, ajustes de Phone/CW, calibración de recepción, audio, antenas, filtros, transverters, cables USB, periféricos, Predistorsión Adaptativa (APD), temas y configuración del puerto serie para FlexControl.

## Antes de comenzar

- AetherSDR debe estar conectado al radio para acceder a las pestañas que se comunican con el radio.
- Algunas pestañas (APD, Themes, Serial) se cargan de forma diferida al hacer clic por primera vez.
- La pestaña APD solo es visible en radios de la serie FLEX-8x00 con firmware SmartSDR 4.2.18 o posterior.

## Abrir el diálogo

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo de Configuración de Radio.

## Comportamiento general del diálogo

- El diálogo recuerda su tamaño y posición entre sesiones.
- Orden de pestañas de izquierda a derecha: Radio, Network, GPS, TX, Phone/CW, RX, Antennas, Audio, Filters, XVTR, USB Cables, Peripherals, APD, Themes, Serial.
- Haga clic en **Close** para cerrar el diálogo.

## Pestaña Radio

Muestra la identificación del radio, información de licencia y controles de actualización de firmware.

### Pasos

1. Haga clic en la pestaña **Radio**.
2. Visualice los indicadores de solo lectura para **Radio SN**, **Region**, **HW Version**, **Model**, **Options**, **FlexControl**, **multiFLEX** y **License Info** (Subscription, Expiration, Radio ID, Licensed version).
3. Opcionalmente, configure un **Nickname**, **Callsign** o **Station Name** en los campos de texto. El **Station Name** identifica este cliente de AetherSDR ante otras estaciones multiFLEX; si está vacío, se usa el nombre del host del SO por defecto.
4. Haga clic en **Remote On** para habilitar el encendido remoto/remote-on.
5. Para actualizar el firmware:
   - Haga clic en **Check for Update** para consultar el servidor de actualizaciones de FlexRadio.
   - Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
   - Haga clic en **Select Installer...** para abrir un selector de archivos. Seleccione el instalador o un archivo `.ssdr` preextraído.
   - Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware al radio.

### Notas sobre la actualización de firmware

- El botón **Select Installer...** acepta archivos `.msi`, `.exe` y `.ssdr`.
- El preparador detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (marca OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas.
- Una barra de progreso y una etiqueta de estado siguen la carga.

## Pestaña Network

Configure cómo el radio obtiene su dirección de red y opciones de red avanzadas.

### Pasos

1. Haga clic en la pestaña **Network**.
2. Observe la **IP Address**, **Mask** y **MAC Address** de solo lectura.
3. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo.
4. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:**.
5. Haga clic en **Apply** para enviar la configuración de red al radio.
6. Reconéctese al radio en su nueva dirección usando `Settings > Connect to Radio...`.

### Controles de red adicionales

- **Enforce Private IP Connections:** Alterne para rechazar pares que no sean RFC1918.
- **Network MTU:** Control giratorio (576-9000 bytes, valor predeterminado 1450). Establece el tamaño máximo del paquete UDP VITA-49 saliente. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`.

## Pestaña GPS

Muestra la información del GPS del radio.

- Muestra el estado de presencia del GPS.
- Muestra en vivo la latitud, longitud, altitud, hora y número de satélites.
- Indicadores de solo lectura.

## Pestaña TX

Configure los tiempos de transmisión, enclavamientos, límites de potencia y comportamiento.

### Pasos

1. Haga clic en la pestaña **TX**.
2. Ajuste los controles giratorios de **Timings** para ACC TX, TX Delay, RCA TX1, Timeout y TX2 delays en milisegundos.
   - **Timeout (sec):** Se muestra en segundos enteros; el radio lo almacena internamente en milisegundos.
3. Alterne **Interlocks - TX REQ: RCA / Accessory** para habilitar las entradas de enclavamiento.
4. Establezca **Max Power:** como porcentaje (0-100%).
5. Seleccione **Tune Mode:** del cuadro combinado.
6. Alterne **Show TX in Waterfall:** para mostrar la señal de TX en el waterfall.
7. Configure el seguimiento de slices:
   - **TX Follows Active Slice:** Botón pulsador (valor predeterminado False). Se almacena como `TxFollowsActiveSlice`. Excluyente mutuamente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split.
   - **Active Slice Follows TX:** Botón pulsador (valor predeterminado False). Se almacena como `ActiveFollowsTxSlice`. Cambia el slice activo cuando el TX se mueve externamente.
8. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia/sintonización por banda.

## Pestaña Phone/CW

Configure el micrófono, el manipulador CW y los valores predeterminados de RTTY.

### Pasos

1. Haga clic en la pestaña **Phone/CW**.
2. Alterne **Enable/Disable the Level Meter During Receive** para mostrar el medidor de nivel de micrófono incluso en RX.
3. Configure los ajustes de CW:
   - **Iambic:** Alterne para habilitar o deshabilitar el manipulador iámbico en el radio.
   - **Iambic Mode: A / B:** Seleccione el modo iámbico Curtis A o B. Esto se aplica tanto al manipulador del radio como al del software local. Par mutuamente excluyente.
   - **Swap:** Alterne para intercambiar dit/dah.
   - **Sideband:** Seleccione LSB o USB para el tono CW.
   - **CWX:** Alterne para habilitar el keying por macros CWX.
   - **Decode:** Alternar (valor predeterminado True) para habilitar la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`.
4. Establezca **RTTY Mark Default:** control giratorio para la frecuencia de marca RTTY predeterminada.

## Pestaña RX

Configure la calibración del desplazamiento de frecuencia del GPSDO y la fuente de referencia de 10 MHz.

### Pasos

1. Haga clic en la pestaña **RX**.
2. Establezca **Cal Frequency (MHz):** para la calibración manual.
3. Haga clic en **Start** para iniciar el barrido de calibración de frecuencia.
4. Ajuste **Freq Offset (ppb):** manualmente.
5. Seleccione **10 MHz Reference Source:** del cuadro combinado (Auto, TCXO, GPSDO, External). El estado de bloqueo (Locked/Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo.

## Pestaña Antennas

Configure los nombres y asignaciones de antenas.

- Nuevo en v26.5.2.1.
- La pestaña etiquetada "Antennas" aparece entre las pestañas RX y Filters.
- Proporciona controles para nombrar y configurar los puertos de antena.

## Pestaña Audio

Configure las salidas de audio del radio, dispositivos de audio del PC, grabación y el contenedor NVIDIA BNR.

### Pasos

1. Haga clic en la pestaña **Audio**.
2. Ajuste los deslizadores **Line Out:** y **Headphone:**. Haga clic en los botones **Mute** correspondientes para silenciar.
3. Haga clic en **Front Speaker: / Mute** para silenciar el altavoz frontal (específico del modelo).
4. Seleccione **Audio Compression (SmartLink):** como **Auto**, **Uncompressed** u **Opus**. Se almacena como `AudioCompression`.
5. Alterne **Prevent system sleep while connected** para mantener el SO despierto. Se almacena como `InhibitSleepWhileConnected`.
6. Seleccione **PC Audio Devices: Input:** y **Output:** de los cuadros combinados.
7. Alterne **Audio Boost:** para ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`.
8. Establezca **Audio Buffer:** (50-1000 ms, valor predeterminado 200) para la fluctuación de VPN/SmartLink. Se almacena como `AudioBufferMs`.
9. Configure la grabación:
   - **Recording: Radio Side / Client Side:** Seleccione el modo de grabación. Se almacena como `RecordingMode`.
   - **Save to:** Campo de texto para la carpeta (solo del lado del cliente). Por defecto en Documents/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`.
   - Haga clic en **...** para buscar una carpeta de grabación.
   - Alterne **Auto-record on TX** para grabar automáticamente mientras transmite. Se almacena como `QsoRecordingAutoRecord`.
   - Establezca **Idle timeout:** (10-3600 seg, valor predeterminado 120) para los segundos de silencio antes de que se detenga la grabación. Se almacena como `QsoRecordingIdleTimeout`.
10. Controle **NVIDIA BNR:** con los botones Autostart Container, Start, Stop y Check Status. Un punto de color indica el estado del contenedor Running/Stopped/Unknown.

## Pestaña Filters

Configure la nitidez del filtro por modo y las opciones de baja latencia para modos digitales.

### Pasos

1. Haga clic en la pestaña **Filters**.
2. Ajuste los **deslizadores de nitidez de filtro Voice / CW / Digital** (0-3). 0 = latencia más baja, 3 = más nítido. El deslizador está deshabilitado cuando Auto está habilitado.
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
2. Visualice la **lista de Cables / Estado** detectada con el estado Plugged/Unplugged por tipo de cable.
3. Configure los parámetros por cable: **Name**, **Enabled**, **Speed**, **Data Bits**, **Parity**, **Stop Bits**, **Flow**, **Source**, **Auto Report**, **BCD Type**, **Polarity**, **Bit Configuration (0-7)**.

## Pestaña Peripherals

Configure las conexiones de dispositivos externos (TGXL, PGXL, Antenna Genius).

### Pasos

1. Haga clic en la pestaña **Peripherals**.
2. Para cada periférico, ingrese la dirección IP y el puerto (puertos predeterminados: TGXL=9010, PGXL=9008, Antenna Genius=9007).
3. Haga clic en **Connect** para establecer una conexión TCP directa. La IP y el puerto se guardan al conectar para que AetherSDR se reconecte automáticamente al inicio.
4. Haga clic en **Disconnect** para cerrar la conexión.

### Reconexión automática de periféricos y limpieza de IP manual

Cuando ingresa una dirección IP para un periférico y hace clic en **Connect**, la IP y el puerto se guardan en la configuración. En inicios posteriores, AetherSDR intenta automáticamente reconectarse a ese periférico.

Si limpia el campo de IP y hace clic en **Connect** mientras está desconectado, la IP y el puerto manuales guardados se eliminan de la configuración, lo que impide la reconexión automática al inicio. Si limpia el campo de IP y cierra el diálogo **Radio Setup** sin hacer clic en Connect/Disconnect, la configuración guardada también se limpia y cualquier conexión activa se desconecta.

### Notas específicas del TGXL

- Requerido para recuperar TUNE en firmware 4.2+.
- Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que está rota en el firmware 4.2.
- El TGXL acciona el PTT del radio a través de su cable de enclavamiento de hardware; no se necesita keying del lado del cliente.
- Si el campo de IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se rellena previamente.

## Pestaña APD

Configure los puertos de muestra de Predistorsión Adaptativa por antena de TX. La pestaña está oculta a menos que el radio informe `apd configurable=1` (FLEX-8x00 con SmartSDR 4.2.18+).

### Pasos

1. Haga clic en la pestaña **APD** (solo visible en radios compatibles).
2. Para cada antena de TX (**ANT1**, **ANT2**, **XVTA**, **XVTB**), seleccione el puerto del sampler del cuadro combinado (**INTERNAL**, **RX_A**, **RX_B**, **XVTA**, **XVTB**).
   - **INTERNAL** muestrea dentro del radio.
   - Los puertos externos requieren una señal de retroalimentación acoplada desde la salida del amplificador lineal.
3. Haga clic en **Reset** para borrar todos los datos de entrenamiento APD por antena en el radio (envía `apd reset`).

## Pestaña Themes

Configure la apariencia de la interfaz de usuario, incluyendo las anulaciones de color por slice.

### Pasos

1. Haga clic en la pestaña **Themes**.
2. En la sección **Slice Colors**:
   - Seleccione **Use Aether defaults** para usar la paleta incorporada (cian, magenta, verde, amarillo, naranja, verde azulado, coral, lavanda).
   - Seleccione **Custom colors** para habilitar selectores de color por slice.
3. Si se selecciona **Custom colors**, haga clic en cualquier botón con letra (A-H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles de inmediato en los widgets VFO, superposiciones del panadapter y distintivos de canales CAT.
4. Haga clic en **Reset All to Defaults** para restablecer todos los colores personalizados de slice a la paleta incorporada.

## Pestaña Serial

Configure los ajustes del puerto serie del FlexControl y la asignación de botones. Disponible solo cuando se compila con soporte para puerto serie.

### Pasos

1. Haga clic en la pestaña **Serial**.
2. Seleccione el **Port** del cuadro combinado, o edite el **Path** manualmente. Haga clic en **Refresh** para volver a escanear los puertos disponibles.
3. Configure los ajustes de **Baud**, **Data**, **Parity** y **Stop**.
4. As
