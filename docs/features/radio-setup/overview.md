# Resumen de Configuración de la Radio

El diálogo de Configuración de la Radio es la ventana de configuración central para su FLEX-8600. Reúne en un solo lugar la identificación de la radio, red, GPS, transmisión, audio, filtros, transvertidores, cables USB, periféricos, nombres de antenas, temas de color de slices, configuración del muestreador APD, gestión de certificados SmartLink y ajustes de la conexión serie del FlexControl. Ábralo cada vez que necesite cambiar algo sobre cómo AetherSDR interactúa con su equipo de radio.

## Antes de comenzar

- La radio debe estar conectada. La Configuración de la Radio requiere una conexión activa con la radio.

## Cómo funciona

Abra la Configuración de la Radio desde `Settings > Radio Setup...`. El diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área de configuración distinta. Las pestañas que no sean Radio cargan su contenido la primera vez que hace clic en ellas.

El diálogo recuerda su tamaño y posición entre sesiones usando `PersistentDialog`. Una barra de título con el texto "Radio Setup" aparece en la parte superior. Puede arrastrar la barra de título para mover el diálogo.

También puede saltar directamente a pestañas específicas:

- `Settings > USB Cables...` abre la Configuración de la Radio con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre la Configuración de la Radio con la pestaña **Serial** activa (solo disponible cuando el soporte para puerto serie está integrado).

### Comportamiento de desplazamiento en pestañas

Las pestañas cuyo contenido puede exceder la altura visible del diálogo en pantallas pequeñas o de alta densidad de píxeles (Radio, Audio, Filters, Themes, Peripherals, SmartLink) incorporan automáticamente un área de desplazamiento vertical. La barra de desplazamiento solo aparece cuando es necesaria; los usuarios con pantallas anchas no ven ningún cambio visual.

### Pestañas de un vistazo

| Pestaña | Qué configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones licenciadas, apodo, indicativo, nombre de estación, información de licencia, actualización de firmware y reinicio de la radio. |
| **Network** | Dirección IP (DHCP o estática), MTU de red y aplicación de IP privada. |
| **GPS** | Estado del GPS en vivo: latitud, longitud, altitud, hora y número de satélites. |
| **TX** | Temporizaciones de suspensión/retardo de TX, enclavamientos, límite de potencia global, modo de sintonía, visualización de TX en el waterfall, comportamiento de seguimiento TX/slice y un acceso directo a la configuración por banda. |
| **Phone/CW** | Medidor de nivel de micrófono, keyer iámbico (modo A/B, intercambio, banda lateral), CWX, decodificador de CW y marca predeterminada de RTTY. |
| **RX** | Calibración de compensación de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración siempre están visibles; cuando hay un GPSDO instalado, la etiqueta de estado confirma su presencia. |
| **Antennas** | Muestra y renombra los puertos de antena (ANT1, ANT2, XVTA, XVTB) según los reconoce la radio. |
| **Audio** | Niveles de salida de línea, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio del PC; refuerzo de audio; tamaño del búfer de audio; modo de grabación, carpeta, grabación automática en TX y tiempo de espera de inactividad; control del contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia vs. filtro nítido por ancho de banda, y una opción separada para modos digitales. |
| **XVTR** | Configuración por transvertidor; crear o eliminar entradas de transvertidor. |
| **APD** | Configuración del muestreador del Predistorsionador Adaptativo Externo: selección del puerto de realimentación por antena de TX y reinicio del ecualizador. Visible solo en radios FLEX-8x00 que reportan `apd configurable=1` (firmware SmartSDR 4.2.18+). |
| **USB Cables** | Asigna adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT y configura sus parámetros serie. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL, Antenna Genius, ShackSwitch y amplificadores ACOM. |
| **KiwiSDR** | Gestión de receptores públicos KiwiSDR: añadir, eliminar, explorar y configurar hasta 10 receptores públicos. |
| **Themes** | Esquema de color de slice: cambiar entre la paleta incorporada de AetherSDR y colores personalizados por slice (A–H). |
| **Serial** | Selección de puerto serie del FlexControl, parámetros de línea, asignación de funciones de pines (DTR/RTS), intercambio de paletas, apertura automática y detección de la perilla de sintonía. (Visible solo cuando el soporte para puerto serie está integrado.) |
| **SmartLink** | Gestión de certificados TLS fijados: lista cada certificado fijado con botones Forget y Forget All. |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistentes o comportamientos notables.

