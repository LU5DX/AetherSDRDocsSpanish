# Cambiar la radio entre DHCP e IP estática

Use esta página para cambiar cómo la FLEX-8600 obtiene su dirección de red — ya sea automáticamente mediante DHCP o con una IP estática fija, máscara de subred y puerta de enlace que usted especifique.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión activa con la radio.
- Si va a cambiar a IP estática, tenga a mano los valores de dirección IP, máscara de subred y puerta de enlace antes de comenzar.
- Cambiar la configuración de red hará que la radio se mueva a una nueva dirección. Deberá reconectarse después de aplicar los cambios.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Observe la **IP Address**, **Mask** y **MAC Address** actuales, que se muestran como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo. El botón refleja el modo actual; al hacer clic, cambia al otro.
5. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:** con los valores de su red.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Vuelva a conectarse a la radio en su nueva dirección usando `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestra las direcciones de red actuales de la radio. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática para asignar a la radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo estático. |
| **Apply** | Botón pulsador | Envía la configuración de red a la radio. |
| **Enforce Private IP Connections:** | Botón de alternancia | Rechaza pares que no sean RFC1918. |
| **Network MTU:** | Spinbox (576-9000 bytes, predeterminado 1450) | Establece el tamaño máximo del paquete UDP VITA-49 saliente en bytes. El valor predeterminado de 1450 es seguro para la mayoría de los túneles VPN/SD-WAN. Se almacena en AppSettings (`NetworkMtu`). |
| **TX Follows Active Slice** | Botón pulsador | TX sigue la segmento (slice) activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante una operación de división (Split). |
| **Active Slice Follows TX** | Botón pulsador | Cambia la segmento activo cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Controles deslizantes (0–3) | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El control deslizante se desactiva cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; desactiva el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón pulsador | Abre/cierra una conexión TCP directa con el TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en el firmware 4.2. El TGXL acciona el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita ninguna clave del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Botón pulsador | Abre/cierra una conexión TCP directa con el Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón pulsador | Abre/cierra la conexión con el Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (no un Antenna Genius estándar) es el dispositivo conectado. |
| **Connect / Disconnect (ShackSwitch)** | Botón pulsador | Abre/cierra la conexión con un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de transmisión de AG. El autodescubrimiento a través de UDP también funciona sin esta fila. La fila se oculta del estado Conectado si un Antenna Genius estándar (no ShackSwitch) es el dispositivo conectado. |
| **Web UI (ShackSwitch)** | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón pulsador | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (pestaña)** | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y las radios con versiones anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Combo de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada externa RX/XVTR cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón pulsador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (pestaña)** | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente alberga la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de color de la segmento entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por segmento. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Botones de color Slice A–H** | Botones pulsadores | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa segmento. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones están desactivados cuando está seleccionado **Use Aether defaults**. Hasta 8 segmentos. |
| **Reset All to Defaults (Themes)** | Botón pulsador | Restablece todos los colores personalizados de las segmentos a la paleta incorporada de AetherSDR. |
| **Enable/Disable the Level Meter During Receive** | Botón de alternancia | Muestra el medidor de nivel de micrófono incluso en RX. |
| **Iambic:** | Botón de alternancia | Habilita o deshabilita el manipulador iambic en la radio. |
| **Iambic Mode: A / B** | Botones pulsadores (mutuamente excluyentes) | Selecciona el modo iambic Curtis A o B tanto para la radio como para el manipulador de software local. |
| **Swap:** | Botón de alternancia | Intercambia dit/dah. |
| **Sideband:** | Cuadro combinado (LSB / USB) | Selecciona la banda lateral del tono CW. |
| **CWX:** | Botón de alternancia | Habilita la manipulación por macros CWX. |
| **Decode:** | Botón de alternancia (predeterminado True) | Habilita la superposición de decodificación CW en el panadapter. Se almacena como `CwDecodeOverlay`. |
| **RTTY Mark Default:** | Spinbox | Frecuencia de marca RTTY predeterminada. |
| **TX Band Settings** | Botón pulsador | Abre el diálogo dedicado de potencia/sintonización por banda. |
| **Timings (in ms)** | Spinbox | Temporizaciones de retardo/permanencia de TX. |
| **Interlocks - TX REQ: RCA / Accessory** | Botón de alternancia | Habilita las entradas de interbloqueo RCA y Accessory. |
| **Max Power:** | Spinbox (0-100 %) | Establece el límite de potencia de TX a nivel de radio. |
| **Tune Mode:** | Cuadro combinado | Selecciona cómo se comporta el botón de sintonización. |
| **Show TX in Waterfall:** | Botón de alternancia | Dibuja la señal de TX en el waterfall. |
| **Line Out:** | Control deslizante | Ganancia de salida de línea. |
| **Mute (Line Out)** | Botón pulsador | Silencia la salida de línea. |
| **Headphone:** | Control deslizante | Ganancia de auriculares. |
| **Mute (Headphone)** | Botón pulsador | Silencia los auriculares. |
| **Front Speaker: / Mute** | Botón pulsador | Silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Botón pulsador (predeterminado Auto) | Selecciona el códec de audio para SmartLink/LAN. Se almacena como `AudioCompression`. |
| **Prevent system sleep while connected** | Casilla de verificación (predeterminado False) | Mantiene el SO despierto mientras la radio está conectada para evitar caídas en los flujos de audio/TCP/UDP durante la inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| **PC Audio Devices: Input: / Output:** | Cuadro combinado | Elige los dispositivos de audio de entrada/salida del equipo anfitrión. |
| **Audio Boost:** | Botón de alternancia | Habilita ganancia adicional en la ruta de audio del cliente. Se almacena como `AudioBoost`. |
| **Audio Buffer:** | Campo de texto (predeterminado 200, rango 50-1000 ms) | Aumenta el búfer de audio en milisegundos para la fluctuación de VPN/SmartLink. Se almacena como `AudioBufferMs`. |
| **Recording: Radio Side / Client Side** | Botón pulsador (predeterminado Radio Side) | Elige la grabación del lado de la radio o del lado del cliente. Se almacena como `RecordingMode`. |
| **Save to:** | Campo de texto | Carpeta para las grabaciones guardadas (solo del lado del cliente). Se almacena como `QsoRecordingDir`. El valor predeterminado es Documentos/AetherSDR/Recordings. |
| **... (browse)** | Botón pulsador | Navega para buscar la carpeta de grabación. |
| **Auto-record on TX** | Casilla de verificación (predeterminado False) | Graba automáticamente mientras se transmite. Se almacena como `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Spinbox (predeterminado 120, rango 10-3600 seg) | Segundos de silencio antes de que se detenga la grabación. Se almacena como `QsoRecordingIdleTimeout`. |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Botones pulsadores | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. |

