<!-- Traducción al español siguiendo las reglas establecidas -->

# Descripción General de Configuración de la Radio

El diálogo Configuración de la Radio es la ventana de configuración central para su FLEX-8600. Reúne identificación de la radio, red, GPS, transmisión, audio, filtros, transvertidores, cables USB, periféricos, nombres de antenas, temas de colores de slices y configuración serial de FlexControl en un solo lugar. Ábralo cada vez que necesite cambiar algo sobre cómo AetherSDR interactúa con el hardware de su radio.

## Antes de empezar

- La radio debe estar conectada. La Configuración de la Radio requiere una conexión activa con la radio.

## Cómo funciona

Abra Configuración de la Radio desde `Settings > Radio Setup...`. El diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área distinta de configuración. Las pestañas que no sean Radio cargan su contenido la primera vez que hace clic en ellas.

El diálogo recuerda su tamaño y posición entre sesiones usando `PersistentDialog`. Una barra de título con el texto "Radio Setup" aparece en la parte superior. Puede arrastrar la barra de título para mover el diálogo.

También puede saltar directamente a pestañas específicas:

- `Settings > USB Cables...` abre Configuración de la Radio con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre Configuración de la Radio con la pestaña **Serial** activa (solo disponible cuando el soporte de puerto serie está incorporado).

### Pestañas de un vistazo

| Pestaña | Qué configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones licenciadas, apodo, indicativo, nombre de estación, información de licencia y actualización de firmware. |
| **Network** | Dirección IP (DHCP o estática), MTU de red y aplicación de IP privada. |
| **GPS** | Estado GPS en vivo: latitud, longitud, altitud, hora y conteo de satélites. |
| **TX** | Temporizaciones de retardo/espera de TX, enclavamientos, límite de potencia global, modo de sintonía, visualización de TX en waterfall, comportamiento de seguimiento TX/slice y un acceso directo a ajustes por banda. |
| **Phone/CW** | Medidor de nivel de micrófono, keyer iambic (modo A/B, intercambio, banda lateral), CWX, decodificador CW y valor predeterminado de marca RTTY. |
| **RX** | Calibración de compensación de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración siempre están visibles; cuando hay un GPSDO instalado, la etiqueta de estado confirma su presencia. |
| **Antennas** | Visualización y cambio de nombre de puertos de antena (ANT1, ANT2, XVTA, XVTB) según lo reconocido por la radio. |
| **Audio** | Niveles de línea de salida, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio del PC; realce de audio; tamaño del búfer de audio; modo de grabación, carpeta, grabación automática en TX y tiempo de espera por inactividad; control del contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia versus filtro nítido por ancho de banda, y una opción separada para modos digitales. |
| **XVTR** | Configuración por transverter; crear o eliminar entradas de transverter. |
| **APD** | Configuración del muestreador de Predistorsión Adaptativa Externa: selección del puerto de retroalimentación por antena de TX y reinicio del ecualizador. Visible solo en radios FLEX-8x00 que reportan `apd configurable=1` (firmware SmartSDR 4.2.18+). |
| **USB Cables** | Asignar adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT y configurar sus parámetros serie. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. |
| **Themes** | Esquema de color de slices: cambiar entre la paleta AetherSDR incorporada y colores personalizados por slice (A–H). |
| **Serial** | Selección de puerto serie FlexControl, parámetros de línea, asignaciones de función de pin (DTR/RTS), intercambio de paddle, apertura automática y detección de perilla de sintonía. (Visible solo cuando el soporte de puerto serie está incorporado). |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistentes o comportamientos notables.

