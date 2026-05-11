# Alternar entre filtros de baja latencia y filtros nítidos por ancho de banda

La pestaña Filters en Radio Setup le permite elegir entre filtros DSP de baja latencia y filtros nítidos para cada ancho de banda de recepción, y opcionalmente forzar el uso de filtros de baja latencia cuando utilice modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Filters solo está disponible cuando hay una conexión activa con la radio.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros para el ancho de banda actual. El botón refleja la selección activa.
4. Para forzar el uso de filtros de baja latencia cuando un modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.
5. Cierre el diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre baja latencia y filtros nítidos para el ancho de banda seleccionado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, anula la elección de filtro por ancho de banda y utiliza filtros de baja latencia siempre que una rebanada DIGU o DIGL esté activa. |
| Deslizadores de nitidez de filtro Voz / CW / Digital | Deslizador | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voz / CW / Digital) | Botón de alternancia | Activa la selección automática del nivel de filtro para ese modo y deshabilita el deslizador manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| TX Follows Active Slice | Botón pulsador | TX sigue la rebanada activa. Es mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. |
| Active Slice Follows TX | Botón pulsador | Cambia la rebanada activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Es mutuamente excluyente con TX Follows Active Slice. |
| Connect / Disconnect (TGXL) | Botón pulsador | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al inicio. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio `tgxl autotune handle=<H>` que está rota en firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de interconexión de hardware; no se necesita activación desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. Si limpia el campo IP mientras está desconectado y hace clic en Connect, o limpia el campo IP y luego cierra el diálogo, la IP y el puerto manuales guardados se eliminan, por lo que el dispositivo deja de conectarse automáticamente en el próximo inicio. |
| Connect / Disconnect (PGXL) | Botón pulsador | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón pulsador | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |
| Connect / Disconnect (ShackSwitch) | Botón pulsador | Abre o cierra una conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo ShackSwitch en la baliza de transmisión AG. El autodescubrimiento mediante UDP también funciona sin necesidad de ingresar una dirección manualmente. |
| ⚙ Web UI (ShackSwitch) | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| Select Installer... | Botón pulsador | Abre un selector de archivos que acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. cabecera PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en este botón para prepararlo. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| Check for Update | Botón pulsador | Consulta actualizaciones de firmware desde la radio. |
| APD (pestaña) | Pestaña | Configuración del muestreador externo de Predistorsión Adaptativa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ lo exponen; las series 6000 y radios anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se llenan dinámicamente desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. |
| Equalizer Reset (APD) | Botón pulsador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente alberga la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de color de las rebanadas entre la paleta integrada de AetherSDR y un conjunto completamente personalizable por rebanada. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de rebanada A–H | Botón pulsador | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa rebanada. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando está seleccionado **Use Aether defaults**. Hasta 8 rebanadas. |
| Reset All to Defaults (Themes) | Botón pulsador | Restablece todos los colores personalizados de las rebanadas a la paleta integrada de AetherSDR. |
| Station Name | Campo de texto | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Si está vacío, se usa el nombre del host del SO de forma predeterminada. Se almacena en AppSettings. Se envía a la radio como 'client station <name>'. |
| Network MTU | Spinbox | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. Rango 576-9000. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings como `NetworkMtu`. |
| Prevent system sleep while connected | Casilla de verificación | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. |
| Audio Boost | Botón de alternancia | Activa ganancia adicional en la ruta de audio del cliente. |
| Audio Buffer | Campo de texto | Aumenta el búfer de audio en milisegundos para compensar la fluctuación de VPN/SmartLink. Rango 50-1000 ms. Se almacena como `AudioBufferMs`. |
| Recording Mode | Botón pulsador | Selecciona la grabación del lado de la radio o del lado del cliente. |
| Save to | Campo de texto | Carpeta para grabaciones guardadas (solo del lado del cliente). Por defecto, Documents/AetherSDR/Recordings. |
| Auto-record on TX | Casilla de verificación | Graba automáticamente mientras se transmite. |
| Idle timeout | Spinbox | Segundos de silencio antes de que se detenga la grabación. Rango 10-3600 seg. |
| NVIDIA BNR: Autostart Container / Start / Stop / Check Status | Botón pulsador | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |
| Audio Compression (SmartLink) | Botón pulsador | Selecciona el códec de audio para SmartLink/LAN: Auto, Uncompressed u Opus. |
| Serial tab | Pestaña | Selección de puerto serie FlexControl, baudios/datos/paridad/stop, asignación de funciones de pines (DTR/RTS/CTS/DSR), intercambio de paletas, apertura automática y mapeo de acciones de botones. Compilación controlada por `HAVE_SERIALPORT`. |
| FlexControl Tuning Knob: Detect / Close | Botón pulsador | Detecta o cierra una perilla FlexControl. |
| Auto-detect on startup | Casilla de verificación | Detecta automáticamente la perilla FlexControl al inicio. |
| Invert tuning direction | Casilla de verificación | Invierte la dirección de sintonía de FlexControl. |
| WheelFrequency / WheelVolume / WheelPower / WheelRit / WheelXit | Cuadro combinado | Disponibles como asignaciones de acciones de botones FlexControl. `WheelRit` y `WheelXit` se agregaron en v26.5.1 para la sintonía de RIT y XIT. |

