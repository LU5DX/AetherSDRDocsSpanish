# Resumen de Configuración de Radio

El diálogo Configuración de Radio es la ventana central de configuración para su FLEX-8600. Reúne en un solo lugar la identificación de la radio, red, GPS, transmisión, audio, filtros, transvertidores, cables USB, periféricos, temas de color de slices y configuraciones serie del FlexControl. Ábralo cuando necesite cambiar algo sobre cómo AetherSDR interactúa con su hardware de radio.

## Antes de comenzar

- La radio debe estar conectada. La Configuración de Radio requiere una conexión activa con la radio.

## Cómo funciona

Abra la Configuración de Radio desde `Settings > Radio Setup...`. El diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área de configuración distinta. Las pestañas distintas a Radio cargan su contenido la primera vez que hace clic en ellas.

También puede saltar directamente a pestañas específicas:

- `Settings > USB Cables...` abre la Configuración de Radio con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre la Configuración de Radio con la pestaña **Serial** activa (solo disponible cuando el soporte de puerto serie está integrado).

El diálogo recuerda su tamaño y posición entre sesiones.

### Pestañas de un vistazo

| Pestaña | Qué configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones licenciadas, apodo, indicativo, nombre de estación, información de licencia y actualización de firmware. |
| **Network** | Dirección IP (DHCP o estática), MTU de red y aplicación de IP privada. |
| **GPS** | Estado GPS en vivo: latitud, longitud, altitud, hora y conteo de satélites. |
| **TX** | Temporizaciones de colgado/retardo de TX, enclavamientos, límite de potencia global, modo de sintonía, visualización TX en waterfall, comportamiento de seguimiento TX/slice y un acceso directo a la configuración por banda. |
| **Phone/CW** | Medidor de nivel de micrófono, keyer iambic (modo A/B, intercambio, banda lateral), CWX, decodificador CW y valor predeterminado de marca RTTY. |
| **RX** | Calibración de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración siempre están visibles; cuando hay un GPSDO instalado, la etiqueta de estado confirma su presencia. |
| **Audio** | Niveles de línea de salida, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio del PC; refuerzo de audio; tamaño del búfer de audio; modo de grabación, carpeta, grabación automática en TX y tiempo de espera de inactividad; control del contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia vs. nítido por ancho de banda, y una opción separada para modos digitales. |
| **XVTR** | Configuración por transvertidor; crear o eliminar entradas de transvertidor. |
| **APD** | Configuración del muestreador de Predistorsión Adaptativa Externa — selección del puerto de retroalimentación por antena TX y reinicio del ecualizador. Visible solo en radios FLEX-8x00 que reportan `apd configurable=1` (firmware SmartSDR 4.2.18+). |
| **USB Cables** | Asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT y configura sus parámetros serie. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. |
| **Themes** | Esquema de color de slices: cambiar entre la paleta AetherSDR integrada y colores personalizados por slice (A–H). |
| **Serial** | Selección de puerto serie del FlexControl, parámetros de línea, asignaciones de función de pines (DTR/RTS), intercambio de paddle, apertura automática y detección de perilla de sintonía. (Visible solo cuando el soporte de puerto serie está integrado). |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistidas o comportamientos notables.