| Control | Pestaña | Comportamiento |
|---|---|---|
| **Radio SN** | Radio | Número de serie del chasis (solo lectura). Incluye un botón de copia al portapapeles (icono de bandeja) junto al valor. |
| **HW Version** | Radio | Cadena de versión de hardware (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **Options** | Radio | Muestra las opciones de radio licenciadas (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **Model** | Radio | Modelo de la radio (solo lectura). Incluye un botón de copia al portapapeles junto al valor. |
| **License Info (Subscription / Expiration / Radio ID / Licensed version)** | Radio | Muestra los detalles de la licencia de la radio. Cada campo incluye un botón de copia al portapapeles junto al valor. |
| **IP Address / Mask / MAC Address** | Network | Direcciones de red de solo lectura. Cada una incluye un botón de copia al portapapeles. |
| **Station Name** | Radio | Identifica este cliente AetherSDR para otras estaciones multiFLEX. Por defecto usa el nombre de host del SO si se deja vacío. Se almacena como `StationName`. Se envía a la radio como `client station <nombre>`. |
| **Select Installer...** | Radio | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en la versión 26.5.3. |
| **Reboot Radio** | Radio | Envía un comando de reinicio a la radio. Aparece primero un diálogo de confirmación. En conexiones LAN, AetherSDR se reconecta automáticamente una vez que la radio termina de iniciar. En conexiones SmartLink/WAN debe reconectarse manualmente. El botón está deshabilitado cuando la radio está desconectada. |
| **Network MTU:** | Network | Establece el tamaño máximo de paquete VITA-49 UDP saliente en bytes (576–9000). El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena como `NetworkMtu`. |
| **Enforce Private IP Connections:** | Network | Rechaza pares que no sean RFC1918. El botón de alternancia muestra "Enabled" cuando está marcado y "Disabled" cuando no lo está. |
| **TX Follows Active Slice** | TX | TX sigue al slice activo. Es mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. Se almacena como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | TX | Cambia el slice activo cuando TX se mueve externamente (ej. WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. |
| **Iambic:** | Phone/CW | Activa o desactiva el keyer iámbico en la radio. |
| **Iambic Mode: A / B** | Phone/CW | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Decode:** | Phone/CW | Activa la superposición de decodificación de CW en el panadapter. Se almacena como `CwDecodeOverlay`. Predeterminado: activado. |
| **10 MHz Reference Source:** | RX | Selecciona la fuente de referencia del oscilador. El cuadro combinado se llena dinámicamente: Auto siempre está presente; TCXO, GPSDO y External 10 MHz aparecen según lo que la radio reporte como instalado o actualmente activo. Si la radio envía `ext` para el ajuste o estado del oscilador, AetherSDR lo normaliza a `external` antes de mostrarlo. Cuando el ajuste es Auto y la radio ha seleccionado una fuente específica, la etiqueta muestra la resolución (por ejemplo, "Auto -> GPSDO"). El estado de bloqueo (Locked / Unlocked) se muestra en verde o rojo junto al cuadro combinado y se actualiza en vivo. Si se selecciona External 10 MHz pero no se detecta ninguna referencia externa, se añade "(not detected)" al texto de estado. |
| **Voice / CW / Digital filter sharpness sliders** | Filters | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El control deslizante se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Filters | Activa la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos** | APD | Selecciona la ruta de realimentación utilizada para muestrear la RF saliente para el entrenamiento APD de esa antena de TX. Elija una entrada externa de RX/XVTR cuando esté manejando un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Utiliza INTERNAL si la radio reporta un valor no reconocido. Predeterminado: INTERNAL. |
| **Equalizer Reset** | APD | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Se almacena como `AudioCompression`. Predeterminado: Auto. |
| **Prevent system sleep while connected** | Audio | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. Predeterminado: desactivado. |
| **Audio Boost:** | Audio | Activa ganancia adicional en la ruta de audio del lado del cliente. Se almacena como `AudioBoost`. |
| **Audio Buffer:** | Audio | Aumenta el búfer de audio (50–1000 ms) para absorber la fluctuación de VPN o SmartLink. Predeterminado: 200 ms. Se almacena como `AudioBufferMs`. |
| **Recording:** Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en la radio o en este ordenador. Se almacena como `RecordingMode`. Predeterminado: Radio Side. |
| **Save to:** | Audio | Ruta de la carpeta donde se guardan las grabaciones del lado del cliente. Se almacena como `QsoRecordingDir`. Predeterminado: `Documents/AetherSDR/Recordings`. |
| **Auto-record on TX** | Audio | Inicia automáticamente la grabación cada vez que la radio transmite. Se almacena como `QsoRecordingAutoRecord`. Predeterminado: desactivado. |
| **Idle timeout:** | Audio | Segundos de silencio (10–3600) tras los cuales una grabación activa se detiene automáticamente. Predeterminado: 120 s. Se almacena como `QsoRecordingIdleTimeout`. |
| **Connect / Disconnect (TGXL)** | Peripherals | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio que está rota en el firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de enclavamiento de hardware; no se necesita claveo del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. Si borra el campo IP y cierra el diálogo, la IP manual guardada y el puerto se eliminan para que el dispositivo ya no se reconecte automáticamente. Si borra el campo IP y hace clic en **Connect**, los ajustes guardados también se eliminan y la conexión se cancela. |
| **Connect / Disconnect (PGXL)** | Peripherals | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. Mismo comportamiento de borrado de IP que TGXL. |
| **Connect / Disconnect (Antenna Genius)** | Peripherals | Abre/cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo actualmente conectado. Mismo comportamiento de borrado de IP que TGXL. |
| **Connect / Disconnect (ShackSwitch)** | Peripherals | Abre/cierra una conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El descubrimiento automático a través de UDP también funciona sin introducir una dirección manualmente. La fila se oculta cuando un Antenna Genius estándar (no ShackSwitch) es el dispositivo conectado. Mismo comportamiento de borrado de IP que TGXL. |
| **⚙ Web UI (ShackSwitch)** | Peripherals | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, utiliza `SS_WebPort` o el puerto 5000. |
| **Connect / Disconnect (ACOM)** | Peripherals | Abre/cierra una conexión TCP directa a un amplificador ACOM (puerto predeterminado 10000). Guarda IP y puerto en `Acom_ManualIp` y `Acom_ManualPort` al conectar para que A
