# Seleccionar dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué dispositivos de audio del PC utiliza AetherSDR para la salida de audio de recepción de radio y la entrada de micrófono. Debe hacer esto cuando configure AetherSDR por primera vez o cuando cambie de auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- La radio debe estar conectada. Los controles de configuración de la radio no están disponibles sin una conexión de radio activa.
- Sepa qué dispositivos de audio de entrada y salida expone su PC (consulte la configuración de audio de su sistema operativo si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en la lista desplegable **Input:** y seleccione el dispositivo que desea usar para la entrada de micrófono o audio.
4. Haga clic en la lista desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones surten efecto inmediatamente.

## Función de cada control

| Control | Qué hace | Valor predeterminado |
|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de audio de entrada del equipo anfitrión (micrófono, interfaz de audio, etc.). | Predeterminado del sistema |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de audio de salida del equipo anfitrión (altavoces, auriculares, interfaz de audio, etc.). | Predeterminado del sistema |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Desactivado |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para absorber la fluctuación en conexiones VPN o SmartLink. | 200 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en la radio o en el cliente. | Radio Side |
| **Save to:** | Carpeta donde se guardan las grabaciones del lado del cliente. El valor predeterminado es Documentos/AetherSDR/Recordings. | — |
| **...** | Abre un explorador de carpetas para seleccionar el directorio de grabación. | — |
| **Auto-record on TX** | Inicia automáticamente la grabación cuando transmite. | Desactivado |
| **Idle timeout:** | Segundos de silencio tras los cuales una grabación activa se detiene automáticamente. | 120 s |
| **TX Follows Active Slice** | TX sigue la slice activa. Excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante una operación de Split. | Desactivado |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Excluyente con **TX Follows Active Slice**. | Desactivado |
| **Control deslizante de nitidez de filtro Voz / CW / Digital** | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo. Deshabilitado cuando Auto está habilitado para ese modo. | — |
| **Auto (Voz / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio, la cual está rota en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita ninguna activación en el lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado de Conectado solo cuando el dispositivo conectado es un Antenna Genius y no un ShackSwitch. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo 'ShackSwitch' en la baliza de difusión de AG. El descubrimiento automático mediante UDP también funciona sin esta fila. Fila oculta del estado 'Conectado' si el dispositivo conectado es un Antenna Genius (que no sea ShackSwitch). | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el webPort de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador de predistorsión adaptativa externa: selección por antena de TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. | — |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD de esa antena de TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz de usuario. Actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores de las slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults |
| **Botones de color de Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones están deshabilitados cuando está seleccionada la opción **Use Aether defaults**. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — |

## Cambios en la actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware en la pestaña **Radio** ha cambiado en v0.9.3.

### Selección de un archivo de firmware

El botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo:

- **.msi** — Instalador WiX de FlexRadio SmartSDR v4.2+
- **.exe** — Instalador SmartSDR autoextraíble antiguo
- **.ssdr** — Un archivo de firmware preextraído

El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes del archivo (magia OLE/MSI para .msi, cabecera PE/COFF MZ para .exe) y extrae la carga útil .ssdr sin necesidad de herramientas externas. Un indicador de progreso y una etiqueta de estado se actualizan durante la extracción.

### Comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más reciente, la etiqueta de estado ahora muestra:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com,  
> then click 'Select Installer...' to stage it.

En versiones anteriores, el botón **Check for Update** se renombraba a **Download v***X.Y.Z* e iniciaba una descarga dentro de la aplicación. Ese paso de descarga integrada se ha eliminado. Descargue el instalador manualmente desde flexradio.com y luego use **Select Installer...** para prepararlo.

### Pasos para actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update** para ver si hay disponible una versión de firmware más reciente.
4. Si hay una actualización disponible, descargue el instalador SmartSDR (.msi o .exe) desde flexradio.com.
5. Haga clic en **Select Installer...** y seleccione el instalador descargado o un archivo .ssdr preextraído.
6. Espere a que el gestor extraiga y prepare el firmware. La etiqueta de estado muestra el progreso.
7. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Cambios en la calibración de frecuencia en v0.9.2.1

El panel de calibración de la pestaña **RX** ha sido rediseñado. En versiones anteriores, el campo **Cal Frequency (MHz):**, el botón **Start** y los controles manuales **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. A partir de v0.9.2.1, estos controles están siempre visibles, independientemente de si hay un GPSDO instalado.

El indicador de estado en la parte superior del grupo de calibración ahora muestra:

- **Verde** — "GPSDO installed. Manual frequency offset calibration available." (GPSDO presente)
- **Ámbar** — "Manual frequency offset calibration available." (sin GPSDO)

### Cómo funciona la calibración ahora

Cuando hace clic en **Start**, AetherSDR:

1. Valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no continúa.
2. Restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) antes de comenzar, de modo que cada ejecución de calibración comience desde una línea base conocida.
3. Deshabilita y vuelve a etiquetar el botón **Start** como **Busy** mientras la calibración está en curso.
4. Envía `radio pll_start` y monitorea la respuesta. La etiqueta de estado se actualiza en vivo para reflejar el progreso (Starting… / estados en ejecución / resultado).
5. Vuelve a habilitar el botón **Start** cuando la calibración se completa o falla.

El botón **Start** es seguro de usar mientras hay un GPSDO instalado; la referencia del GPSDO no se ve alterada.

Si navega fuera de la pestaña **RX** o cierra Radio Setup mientras la calibración se está ejecutando, las devoluciones de llamada en curso se descartan de forma segura; no se escribe ningún estado parcial.

## Cambios en la fuente de referencia de 10 MHz en v0.9.7

El cuadro combinado **10 MHz Reference Source:** en la pestaña **RX** se ha actualizado. La lista de opciones y la etiqueta de estado de bloqueo ahora se completan dinámicamente según el hardware que la radio informa como presente o activo.

### Comportamiento de la lista de opciones

Anteriormente, el cuadro combinado se completaba una vez cuando se construía la pestaña RX, e incluía solo opciones para el hardware detectado en ese momento (TCXO, GPSDO, External). A partir de v0.9.7, la lista se actualiza cada vez que cambia el estado del oscilador de la radio:

- **Auto** está siempre presente.
- **TCXO** aparece cuando la radio informa que hay hardware TCXO presente, cuando la configuración o el estado activo actual es TCXO, o siempre que la radio haya informado algún estado del oscilador.
- **GPSDO** aparece cuando la radio informa que hay hardware GPSDO presente, o cuando la configuración o el estado activo actual es GPSDO.
- **External 10 MHz** aparece cuando la radio informa que hay una referencia externa presente, cuando la configuración o el estado activo actual es externo, o siempre que la radio haya informado algún estado del oscilador.

La etiqueta utilizada anteriormente **External** ha sido renombrada a **External 10 MHz**.

### Etiqueta de estado de bloqueo

La etiqueta de estado de bloqueo se actualiza en tiempo real junto al cuadro combinado y muestra:

- **Locked** (verde) cuando la fuente de referencia seleccionada está bloqueada.
- **Unlocked** (rojo) cuando la fuente de referencia seleccionada está desbloqueada o la radio no bloquea esa fuente.

## Cambios en el diálogo Radio Setup en v26.5.1

El diálogo Radio Setup se ha actualizado con una barra de título personalizada y soporte para ventana sin bordes.

### Modo de ventana sin bordes

El diálogo Radio Setup ahora utiliza una barra de título personalizada cuando AetherSDR se ejecuta en modo de ventana sin bordes. La barra de título muestra el título de la ventana "Radio Setup" y proporciona los controles de ventana estándar (minimizar, maximizar, cerrar).

Cuando **FramelessWindow** está habilitado en la configuración (valor predeterminado: True):

- El diálogo utiliza una barra de título dibujada personalizada en lugar del marco de ventana del sistema operativo.
- Se instalan controladores de cambio de tamaño a lo largo de todos los bordes y esquinas para redimensionar la ventana manualmente.
- Arrastrar la barra de título mueve la ventana.

Cuando el modo sin bordes está deshabilitado, el diálogo utiliza la decoración de ventana estándar del sistema operativo.

### Comportamiento de guardar al cerrar en la pestaña Peripherals

Los botones **Connect / Disconnect** en la pestaña **Peripherals** ahora tienen un manejo mejorado para campos de dirección IP vacíos:

- **Borrar una IP guardada mientras está conectado:** Si borra el campo IP y hace clic en **Disconnect**, la configuración de IP y puerto manuales guardados se borra *antes* de que se ejecute la desconexión. Esto garantiza que los controladores posteriores (por ejemplo, la visibilidad del botón ShackSwitch) vean la configuración borrada de inmediato.
- **Borrar una IP guard