## Reconexión automática de periféricos y borrado de IP manual

Cuando ingresa una dirección IP para un periférico (TGXL, PGXL, Antenna Genius o ShackSwitch) y hace clic en **Connect**, la IP y el puerto se guardan en la configuración. En inicios posteriores, AetherSDR intenta automáticamente reconectarse a ese periférico.

Si borra el campo IP y hace clic en **Connect** mientras está desconectado, la IP y el puerto manuales guardados se eliminan de la configuración, evitando la reconexión automática al iniciar. Si borra el campo IP y cierra el diálogo **Radio Setup** sin hacer clic en Connect/Disconnect, la configuración guardada también se borra y cualquier conexión activa se desconecta, asegurando que los manejadores secundarios (como la visibilidad de los botones) vean el estado borrado.

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles para buscar actualizaciones de firmware y preparar un archivo de firmware para su carga.

### Cómo actualizar el firmware en v0.9.3

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** para abrir el selector de archivos. Seleccione el instalador que descargó, o un archivo `.ssdr` preextraído si ya tiene uno. El preparador detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. La etiqueta de estado se actualiza para mostrar el progreso de la preparación.
4. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y una etiqueta de estado siguen la carga.

> **Nota:** En v0.9.3, el botón anteriormente etiquetado como **Browse .ssdr...** pasó a llamarse **Select Installer...** y el selector de archivos ahora acepta archivos `.msi`, `.exe` y `.ssdr`. El botón **Check for Update** ya no cambia a un botón de descarga cuando se encuentra una actualización; usted descarga el instalador manualmente desde flex
