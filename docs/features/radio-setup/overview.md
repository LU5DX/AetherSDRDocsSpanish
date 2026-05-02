# Descripción general de la configuración de radio

El cuadro de diálogo Radio Setup es la ventana de configuración central para su FLEX-8600. Reúne en un solo lugar la identificación de la radio, la red, el GPS, la transmisión, el audio, los filtros, los transvertores, los cables USB, los periféricos, los temas de color de los slices (canales de recepción individuales) y la configuración del puerto serie de FlexControl. Ábralo siempre que necesite cambiar la forma en que AetherSDR interactúa con el hardware de su radio.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.

## Cómo funciona

Abra Radio Setup desde `Settings > Radio Setup...`. El cuadro de diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área de configuración diferente. Las pestañas distintas a Radio cargan su contenido la primera vez que hace clic en ellas.

También puede ir directamente a pestañas específicas:

- `Settings > USB Cables...` abre Radio Setup con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre Radio Setup con la pestaña **Serial** activa (solo disponible cuando la compatibilidad con puertos serie está integrada).

El cuadro de diálogo recuerda su tamaño y posición entre sesiones.

### Pestañas de un vistazo

| Pestaña | Qué se configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones con licencia, apodo, indicativo, nombre de la estación, información de licencia y actualización de firmware. |
| **Network** | Dirección IP (DHCP o estática), MTU de red y aplicación de IP privada. |
| **GPS** | Estado GPS en tiempo real: latitud, longitud, altitud, hora y número de satélites. |
| **TX** | Tiempos de retardo/hang de TX, enclavamientos, límite de potencia global, modo de ajuste, visualización de TX en el waterfall, comportamiento de seguimiento TX/slice y un acceso directo a la configuración por banda. |
| **Phone/CW** | Medidor de nivel del micrófono, manipulador iámbico (modo A/B, intercambio, banda lateral), CWX, decodificador CW y marca RTTY predeterminada. |
| **RX** | Calibración de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración siempre están visibles; cuando hay un GPSDO instalado, la etiqueta de estado confirma su presencia. |
| **Audio** | Niveles de salida de línea, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio del PC; refuerzo de audio; tamaño del búfer de audio; modo de grabación, carpeta, grabación automática al transmitir y tiempo de espera por inactividad; control del contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia frente a filtro nítido por ancho de banda, y una opción separada para modos digitales. |
| **XVTR** | Configuración por transvertor; crear o eliminar entradas de transvertor. |
| **APD** | Configuración del muestreador externo de Adaptive Pre-Distortion: selección del puerto de retroalimentación por antena de TX y restablecimiento del ecualizador. Visible solo en radios FLEX-8x00 que informan `apd configurable=1` (firmware SmartSDR 4.2.18+). |
| **USB Cables** | Asignar adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT, y configurar sus parámetros serie. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. |
| **Themes** | Esquema de color de los slices: cambiar entre la paleta integrada de AetherSDR y colores personalizados por slice (A–H). |
| **Serial** | Selección del puerto serie de FlexControl, parámetros de línea, asignaciones de función de pines (DTR/RTS), intercambio de paleta, apertura automática y detección del mando de sintonía. (Visible solo cuando la compatibilidad con puertos serie está integrada.) |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistente o comportamientos destacados.

