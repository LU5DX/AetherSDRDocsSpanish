# Establecer el apodo, indicativo y nombre de estación de la radio

Establezca un apodo legible, su indicativo y un nombre de estación en la FLEX-8600 conectada. Estos valores identifican la radio y este cliente ante otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio de inmediato.
5. En el campo **Callsign**, escriba su indicativo de estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica a este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en el botón de cerrar de la ventana o presione Escape para descartar el diálogo.

## Características de la ventana de diálogo

El diálogo Radio Setup utiliza una ventana sin marco con una barra de título personalizada que incluye áreas arrastrables y controles de ventana estándar. La apariencia sin marco respeta la configuración de aplicación `FramelessWindow`; cuando está habilitada (valor predeterminado), el diálogo carece de la barra de título del sistema operativo y utiliza la barra de título personalizada de AetherSDR. Cuando está deshabilitada, el diálogo utiliza las decoraciones de ventana estándar del sistema operativo.

## Función de cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como nombre de la radio. | Nombre reportado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(en blanco)_ |
| **Station Name** | Identifica a este cliente AetherSDR ante otras estaciones multiFLEX. | Nombre de host del SO |
| **TX Follows Active Slice** | TX sigue la slice activa. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. | Falso |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | Falso |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el control deslizante está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que está rota en firmware 4.2. El TGXL activa PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita activación desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (no un Antenna Genius estándar) es el dispositivo conectado. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de difusión de AG. La auto-detección mediante UDP también funciona sin esta fila. La fila se oculta del estado Connected si un Antenna Genius (no ShackSwitch) es el dispositivo conectado. | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr pre-extraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador externo de Predistorsión Adaptativa (APD): selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de restablecimiento del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. | — |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF de salida para el entrenamiento APD de esa antena TX. Elija una entrada externa RX/XVTR cuando se utilice un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. | — |
| **Themes (pestaña)** | Pestaña de personalización de interfaz de usuario — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores de slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles de inmediato en los widgets VFO, superposiciones del panadapter y etiquetas de canales CAT. Los botones están deshabilitados cuando está seleccionado **Use Aether defaults**. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de slice a la paleta integrada de AetherSDR. | — |
| **Network MTU:** | Establece el tamaño máximo de paquete UDP VITA-49 saliente en bytes. El valor predeterminado 1450 es seguro para la mayoría de túneles VPN/SD-WAN. Almacenado en AppSettings. | 1450 |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para SmartLink/LAN. | Auto |
| **Prevent system sleep while connected** | Mantiene el SO despierto mientras la radio está conectada para evitar caídas de flujo de audio/TCP/UDP durante la inactividad. | Falso |
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | — |
| **Audio Buffer:** | Aumenta el búfer de audio en milisegundos para compensar la fluctuación en VPN/SmartLink. Almacenado como `AudioBufferMs`. | 200 |
| **Recording: Radio Side / Client Side** | Elige la grabación del lado de la radio o del lado del cliente. | Radio Side |
| **Save to:** | Carpeta para grabaciones guardadas (solo lado del cliente). | Documents/AetherSDR/Recordings |
| **Auto-record on TX** | Graba automáticamente mientras transmite. | Falso |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga. | 120 |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. | — |
| **Iambic:** | Habilita o deshabilita el manipulador iámbico en la radio. | — |
| **Iambic Mode: A / B** | Selecciona el modo iámbico Curtis A o B tanto para la radio como para el manipulador de software local. Par mutuamente excluyente. | A |
| **Decode:** | Habilita la superposición de decodificación CW en el panadapter. | Verdadero |
| **Campos IP/puerto de Periféricos** | Cuando el campo IP está vacío mientras está desconectado, hacer clic en **Connect** no hace nada; en su lugar, elimina cualquier IP manual previamente guardada de la configuración, evitando la reconexión automática al inicio. Cuando el diálogo se cierra con un campo IP vacío y existe una IP manual previamente guardada, la IP guardada se elimina automáticamente y el dispositivo se desconecta si está conectado actualmente. | — |
| **Acciones de botón FlexControl** | El mapeo de acciones de botón incluye nuevas acciones de rueda: WheelRit y WheelXit. Estas mapean la perilla de sintonización FlexControl para ajustar los desplazamientos RIT y XIT respectivamente. | — |

## Actualización de firmware (pestaña Radio)

Use los controles de actualización de firmware en la pestaña **Radio** para buscar y aplicar actualizaciones de firmware a la radio.

### Para buscar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com, y luego use **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

### Para preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr pre-extraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Abrir.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<filename\>..." y aparece la barra de progreso.
   - El gestor de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae la carga útil .ssdr sin herramientas externas.
   - Cuando la preparación está completa, **Upload Firmware** se habilita.
3. Haga clic en **Upload Firmware** para enviar el firmware a la radio.
   - Una barra de progreso rastrea la carga.
   - La etiqueta de estado reporta el resultado cuando la carga finaliza.

> **Nota:** En v0.9.3, el botón anteriormente etiquetado **Browse .ssdr...** fue renombrado a **Select Installer...** y ampliado para aceptar paquetes instaladores .msi y .exe además de archivos .ssdr. También se eliminó la ruta de descarga y preparación automática que se activaba con un segundo clic en **Check for Update**; descargue el instalador manualmente desde flexradio.com.

### Controles de actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta el servidor de actualizaciones para la versión de firmware más reciente disponible. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo .msi, .exe o .ssdr. AetherSDR prepara el firmware automáticamente después de la selección. |
| **Upload Firmware** | Envía el firmware preparado a la radio. Habilitado solo después de que un archivo se haya preparado exitosamente. |
| Etiqueta de estado de firmware | Vacía hasta que comienza una operación, luego muestra texto de progreso y resultado. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." en verde.
- Si no hay GPSDO instalado, la etiqueta de estado muestra "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** siempre se muestran.

### Para ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida en el campo **Cal Frequency (MHz)**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en progreso.
   - Una etiqueta de estado junto al botón muestra el estado actual (por ejemplo, "Starting…").
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido de calibración.
5. Espere a que la etiqueta de estado indique finalización. El botón **Start** se vuelve a habilitar automáticamente.

### Comportamiento del campo Cal Frequency (MHz)

| Condición | Resultado |
|---|---|
| El campo está vacío al hacer clic en Start | La etiqueta de estado muestra "Enter cal frequency" en ámbar; la calibración no se inicia. |
| Se ingresa una frecuencia válida | AetherSDR envía `radio set cal_freq=<valor>`, restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración PLL. |

### Controles de la pestaña RX

| Control | Descripción
