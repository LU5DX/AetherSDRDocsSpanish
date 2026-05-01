# Seleccionar dispositivos de entrada/salida de audio de la PC

Esta página explica cómo seleccionar qué dispositivos de audio de la PC utiliza AetherSDR para la salida de audio de recepción de radio y la entrada del micrófono. Debe hacerlo cuando configure AetherSDR por primera vez o cuando cambie auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- La radio debe estar conectada. Los controles de Radio Setup no están disponibles sin una conexión de radio activa.
- Conozca qué dispositivos de entrada y salida de audio expone su PC (verifique la configuración de audio del SO si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en la lista desplegable **Input:** y seleccione el dispositivo que desea usar para entrada de micrófono o audio.
4. Haga clic en la lista desplegable **Output:** y seleccione el dispositivo que desea usar para reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones toman efecto inmediatamente.

## Qué hace cada control

| Control | Qué hace | Predeterminado |
|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del host (micrófono, interfaz de audio, etc.). | Predeterminado del sistema |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del host (altavoces, auriculares, interfaz de audio, etc.). | Predeterminado del sistema |
| **Audio Boost:** | Aplica ganancia extra en la ruta de audio del cliente. | Apagado |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para absorber fluctuaciones en conexiones VPN o SmartLink. | 200 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado en SmartLink o LAN. | Auto |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en la radio o en el cliente. | Radio Side |
| **Save to:** | Carpeta donde se guardan las grabaciones del lado del cliente. Predeterminado: Documents/AetherSDR/Recordings. | — |
| **...** | Abre un navegador de carpetas para seleccionar el directorio de grabación. | — |
| **Auto-record on TX** | Inicia automáticamente la grabación cuando transmite. | Apagado |
| **Idle timeout:** | Segundos de silencio después de los cuales se detiene automáticamente una grabación activa. | 120 s |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación Split. | Apagado |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | Apagado |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo. Se desactiva cuando Auto está habilitado para ese modo. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática de nivel de filtro para ese modo y desactiva el deslizador de nitidez manual. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de bloqueo de hardware; no se requiere codificación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa previamente. | Conectar |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Conectar |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado Conectado solo cuando el dispositivo conectado es Antenna Genius y no un ShackSwitch. | Conectar |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en el mensaje de difusión AG. El autodescubrimiento vía UDP también funciona sin esta fila. La fila se oculta del estado 'Conectado' si Antenna Genius (no-ShackSwitch) es el dispositivo conectado. | Conectar |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza webPort del mensaje de difusión si es mayor a 1024; de lo contrario, recurre a `SS_WebPort` o puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato de los primeros 8 bytes (magia OLE/MSI versus encabezado MZ PE/COFF) y extrae el .ssdr sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador externo de Predistorsión Adaptativa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de restablecimiento del ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se cumplen en directo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y distintivos de canal CAT. Los botones se desactivan cuando **Use Aether defaults** está seleccionado. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — |

## Cambios de actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware en la pestaña **Radio** ha cambiado en v0.9.3.

### Seleccionar un archivo de firmware

El botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo:

- **.msi** — Instalador WiX FlexRadio SmartSDR v4.2+
- **.exe** — instalador autoextraíble SmartSDR antiguo
- **.ssdr** — archivo de firmware preextraído

El preparador de firmware detecta automáticamente el formato de los primeros 8 bytes del archivo (magia OLE/MSI para .msi, encabezado PE/COFF MZ para .exe) y extrae la carga .ssdr sin requerir herramientas externas. Un indicador de progreso y etiqueta de estado se actualizan a medida que procede la extracción.

### Comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más nueva, la etiqueta de estado ahora dice:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com,  
> then click 'Select Installer...' to stage it.

En versiones anteriores, el botón **Check for Update** se renombraba a **Download v***X.Y.Z* e activaba una descarga en la aplicación. Ese paso de descarga en la aplicación ha sido eliminado. Descargue el instalador manualmente desde flexradio.com, luego use **Select Installer...** para prepararlo.

### Pasos para actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update** para ver si hay disponible una versión de firmware más nueva.
4. Si hay una actualización disponible, descargue el instalador de SmartSDR (.msi o .exe) desde flexradio.com.
5. Haga clic en **Select Installer...** y seleccione el instalador descargado o un archivo .ssdr preextraído.
6. Espere a que el preparador extraiga y prepare el firmware. La etiqueta de estado muestra el progreso.
7. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Cambios de calibración de frecuencia en v0.9.2.1

El panel de calibración de la pestaña **RX** ha sido rediseñado. En versiones anteriores, el campo **Cal Frequency (MHz):**, botón **Start** y controles manuales **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. A partir de v0.9.2.1, estos controles siempre son visibles independientemente de si está instalado un GPSDO.

El indicador de estado en la parte superior del grupo de calibración ahora dice:

- **Verde** — "GPSDO installed. Manual frequency offset calibration available." (GPSDO presente)
- **Ámbar** — "Manual frequency offset calibration available." (sin GPSDO)

### Cómo funciona la calibración ahora

Cuando hace clic en **Start**, AetherSDR:

1. Valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no procede.
2. Restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) antes de comenzar, por lo que cada ejecución de calibración comienza desde una línea de base conocida.
3. Desactiva y renombra el botón **Start** a **Busy** mientras la calibración está en progreso.
4. Envía `radio pll_start` y monitorea la respuesta. La etiqueta de estado se actualiza en vivo para reflejar el progreso (Starting… / running states / result).
5. Reactiva el botón **Start** cuando la calibración se completa o falla.

El botón **Start** es seguro de usar mientras está instalado un GPSDO; la referencia GPSDO no se ve afectada.

Si navega fuera de la pestaña **RX** o cierra Radio Setup mientras la calibración se ejecuta, las devoluciones de llamada en progreso se descartan de forma segura — no se escribe estado parcial alguno.

## Cambios de ShackSwitch en v0.9.4

La pestaña **Peripherals** obtiene soporte explícito de ShackSwitch en v0.9.4.

### Comportamiento de la fila Antenna Genius

La fila **Connect / Disconnect (Antenna Genius)** ahora muestra estado Conectado solo cuando el dispositivo conectado es un verdadero Antenna Genius. Si se conecta un ShackSwitch, la fila Antenna Genius ya no reporta Conectado — la fila ShackSwitch refleja ese estado.

### Fila ShackSwitch

Se ha añadido una fila dedicada **Connect / Disconnect (ShackSwitch)**. Se conecta al ShackSwitch en puerto 9007 usando el protocolo de control AG. La dirección IP se guarda en `SS_ManualIp` y el puerto en `SS_ControlPort`. AetherSDR también puede descubrir automáticamente un ShackSwitch mediante el mensaje de difusión UDP sin usar esta fila.

### Botón Web UI

Un botón **⚙ Web UI** aparece junto a la fila ShackSwitch. Haga clic en él para abrir la interfaz web local del ShackSwitch en su navegador del sistema. AetherSDR determina el puerto de la siguiente manera:

1. Si el mensaje de difusión del dispositivo anuncia un `webPort` mayor a 1024, se utiliza ese puerto.