| Control | Pestaña | Comportamiento |
|---|---|---|
| **Station Name** | Radio | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. Por defecto toma el nombre de host del SO si se deja vacío. Se almacena como `StationName`. Se envía a la radio como `client station <nombre>`. |
| **Select Installer...** | Radio | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **Network MTU:** | Network | Establece el tamaño máximo de paquete UDP VITA-49 de salida en bytes (576–9000). El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Se almacena como `NetworkMtu`. |
| **TX Follows Active Slice** | TX | TX sigue al slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. Se almacena como `TxFollowsActiveSlice`. |
| **Active Slice Follows TX** | TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. Se almacena como `ActiveFollowsTxSlice`. |
| **Iambic Mode: A / B** | Phone/CW | Selecciona el modo iambic Curtis A o B tanto para la radio como para el keyer de software local. Par mutuamente excluyente. Predeterminado: A. |
| **Decode:** | Phone/CW | Activa la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. Predeterminado: activado. |
| **10 MHz Reference Source:** | RX | Selecciona la fuente de referencia del oscilador. El cuadro combinado se completa dinámicamente: Auto siempre está presente; TCXO, GPSDO y External 10 MHz aparecen según lo que la radio reporta como instalado o actualmente activo. Si la radio envía `ext` para el ajuste o estado del oscilador, AetherSDR lo normaliza a `external` antes de mostrarlo. Cuando el ajuste es Auto y la radio ha seleccionado una fuente específica, la etiqueta muestra la resolución (por ejemplo, "Auto -> GPSDO"). El estado de bloqueo (Locked / Unlocked) se muestra en verde o rojo junto al cuadro combinado y se actualiza en vivo. Si se selecciona External 10 MHz pero no se detecta ninguna referencia externa, se añade "(not detected)" al texto de estado. |
| **Voice / CW / Digital filter sharpness sliders** | Filters | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador está desactivado cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Filters | Activa la selección automática del nivel de filtro para ese modo; desactiva el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos** | APD | Selecciona la ruta de retroalimentación utilizada para muestrear la RF de salida para el entrenamiento APD para esa antena de TX. Elija una entrada externa de RX/XVTR cuando maneje un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. Predeterminado: INTERNAL. |
| **Equalizer Reset** | APD | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado a través de SmartLink o LAN. Se almacena como `AudioCompression`. Predeterminado: Auto. |
| **Prevent system sleep while connected** | Audio | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. Predeterminado: desactivado. |
| **Audio Boost:** | Audio | Activa ganancia adicional en la ruta de audio del lado del cliente. Se almacena como `AudioBoost`. |
| **Audio Buffer:** | Audio | Aumenta el búfer de audio (50–1000 ms) para absorber fluctuaciones de VPN o SmartLink. Predeterminado: 200 ms. Se almacena como `AudioBufferMs`. |
| **Recording:** Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en la radio o en este ordenador. Se almacena como `RecordingMode`. Predeterminado: Radio Side. |
| **Save to:** | Audio | Ruta de carpeta donde se guardan las grabaciones del lado del cliente. Se almacena como `QsoRecordingDir`. Predeterminado: `Documents/AetherSDR/Recordings`. |
| **Auto-record on TX** | Audio | Inicia automáticamente la grabación cada vez que la radio transmite. Se almacena como `QsoRecordingAutoRecord`. Predeterminado: desactivado. |
| **Idle timeout:** | Audio | Segundos de silencio (10–3600) tras los cuales una grabación activa se detiene automáticamente. Predeterminado: 120 s. Se almacena como `QsoRecordingIdleTimeout`. |
| **Connect / Disconnect (TGXL)** | Peripherals | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL maneja el PTT de la radio a través de su cable de interconexión de hardware; no se necesita keying del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. Si limpia el campo IP y cierra el diálogo, la IP manual y el puerto guardados se eliminan para que el dispositivo ya no se reconecte automáticamente. Si limpia el campo IP y hace clic en **Connect**, los ajustes guardados también se eliminan y la conexión se cancela. |
| **Connect / Disconnect (PGXL)** | Peripherals | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. Mismo comportamiento de limpieza de IP que TGXL. |
| **Connect / Disconnect (Antenna Genius)** | Peripherals | Abre/cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo actualmente conectado. Mismo comportamiento de limpieza de IP que TGXL. |
| **Connect / Disconnect (ShackSwitch)** | Peripherals | Abre/cierra una conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. El ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento a través de UDP también funciona sin necesidad de introducir una dirección manualmente. La fila se oculta cuando un Antenna Genius estándar (no ShackSwitch) es el dispositivo conectado. Mismo comportamiento de limpieza de IP que TGXL. |
| **⚙ Web UI (ShackSwitch)** | Peripherals | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, utiliza `SS_WebPort` o el puerto 5000. |
| **Use Aether defaults / Custom colors** | Themes | Cambia el esquema de color de los slices entre la paleta AetherSDR incorporada y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. Predeterminado: Use Aether defaults. |
| **Slice A–H color buttons** | Themes | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones de panadapter e insignias de canal CAT. Los botones están desactivados cuando **Use Aether defaults** está seleccionado. Se admiten hasta 8 slices. |
| **Reset All to Defaults** | Themes | Restablece todos los colores personalizados de slices a la paleta AetherSDR incorporada. |

## 10 MHz Reference Source (pestaña RX)

El cuadro combinado **10 MHz Reference Source:** en la pestaña RX se comporta de manera diferente en v0.9.7 en comparación con versiones anteriores. Anteriormente enumeraba solo las fuentes detectadas físicamente al abrir el diálogo y mostraba una etiqueta simple "Locked / Unlocked". El nuevo comportamiento es:

- **Población dinámica.** El cuadro combinado siempre contiene Auto. TCXO, GPSDO y External 10 MHz se añaden siempre que la radio los reporta como presentes, como el ajuste actual o como el estado actual del oscilador. Los elementos no se eliminan mientras el diálogo está abierto, incluso si la radio deja de reportarlos momentáneamente.

## Limpieza del Campo IP de Periféricos

En la pestaña Peripherals, las tres filas de dispositivos (TGXL, PGXL, Antenna Genius/ShackSwitch) ahora permiten limpiar una dirección IP manual guardada previamente:

- **Limpie el campo IP y cierre el diálogo.** Si el campo IP está vacío cuando cierra Configuración de la Radio (haciendo clic en el botón de cerrar ventana o presionando Esc), cualquier IP manual y puerto guardados para ese dispositivo se eliminan de la configuración. Si el dispositivo está actualmente conectado, se desconecta. El resultado es que el dispositivo ya no se reconecta automáticamente en el próximo inicio.
- **Limpie el campo IP y haga clic en Connect.** Si el campo IP está vacío cuando hace clic en **Connect**, la IP manual y el puerto guardados se eliminan y la conexión se cancela. Esto evita borrar accidentalmente los ajustes guardados y luego no hacer nada.
- **Limpie el campo IP y haga clic en Disconnect.** Si desconecta un dispositivo mientras el campo IP ya está vacío, la IP manual y el puerto guardados se eliminan primero.
