# Descripción general de la configuración de radio

El diálogo Radio Setup es la ventana de configuración central de su FLEX-8600. Reúne identificación de radio, red, GPS, transmisión, audio, filtros, transversores, cables USB, periféricos, temas de color de slice y configuración serial de FlexControl en un solo lugar. Ábralo siempre que necesite cambiar algo sobre cómo AetherSDR interactúa con su hardware de radio.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.

## Cómo funciona

Abra Radio Setup desde `Settings > Radio Setup...`. El diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área distinta de configuración. Las pestañas distintas de Radio cargan su contenido la primera vez que hace clic en ellas.

También puede saltar directamente a pestañas específicas:

- `Settings > USB Cables...` abre Radio Setup con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre Radio Setup con la pestaña **Serial** activa (solo disponible cuando la compatibilidad con puerto serial está integrada).

El diálogo recuerda su tamaño y posición entre sesiones.

### Pestañas de un vistazo

| Pestaña | Qué configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones con licencia, alias, indicativo de llamada, nombre de estación, información de licencia y actualización de firmware. |
| **Network** | Dirección IP (DHCP o estática), MTU de red e imposición de IP privada. |
| **GPS** | Estado de GPS en vivo: latitud, longitud, altitud, hora y número de satélites. |
| **TX** | Tiempos de suspensión/retardo de TX, bloqueos, límite de potencia global, modo de afinación, visualización TX en panadapter, comportamiento de TX/slice, y acceso directo a configuración por banda. |
| **Phone/CW** | Medidor de nivel de micrófono, manipulador iámbico (modo A/B, intercambio, banda lateral), CWX, decodificador CW y marca predeterminada de RTTY. |
| **RX** | Calibración de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración siempre están visibles; cuando está instalado un GPSDO, la etiqueta de estado confirma su presencia. |
| **Audio** | Niveles de salida de línea, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio de PC; refuerzo de audio; tamaño del búfer de audio; modo de grabación, carpeta, grabación automática en TX e tiempo de espera inactivo; control de contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia vs. filtro afilado por ancho de banda, y una opción separada para modos digitales. |
| **XVTR** | Configuración por transversor; crear o eliminar entradas de transversor. |
| **APD** | Configuración del muestreador de predistorsión adaptativa externa; selección del puerto de retroalimentación por antena TX y reinicio del ecualizador. Visible solo en radios FLEX-8x00 que reportan `apd configurable=1` (firmware SmartSDR 4.2.18+). |
| **USB Cables** | Asigne adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT, y configure sus parámetros seriales. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. |
| **Themes** | Esquema de color de slice: cambie entre la paleta AetherSDR integrada y colores personalizados por slice (A–H). |
| **Serial** | Selección de puerto serial de FlexControl, parámetros de línea, asignación de función de pin (DTR/RTS), intercambio de paleta, apertura automática y detección de perilla de afinación. (Visible solo cuando la compatibilidad con puerto serial está integrada.) |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistentes o comportamientos notables.

| Control | Pestaña | Comportamiento |
|---|---|---|
| **Station Name** | Radio | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto, el nombre de host del sistema operativo si se deja vacío. Se almacena como `StationName`. Se envía a la radio como `client station <name>`. |
| **Select Installer...** | Radio | Abre un explorador de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El organizador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **Network MTU:** | Network | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes (576–9000). El valor predeterminado de 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena como `NetworkMtu`. |
| **TX Follows Active Slice** | TX | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación de Split. Se almacena como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | TX | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. |
| **Iambic Mode: A / B** | Phone/CW | Selecciona el modo iámbico Curtis A o B para la radio y el manipulador de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Decode:** | Phone/CW | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. Predeterminado: habilitado. |
| **Voice / CW / Digital filter sharpness sliders** | Filters | Establece la nitidez del filtro (0 = latencia más baja a 3 = más agudo) por modo. El deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Filters | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos** | APD | Selecciona la ruta de retroalimentación utilizada para muestrear RF saliente para entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando conduzca un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. Predeterminado: INTERNAL. |
| **Equalizer Reset** | APD | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado en SmartLink o LAN. Se almacena como `AudioCompression`. Predeterminado: Auto. |
| **Prevent system sleep while connected** | Audio | Mantiene el sistema operativo activo mientras la radio está conectada para evitar caídas de flujo de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. Predeterminado: deshabilitado. |
| **Audio Boost:** | Audio | Habilita ganancia adicional en la ruta de audio del lado del cliente. Se almacena como `AudioBoost`. |
| **Audio Buffer:** | Audio | Aumenta el búfer de audio (50–1000 ms) para absorber fluctuación de VPN o SmartLink. Predeterminado: 200 ms. Se almacena como `AudioBufferMs`. |
| **Recording:** Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en la radio o en esta computadora. Se almacena como `RecordingMode`. Predeterminado: Radio Side. |
| **Save to:** | Audio | Ruta de carpeta donde se guardan las grabaciones del lado del cliente. Se almacena como `QsoRecordingDir`. Por defecto es `Documents/AetherSDR/Recordings`. |
| **Auto-record on TX** | Audio | Inicia automáticamente la grabación cada vez que la radio transmite. Se almacena como `QsoRecordingAutoRecord`. Predeterminado: deshabilitado. |
| **Idle timeout:** | Audio | Segundos de silencio (10–3600) después de los cuales una grabación activa se detiene automáticamente. Predeterminado: 120 s. Se almacena como `QsoRecordingIdleTimeout`. |
| **Connect / Disconnect (TGXL)** | Peripherals | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de radio rota en firmware 4.2. El TGXL controla PTT de radio mediante su cable de bloqueo de hardware; no se necesita activación del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Peripherals | Abre/cierra una conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Peripherals | Abre/cierra una conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo actualmente conectado. |
| **Connect / Disconnect (ShackSwitch)** | Peripherals | Abre/cierra una conexión a un conmutador de antena ShackSwitch a través del protocolo UDP/TCP de AG en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en el faro de transmisión de AG. El descubrimiento automático a través de UDP también funciona sin ingresar manualmente una dirección. La fila se oculta cuando un Antenna Genius estándar (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Peripherals | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza `webPort` del faro si es mayor a 1024; de lo contrario, recurre a `SS_WebPort` o puerto 5000. |
| **Use Aether defaults / Custom colors** | Themes | Cambia el esquema de color del slice entre la paleta AetherSDR integrada y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. Predeterminado: Use Aether defaults. |
| **Slice A–H color buttons** | Themes | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter e insignias de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Se admiten hasta 8 slices. |
| **Reset All to Defaults** | Themes | Restablece todos los colores personalizados del slice a la paleta AetherSDR integrada. |

## Actualización de firmware (pestaña Radio)

En v0.9.3 el flujo de trabajo de actualización de firmware cambió. AetherSDR ya no descarga el instalador automáticamente. El botón previamente etiquetado como **Browse .ssdr...** ahora se etiqueta como **Select Installer...** y el flujo de verificación de actualización funciona de la siguiente manera:

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualización.
   - Si el firmware es actual, la etiqueta de estado muestra "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el nuevo número de versión e instrucciones para descargar el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde [flexradio.com](https://www.flexradio.com) a su computadora. El instalador puede ser un archivo `.msi` (instalador WiX de FlexRadio v4.2+), un archivo `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído.
3. Haga clic en **Select Installer...**. Se abre un explorador de archivos con el filtro:
   - Instalador o firmware de SmartSDR (`*.msi *.exe *.ssdr`)
   - Instalador MSI (`*.msi`)
   - Instalador EXE (`*.exe`)
   - Firmware extraído (`*.ssdr`)
   - Todos los archivos (`*`)