| Control | Pestaña | Comportamiento |
|---|---|---|
| **Station Name** | Radio | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto toma el nombre de host del sistema operativo si se deja vacío. Se almacena como `StationName`. Se envía a la radio como `client station <name>`. |
| **Select Installer...** | Radio | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic frente a PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en la versión v0.9.3. |
| **Network MTU:** | Network | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes (576–9000). El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena como `NetworkMtu`. |
| **TX Follows Active Slice** | TX | TX sigue al slice activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. Se almacena como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. |
| **Iambic Mode: A / B** | Phone/CW | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente exclusivo. Valor predeterminado: A. |
| **Decode:** | Phone/CW | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. Valor predeterminado: habilitado. |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Filters | Establece la nitidez del filtro (0 = menor latencia a 3 = más nítido) por modo. El control deslizante se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Filters | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB** | APD | Selecciona la ruta de retroalimentación utilizada para muestrear la RF saliente en el entrenamiento APD para esa antena de TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se actualizan en tiempo real desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. Valor predeterminado: INTERNAL. |
| **Equalizer Reset** | APD | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Se almacena como `AudioCompression`. Valor predeterminado: Auto. |
| **Prevent system sleep while connected** | Audio | Mantiene el sistema operativo activo mientras la radio está conectada para evitar interrupciones en los flujos de audio/TCP/UDP durante el período de inactividad. Se almacena como `InhibitSleepWhileConnected`. Valor predeterminado: deshabilitado. |
| **Audio Boost:** | Audio | Habilita ganancia adicional en la ruta de audio del lado del cliente. Se almacena como `AudioBoost`. |
| **Audio Buffer:** | Audio | Aumenta el búfer de audio (50–1000 ms) para absorber la fluctuación de latencia (jitter) de VPN o SmartLink. Valor predeterminado: 200 ms. Se almacena como `AudioBufferMs`. |
| **Recording:** Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en la radio o en este equipo. Se almacena como `RecordingMode`. Valor predeterminado: Radio Side. |
| **Save to:** | Audio | Ruta de la carpeta donde se guardan las grabaciones del lado del cliente. Se almacena como `QsoRecordingDir`. Valor predeterminado: `Documents/AetherSDR/Recordings`. |
| **Auto-record on TX** | Audio | Inicia automáticamente la grabación cada vez que la radio transmite. Se almacena como `QsoRecordingAutoRecord`. Valor predeterminado: deshabilitado. |
| **Idle timeout:** | Audio | Segundos de silencio (10–3600) tras los cuales una grabación activa se detiene automáticamente. Valor predeterminado: 120 s. Se almacena como `QsoRecordingIdleTimeout`. |
| **Connect / Disconnect (TGXL)** | Peripherals | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE con firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que quedó interrumpida en el firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de enclavamiento de hardware; no se necesita manipulación desde el cliente. Si el campo de IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Peripherals | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Peripherals | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta en el estado Connected si el dispositivo conectado actualmente es un ShackSwitch (en lugar de un Antenna Genius estándar). |
| **Connect / Disconnect (ShackSwitch)** | Peripherals | Abre o cierra una conexión a un conmutador de antenas ShackSwitch mediante el protocolo UDP/TCP de AG en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento mediante UDP también funciona sin necesidad de introducir una dirección manualmente. La fila se oculta cuando el dispositivo conectado es un Antenna Genius estándar (que no es ShackSwitch). |
| **⚙ Web UI (ShackSwitch)** | Peripherals | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Use Aether defaults / Custom colors** | Themes | Cambia el esquema de color de los slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. Valor predeterminado: Use Aether defaults. |
| **Botones de color de los slices A–H** | Themes | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Se admiten hasta 8 slices. |
| **Reset All to Defaults** | Themes | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

En la versión v0.9.3 cambió el flujo de trabajo de actualización de firmware. AetherSDR ya no descarga el instalador automáticamente. El botón que anteriormente se llamaba **Browse .ssdr...** ahora se llama **Select Installer...** y el flujo de verificación de actualizaciones funciona de la siguiente manera:

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones.
   - Si el firmware está actualizado, la etiqueta de estado muestra "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el nuevo número de versión e indica que debe descargar el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde [flexradio.com](https://www.flexradio.com) en su equipo. El instalador puede ser un archivo `.msi` (instalador WiX de FlexRadio v4.2+), un archivo `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` ya extraído.
3. Haga clic en **Select Installer...**. Se abre un selector de archivos con el filtro:
   - Instalador de SmartSDR o firmware (`*.msi *.exe *.ssdr`)
   - Instalador MSI (`*.msi`)
   - Instalador EXE (`*.exe`)
   - Firmware extraído (`*.ssdr`)
   - Todos los archivos (`*`)