## Flujo de trabajo de actualización de firmware (v0.9.3)

A partir de v0.9.3, el flujo de actualización de firmware ya no descarga el instalador automáticamente. Cuando **Check for Update** encuentra una versión más reciente, el área de estado le indica que descargue el instalador de SmartSDR desde flexradio.com usted mismo. Use **Select Installer...** para indicarle a AetherSDR el archivo que descargó.

### Formatos de instalador compatibles

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador WiX de FlexRadio (SmartSDR v4.2 y posterior). Recomendado. |
| `.exe` | Instalador autoextraíble más antiguo (versiones anteriores a v4.2). |
| `.ssdr` | Archivo de firmware preextraído. |

El preparador lee los primeros 8 bytes del archivo para identificar el formato (magia OLE/MSI o cabecera PE/COFF MZ) y extrae la carga útil `.ssdr` sin necesidad de herramientas externas.

### Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión y le indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en **Select Installer...** y localice el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR prepara el firmware e informa el progreso en el área de estado.
6. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1, los controles de calibración de frecuencia en la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles Cal Frequency y Start estaban ocultos cuando se detectaba un GPSDO.

- Cuando hay un GPSDO instalado, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." en verde.
- Cuando no hay un GPSDO instalado, la etiqueta de estado muestra "Manual frequency offset calibration available." en ámbar.

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), establece la frecuencia de calibración e inicia el barrido de calibración PLL. El campo de estado junto al botón Start se actualiza a medida que avanza la calibración.
5. Mientras la calibración está en ejecución, el botón **Start** está deshabilitado y muestra "Busy". Se vuelve a habilitar cuando la calibración se completa o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario después de que la calibración se complete.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Spinbox | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón pulsador | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración PLL. Se deshabilita y etiqueta como "Busy" mientras una calibración está en curso. |
| **Freq Offset (ppb)** | Spinbox | Desplazamiento de frecuencia manual en partes por billón. |
| **10 MHz Reference Source** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External 10 MHz. Las opciones mostradas dependen del hardware instalado y del estado del oscilador informado por la radio. Si se selecciona Auto y la radio ha resuelto una fuente específica, la etiqueta de estado muestra la fuente resuelta (por ejemplo, "Auto -> GPSDO"). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, "GPSDO -> TCXO"). El estado de bloqueo (Locked / Unlocked) se agrega a la etiqueta y se actualiza en vivo. Si se selecciona External 10 MHz pero no se detecta ninguna referencia externa, la etiqueta además muestra "(not detected)". El color de la etiqueta es verde cuando está bloqueada y rojo cuando está desbloqueada. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento, lo que beneficia la decodificación de modos digitales en tiempo real y CW. Los filtros nítidos proporcionan una selectividad de pendiente más pronunciada, lo cual es más útil para condiciones de SSB congestionadas.
- La casilla de verificación **Use Low Latency Filters for Digital Modes** se aplica a todos