| Control | Pestaña | Comportamiento |
|---|---|---|
| **Station Name** | Radio | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Se predetermina al nombre de host del SO si se deja vacío. Se almacena como `StationName`. Se envía a la radio como `client station <name>`. |
| **Select Installer...** | Radio | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **Network MTU:** | Network | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes (576–9000). El valor predeterminado 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena como `NetworkMtu`. |
| **TX Follows Active Slice** | TX | TX sigue al slice activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. Se almacena como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. |
| **Iambic Mode: A / B** | Phone/CW | Selecciona el modo iambic Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente exclusivo. Predeterminado: A. |
| **Decode:** | Phone/CW | Activa la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. Predeterminado: activado. |
| **10 MHz Reference Source:** | RX | Selecciona la fuente de referencia del oscilador. El cuadro combinado se llena dinámicamente: Auto siempre está presente; TCXO, GPSDO y External 10 MHz aparecen según lo que la radio reporte como instalado o actualmente activo. Si la radio envía `ext` para la configuración o estado del oscilador, AetherSDR lo normaliza a `external` antes de mostrarlo. Cuando la configuración es Auto y la radio ha seleccionado una fuente específica, la etiqueta muestra la resolución (por ejemplo, "Auto -> GPSDO"). El estado de bloqueo (Locked / Unlocked) se muestra en verde o rojo junto al cuadro combinado y se actualiza en vivo. Si se selecciona External 10 MHz pero no se detecta ninguna referencia externa, se agrega "(not detected)" al texto de estado. |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Filters | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El control deslizante está desactivado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Filters | Activa la selección automática del nivel de filtro para ese modo; desactiva el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB** | APD | Selecciona la ruta de retroalimentación utilizada para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada externa RX/XVTR cuando utilice un amplificador lineal externo. Las opciones se llenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. Predeterminado: INTERNAL. |
| **Equalizer Reset** | APD | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Se almacena como `AudioCompression`. Predeterminado: Auto. |
| **Prevent system sleep while connected** | Audio | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. Predeterminado: desactivado. |
| **Audio Boost:** | Audio | Activa ganancia adicional en la ruta de audio del lado del cliente. Se almacena como `AudioBoost`. |
| **Audio Buffer:** | Audio | Aumenta el búfer de audio (50–1000 ms) para absorber la fluctuación de VPN o SmartLink. Predeterminado: 200 ms. Se almacena como `AudioBufferMs`. |
| **Recording:** Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en la radio o en esta computadora. Se almacena como `RecordingMode`. Predeterminado: Radio Side. |
| **Save to:** | Audio | Ruta de carpeta donde se guardan las grabaciones del lado del cliente. Se almacena como `QsoRecordingDir`. Se predetermina a `Documents/AetherSDR/Recordings`. |
| **Auto-record on TX** | Audio | Inicia automáticamente la grabación cada vez que la radio transmite. Se almacena como `QsoRecordingAutoRecord`. Predeterminado: desactivado. |
| **Idle timeout:** | Audio | Segundos de silencio (10–3600) después de los cuales una grabación activa se detiene automáticamente. Predeterminado: 120 s. Se almacena como `QsoRecordingIdleTimeout`. |
| **Connect / Disconnect (TGXL)** | Peripherals | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL acciona el PTT de la radio a través de su cable de enclavamiento de hardware; no se necesita manipulación del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Peripherals | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Peripherals | Abre/cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo actualmente conectado. |
| **Connect / Disconnect (ShackSwitch)** | Peripherals | Abre/cierra una conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento a través de UDP también funciona sin introducir una dirección manualmente. La fila se oculta cuando un Antenna Genius estándar (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Peripherals | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, vuelve a `SS_WebPort` o al puerto 5000. |
| **Use Aether defaults / Custom colors** | Themes | Cambia el esquema de color de los slices entre la paleta AetherSDR integrada y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. Predeterminado: Use Aether defaults. |
| **Botones de color Slice A–H** | Themes | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones están desactivados cuando **Use Aether defaults** está seleccionado. Se admiten hasta 8 slices. |
| **Reset All to Defaults** | Themes | Restablece todos los colores de slice personalizados a la paleta AetherSDR integrada. |

## Fuente de Referencia de 10 MHz (pestaña RX)

El cuadro combinado **10 MHz Reference Source:** en la pestaña RX se comporta de manera diferente en v0.9.7 en comparación con versiones anteriores. Anteriormente, enumeraba solo las fuentes detectadas físicamente al abrir el diálogo y mostraba una etiqueta simple "Locked / Unlocked". El nuevo comportamiento es:

- **Población dinámica.** El cuadro combinado siempre contiene Auto. TCXO, GPSDO y External 10 MHz se agregan siempre que la radio los reporte como presentes, como la configuración actual o como el estado actual del oscilador. Los elementos no se eliminan mientras el diálogo está abierto, incluso si la radio deja de reportarlos momentáneamente.
