# Elegir dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué dispositivos de audio del PC utiliza AetherSDR para la salida de audio de recepción de radio y la entrada de micrófono. Debe hacer esto cuando configure AetherSDR por primera vez o cuando cambie de auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- La radio debe estar conectada. Los controles de configuración de radio no están disponibles sin una conexión de radio activa.
- Sepa qué dispositivos de entrada y salida de audio expone su PC (consulte la configuración de audio de su sistema operativo si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en la lista desplegable **Input:** y seleccione el dispositivo que desea usar para la entrada de micrófono o audio.
4. Haga clic en la lista desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones surten efecto de inmediato.

## Función de cada control

| Control | Función | Valor predeterminado |
|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del anfitrión (micrófono, interfaz de audio, etc.). | Predeterminado del sistema |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del anfitrión (altavoces, auriculares, interfaz de audio, etc.). | Predeterminado del sistema |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Desactivado |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para absorber fluctuaciones en conexiones VPN o SmartLink. | 200 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado en SmartLink o LAN. | Auto |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en la radio o en el cliente. | Radio Side |
| **Save to:** | Carpeta donde se guardan las grabaciones del lado del cliente. El valor predeterminado es Documentos/AetherSDR/Recordings. | — |
| **...** | Abre un explorador de carpetas para seleccionar el directorio de grabación. | — |
| **Auto-record on TX** | Inicia la grabación automáticamente cuando transmite. | Desactivado |
| **Idle timeout:** | Segundos de silencio tras los cuales una grabación activa se detiene automáticamente. | 120 s |
| **TX Follows Active Slice** | TX sigue a la franja activa. Es mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación en Split. | Desactivado |
| **Active Slice Follows TX** | Cambia la franja activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. | Desactivado |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=mínima latencia a 3=máxima nitidez) por modo. Desactivado cuando Auto está habilitado para ese modo. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y desactiva el control deslizante de nitidez manual. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio, la cual está dañada en firmware 4.2. El TGXL activa la PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita señalización del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado "Connected" solo cuando el dispositivo conectado es un Antenna Genius y no un ShackSwitch. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en el beacon de difusión de AG. El descubrimiento automático mediante UDP también funciona sin esta fila. La fila se oculta del estado "Connected" si el dispositivo conectado es un Antenna Genius (que no es ShackSwitch). | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el webPort del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs encabezado PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador de Predistorsión Adaptativa Externa (APD): selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y las radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. | — |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF de salida para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz de usuario; actualmente aloja la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color de las franjas entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por franja. | Use Aether defaults |
| **Botones de color de franja A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa franja. Los cambios son visibles de inmediato en los widgets de VFO, superposiciones del panadapter y etiquetas de canal CAT. Los botones están desactivados cuando se selecciona **Use Aether defaults**. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de franja personalizados a la paleta integrada de AetherSDR. | — |

## Cambios en la actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware en la pestaña **Radio** ha cambiado en v0.9.3.

### Selección de un archivo de firmware

El botón **Browse .ssdr...** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo:

- **.msi** — Instalador WiX de FlexRadio SmartSDR v4.2+
- **.exe** — Instalador SmartSDR autoextraíble antiguo
- **.ssdr** — Un archivo de firmware preextraído

El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes del archivo (magia OLE/MSI para .msi, encabezado PE/COFF MZ para .exe) y extrae la carga útil .ssdr sin requerir herramientas externas. Un indicador de progreso y una etiqueta de estado se actualizan a medida que avanza la extracción.

### Comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más reciente, la etiqueta de estado ahora muestra:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com,  
> then click 'Select Installer...' to stage it.

En versiones anteriores, el botón **Check for Update** se volvía a etiquetar como **Download v***X.Y.Z***** y activaba una descarga dentro de la aplicación. Ese paso de descarga en la aplicación se ha eliminado. Descargue el instalador manualmente desde flexradio.com, luego use **Select Installer...** para prepararlo.

### Pasos para actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update** para ver si hay una versión de firmware más reciente disponible.
4. Si hay una actualización disponible, descargue el instalador de SmartSDR (.msi o .exe) desde flexradio.com.
5. Haga clic en **Select Installer...** y seleccione el instalador descargado o un archivo .ssdr preextraído.
6. Espere a que el preparador extraiga y prepare el firmware. La etiqueta de estado muestra el progreso.
7. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Cambios en la calibración de frecuencia en v0.9.2.1

El panel de calibración de la pestaña **RX** ha sido rediseñado. En versiones anteriores, el campo **Cal Frequency (MHz):**, el botón **Start** y los controles manuales de **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. A partir de v0.9.2.1, estos controles siempre están visibles, independientemente de si hay un GPSDO instalado.

El indicador de estado en la parte superior del grupo de calibración ahora muestra:

- **Verde** — "GPSDO installed. Manual frequency offset calibration available." (GPSDO presente)
- **Ámbar** — "Manual frequency offset calibration available." (sin GPSDO)

### Cómo funciona la calibración ahora

Cuando hace clic en **Start**, AetherSDR:

1. Valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calificación no procede.
2. Restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) antes de comenzar, para que cada ejecución de calibración comience desde una línea base conocida.
3. Desactiva y vuelve a etiquetar el botón **Start** como **Busy** mientras la calibración está en curso.
4. Envía `radio pll_start` y monitorea la respuesta. La etiqueta de estado se actualiza en vivo para reflejar el progreso (Starting… / estados en ejecución / resultado).
5. Vuelve a habilitar el botón **Start** cuando la calibración se completa o falla.

El botón **Start** es seguro de usar mientras hay un GPSDO instalado; la referencia del GPSDO no se ve afectada.

Si navega fuera de la pestaña **RX** o cierra Radio Setup mientras la calibración se está ejecutando, las devoluciones de llamada en curso se descartan de forma segura; no se escribe ningún estado parcial.

## Cambios en la fuente de referencia de 10 MHz en v0.9.7

El cuadro combinado **10 MHz Reference Source:** en la pestaña **RX** ha sido actualizado. La lista de opciones y la etiqueta de estado de bloqueo ahora se rellenan dinámicamente según el hardware que la radio informa como presente o activo.

### Comportamiento de la lista de opciones

Anteriormente, el cuadro combinado se poblaba una vez cuando se construía la pestaña RX y solo incluía opciones para el hardware detectado en ese momento (TCXO, GPSDO, External). A partir de v0.9.7, la lista se actualiza cada vez que cambia el estado del oscilador de la radio:

- **Auto** está siempre presente.
- **TCXO** aparece cuando la radio informa hardware TCXO presente, cuando la configuración actual o el estado activo es TCXO, o siempre que la radio haya informado algún estado del oscilador.
- **GPSDO** aparece cuando la radio informa hardware GPSDO presente, o cuando la configuración actual o el estado activo es GPSDO.
- **External 10 MHz** aparece cuando la radio informa una referencia externa presente, cuando la configuración actual o el estado activo es externo, o siempre que la radio haya informado algún estado del oscilador.

La etiqueta utilizada anteriormente, **External**, ha sido renombrada a **External 10 MHz**.

### Etiqueta de estado de bloqueo

El bloqueo
