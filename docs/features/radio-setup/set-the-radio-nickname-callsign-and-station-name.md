# Configurar el apodo de la radio, el indicativo y el nombre de la estación

Establezca un apodo legible, su indicativo y un nombre de estación en la FLEX-8600 conectada. Estos valores identifican la radio y este cliente para otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio inmediatamente.
5. En el campo **Callsign**, escriba el indicativo de su estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica a este cliente para otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en el botón de cierre de la ventana o presione Escape para descartar el diálogo.

## Características de la ventana de diálogo

El diálogo Radio Setup utiliza un diálogo persistente con guardado de geometría. La posición y el tamaño del diálogo se guardan automáticamente al cerrarlo y se restauran la próxima vez que lo abra. La geometría se almacena en AppSettings bajo la clave `RadioSetupDialogGeometry`.

## Función de cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como el nombre de la radio. | Nombre reportado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(en blanco)_ |
| **Station Name** | Identifica a este cliente de AetherSDR para otras estaciones multiFLEX. | Nombre de host del SO |
| **TX Follows Active Slice** | La transmisión sigue la porción activa. Excluyente con Active Slice Follows TX. Se desactiva automáticamente durante Split. | Falso |
| **Active Slice Follows TX** | Cambia la porción activa cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Excluyente con TX Follows Active Slice. | Falso |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el control deslizante está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Activa la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que está rota en firmware 4.2. El TGXL activa el PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita accionamiento desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se pre-rellena. | Conectar |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Conectar |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila está oculta en el estado Conectado si un ShackSwitch (no un Antenna Genius estándar) es el dispositivo conectado. | Conectar |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión de AG. El descubrimiento automático mediante UDP también funciona sin esta fila. La fila está oculta en el estado Conectado si un Antenna Genius (no ShackSwitch) es el dispositivo conectado. | Conectar |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador de predistorsión adaptativa externa: selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con SmartSDR 4.2.18+ exponen esto; las series 6000 y radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de realimentación que usa la radio para muestrear la RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se obtienen en vivo del subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de la interfaz de usuario: actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores de las porciones entre la paleta integrada de AetherSDR y un conjunto completamente personalizable por porción. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa porción. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter e insignias de canal CAT. Los botones están deshabilitados cuando **Use Aether defaults** está seleccionado. Hasta 8 porciones. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de las porciones a la paleta integrada de AetherSDR. | — |
| **Network MTU:** | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Almacenado en AppSettings. | 1450 |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN. | Auto |
| **Prevent system sleep while connected** | Mantiene el SO activo mientras la radio está conectada para evitar caídas en los flujos de audio/TCP/UDP durante la inactividad. | Falso |
| **Audio Boost:** | Activa ganancia adicional en la ruta de audio del cliente. | — |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Almacenado como `AudioBufferMs`. | 200 |
| **Recording: Radio Side / Client Side** | Selecciona la grabación del lado de la radio o del lado del cliente. | Radio Side |
| **Save to:** | Carpeta para las grabaciones guardadas (solo lado del cliente). | Documents/AetherSDR/Recordings |
| **Auto-record on TX** | Graba automáticamente mientras transmite. | Falso |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga. | 120 |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. | — |
| **Iambic:** | Activa o desactiva el manipulador iámbico en la radio. | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par excluyente. | A |
| **Decode:** | Activa la superposición de decodificación CW en el panadapter. | Verdadero |
| **Peripherals IP/port fields** | Cuando el campo IP se limpia mientras está desconectado, hacer clic en **Connect** no hace nada; en su lugar, elimina cualquier IP manual previamente guardada de la configuración, evitando la reconexión automática al inicio. Cuando el diálogo se cierra con un campo IP limpio y existe una IP manual previamente guardada, la IP guardada se elimina automáticamente y el dispositivo se desconecta si está conectado actualmente. | — |
| **FlexControl button actions** | La asignación de acciones de botones incluye nuevas acciones de rueda: WheelRit y WheelXit. Estas asignan la perilla de sintonización del FlexControl para ajustar los offsets de RIT y XIT respectivamente. | — |
| APD (tab) | Selección del puerto de muestra de predistorsión adaptativa externa por antena TX (ANT1, ANT2, XVTA, XVTB). La pestaña está oculta a menos que la radio reporte apd configurable=1 (FLEX-8x00 con SmartSDR 4.2.18+). | Nuevo en v26.5.1 (#2186). Se crea de forma diferida solo cuando se hace clic en la pestaña por primera vez. |
| External Sampler (per TX ANT) | Encabezado de sección dentro de la pestaña APD que muestra una cuadrícula de 2x2 de cuadros combinados del puerto de muestra de ANT1/ANT2/XVTA/XVTB. | |
| ANT1: / ANT2: / XVTA: / XVTB: | Selecciona el puerto de muestra (INTERNAL, RX_A, RX_B, XVTA, XVTB) que la radio utiliza para la realimentación APD en esa antena TX. | INTERNAL muestrea dentro de la radio; los puertos externos requieren una señal de realimentación acoplada desde la salida del amplificador lineal. El cambio envía setApdSamplerPort() a la radio. |
| Equalizer Reset: | Etiqueta de fila de sección para el botón de reinicio del ecualizador APD. | |
| Reset (APD Equalizer) | Borra todos los datos de entrenamiento APD por antena en la radio. | Envía resetApdEqualizer() al TransmitModel de la radio. |
| Themes (tab) | Configuración de apariencia de la interfaz de usuario, incluidas las anulaciones de color por porción. | La etiqueta de la pestaña en código es 'Themes'. Se crea de forma diferida al hacer clic por primera vez. |
| Slice Colors | Encabezado del cuadro de grupo para los controles de color de las porciones. | |
| Use Aether defaults | Usa la paleta de colores de porciones integrada (cian/magenta/verde/amarillo/naranja/verde azulado/coral/lavanda). | Seleccionar esto deshabilita los botones de color personalizados. |
| Custom colors | Activa los selectores de color por porción (A-H). | Seleccionar esto habilita los ocho botones de color a continuación. |
| A/B/C/D/E/F/G/H color buttons | Haga clic para abrir un selector de color para esa letra de porción (A-H). El fondo del botón refleja el color asignado actualmente. | 8 botones dispuestos en una cuadrícula horizontal. Almacenados a través de SliceColorManager que persiste en AppSettings. |
| Reset All to Defaults | Restablece cada color personalizado por porción a su valor predeterminado integrado. | |
| **Antennas (tab)** | Configuración de nombres y parámetros de antenas. | Nuevo en v26.5.2.1. |

## Controles de temporización de la pestaña TX

La pestaña **TX** incluye campos de temporización para retrasos de interbloqueo y tiempo de espera. El campo de tiempo de espera se muestra en segundos para facilitar la lectura, pero se almacena y transmite a la radio en milisegundos.

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **ACC TX:** | Retraso de transmisión ACC en milisegundos. | — |
| **TX Delay:** | Retraso de transmisión en milisegundos. | — |
| **RCA TX1:** | Retraso de transmisión RCA TX1 en milisegundos. | — |
| **Timeout (sec):** | Tiempo de espera de interbloqueo mostrado en segundos. La radio almacena este valor en milisegundos internamente. | — |

## Actualización de firmware (pestaña Radio)

Use los controles de actualización de firmware en la pestaña **Radio** para buscar y aplicar actualizaciones de firmware a la radio.

### Para buscar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com, y luego use **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

### Para preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Abrir.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from <nombre de archivo>..." y aparece la barra de progreso.
   - El preparador de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (OLE/MS
