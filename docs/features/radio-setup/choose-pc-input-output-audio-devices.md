# Selección de dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué dispositivos de audio del PC utiliza AetherSDR para la salida de audio de recepción y la entrada de micrófono. Es necesario realizar esta configuración la primera vez que se instala AetherSDR o cuando se cambia de auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- La radio debe estar conectada. Los controles de Radio Setup no están disponibles sin una conexión de radio activa.
- Conozca qué dispositivos de entrada y salida de audio expone su PC (consulte la configuración de audio del sistema operativo si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el dispositivo que desea usar para el micrófono o la entrada de audio.
4. Haga clic en el menú desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción del audio de recepción.
5. Cierre el diálogo. Las selecciones surten efecto de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado |
|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del sistema (micrófono, interfaz de audio, etc.). | System default |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del sistema (altavoces, auriculares, interfaz de audio, etc.). | System default |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Off |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para absorber la fluctuación en conexiones VPN o SmartLink. | 200 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado sobre SmartLink o LAN. | Auto |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en la radio o en el cliente. | Radio Side |
| **Save to:** | Carpeta donde se guardan las grabaciones del lado del cliente. El valor predeterminado es Documents/AetherSDR/Recordings. | — |
| **...** | Abre un explorador de carpetas para seleccionar el directorio de grabación. | — |
| **Auto-record on TX** | Inicia automáticamente la grabación al transmitir. | Off |
| **Idle timeout:** | Segundos de silencio tras los cuales se detiene automáticamente una grabación activa. | 120 s |
| **TX Follows Active Slice** | TX sigue al slice (canal de recepción) activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. | Off |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. | Off |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=mínima latencia a 3=máxima nitidez) por modo. Se deshabilita cuando Auto está habilitado para ese modo. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control manual de nitidez. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Es necesario para recuperar TUNE con firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de usar la ruta del lado de la radio que quedó rota en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y la radio ha detectado el TGXL, la IP detectada se rellena automáticamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected únicamente cuando el dispositivo conectado es un Antenna Genius y no un ShackSwitch. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado 'Connected' si el dispositivo conectado es un Antenna Genius (no ShackSwitch). | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del ShackSwitch en el navegador del sistema. Utiliza el webPort de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble anterior) o un archivo de firmware .ssdr ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (encabezado OLE/MSI para .msi, encabezado PE/COFF MZ para .exe) y extrae el archivo .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en la versión v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esta función; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente en el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando conecte un amplificador lineal externo. Las opciones se obtienen en tiempo real del sub-objeto `apd sampler` de la radio. Si la radio informa un valor no reconocido, recurre a INTERNAL. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de cero. | — |
| **Themes (tab)** | Pestaña de personalización de la interfaz — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los controles VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de slice a la paleta integrada de AetherSDR. | — |

## Cambios en el proceso de actualización de firmware en v0.9.3

El flujo de actualización de firmware en la pestaña **Radio** cambió en la versión v0.9.3.

### Selección de un archivo de firmware

El botón **Browse .ssdr...** ha sido renombrado **Select Installer...**. Ahora acepta tres tipos de archivos:

- **.msi** — instalador WiX de FlexRadio SmartSDR v4.2+
- **.exe** — instalador autoextraíble anterior de SmartSDR
- **.ssdr** — un archivo de firmware ya extraído

El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes del archivo (encabezado OLE/MSI para .msi, encabezado PE/COFF MZ para .exe) y extrae el contenido .ssdr sin requerir herramientas externas. Un indicador de progreso y una etiqueta de estado se actualizan conforme avanza la extracción.

### Comportamiento de Check for Update

Cuando **Check for Update** detecta una versión de firmware más reciente, la etiqueta de estado ahora muestra:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com,  
> then click 'Select Installer...' to stage it.

En versiones anteriores, el botón **Check for Update** cambiaba su etiqueta a **Download v***X.Y.Z* e iniciaba una descarga dentro de la aplicación. Ese paso de descarga en la aplicación ha sido eliminado. Descargue el instalador manualmente desde flexradio.com y luego use **Select Installer...** para prepararlo.

### Pasos para actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update** para verificar si hay una versión de firmware más reciente disponible.
4. Si hay una actualización disponible, descargue el instalador de SmartSDR (.msi o .exe) desde flexradio.com.
5. Haga clic en **Select Installer...** y seleccione el instalador descargado o un archivo .ssdr ya extraído.
6. Espere a que el preparador extraiga y prepare el firmware. La etiqueta de estado muestra el progreso.
7. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Cambios en la calibración de frecuencia en v0.9.2.1

El panel de calibración de la pestaña **RX** ha sido rediseñado. En versiones anteriores, el campo **Cal Frequency (MHz):**, el botón **Start** y los controles manuales **Freq Offset (ppb):** se ocultaban cuando se detectaba un GPSDO. A partir de la versión v0.9.2.1, estos controles son siempre visibles independientemente de si hay un GPSDO instalado.

El indicador de estado en la parte superior del grupo de calibración ahora muestra:

- **Verde** — "GPSDO installed. Manual frequency offset calibration available." (GPSDO presente)
- **Ámbar** — "Manual frequency offset calibration available." (sin GPSDO)

### Cómo funciona ahora la calibración

Al hacer clic en **Start**, AetherSDR:

1. Valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no continúa.
2. Restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) antes de comenzar, de modo que cada ejecución de calibración parta de una línea base conocida.
3. Deshabilita y cambia la etiqueta del botón **Start** a **Busy** mientras la calibración está en curso.
4. Envía `radio pll_start` y supervisa la respuesta. La etiqueta de estado se actualiza en tiempo real para reflejar el progreso (Starting… / estados en ejecución / resultado).
5. Vuelve a habilitar el botón **Start** cuando la calibración se completa o falla.

El botón **Start** es seguro de usar mientras hay un GPSDO instalado; la referencia del GPSDO no se ve afectada.

Si navega fuera de la pestaña **RX** o cierra Radio Setup mientras la calibración está en curso, las retrollamadas en progreso se descartan de forma segura — no se escribe ningún estado parcial.

## Cambios de ShackSwitch en v0.9.4

La pestaña **Peripherals** incorpora soporte explícito para ShackSwitch en la versión v0.9.4.

### Comportamiento de la fila Antenna Genius

La fila **Connect / Disconnect (Antenna Genius)** ahora muestra el estado Connected únicamente cuando el dispositivo conectado es un Antenna Genius verdadero. Si en cambio hay un ShackSwitch conectado, la fila de Antenna Genius ya no reporta Connected — el estado se refleja en la fila de ShackSwitch.

### Fila ShackSwitch

Se ha agregado una fila dedicada **Connect / Disconnect (ShackSwitch)**. Se conecta al ShackSwitch en el puerto 9007 usando el protocolo de control AG. La dirección IP se guarda en `SS_ManualIp` y el puerto en `SS_ControlPort`. AetherSDR también puede descubrir un ShackSwitch automáticamente mediante la baliza de difusión UDP sin necesidad de usar esta fila.

### Botón Web UI

Un botón **⚙ Web UI** aparece junto a la fila de ShackSwitch. Haga clic en él para abrir la interfaz web local del ShackSwitch en el navegador del sistema. AetherSDR determina el puerto de la siguiente manera:

1. Si la baliza del dispositivo anuncia un `webPort` mayor que 1024, se utiliza ese puerto.
