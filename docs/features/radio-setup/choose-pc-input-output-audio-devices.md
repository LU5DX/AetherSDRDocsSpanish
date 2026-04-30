# Elegir dispositivos de entrada/salida de audio de la PC

Esta página explica cómo seleccionar qué dispositivos de audio de la PC utiliza AetherSDR para la salida de audio de recepción de radio y la entrada del micrófono. Debe hacerlo cuando configura AetherSDR por primera vez o cuando cambia auriculares, parlantes o interfaces de audio.

## Antes de empezar

- La radio debe estar conectada. Los controles de Radio Setup no están disponibles sin una conexión activa a la radio.
- Sepa qué dispositivos de entrada y salida de audio expone su PC (verifique la configuración de audio de su SO si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el dispositivo que desea usar para micrófono o entrada de audio.
4. Haga clic en el menú desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones surten efecto inmediatamente.

## Qué hace cada control

| Control | Qué hace | Predeterminado |
|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del equipo (micrófono, interfaz de audio, etc.). | Predeterminado del sistema |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del equipo (parlantes, auriculares, interfaz de audio, etc.). | Predeterminado del sistema |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Desactivado |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para absorber fluctuaciones en conexiones VPN o SmartLink. | 200 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio usado sobre SmartLink o LAN. | Auto |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en la radio o en el cliente. | Radio Side |
| **Save to:** | Carpeta donde se guardan las grabaciones del lado del cliente. De forma predeterminada, Documents/AetherSDR/Recordings. | — |
| **...** | Abre un navegador de carpetas para seleccionar el directorio de grabación. | — |
| **Auto-record on TX** | Inicia automáticamente la grabación cuando transmite. | Desactivado |
| **Idle timeout:** | Segundos de silencio después de los cuales una grabación activa se detiene automáticamente. | 120 s |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación en Split. | Desactivado |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | Desactivado |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=menor latencia a 3=más nitidez) por modo. Se deshabilita cuando Auto está habilitado para ese modo. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la dirección IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio interrumpida en firmware 4.2. TGXL controla el PTT de la radio a través de su cable de bloqueo de hardware; no se necesita control de tecla del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la dirección IP descubierta se rellena previamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda la dirección IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda la dirección IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. | Connect |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr preextraído. El firmware stager detecta automáticamente el formato de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. | — |
| **APD (tab)** | Configuración de muestreador externo de Predistorsión Adaptativa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que usa la radio para muestrear el RF saliente para entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando controle un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de interfaz — actualmente aloja la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets de VFO, superposiciones de panadapter y distintivos de canal de CAT. Los botones están deshabilitados cuando se selecciona **Use Aether defaults**. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | — |

## Cambios de actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware en la pestaña **Radio** ha cambiado en v0.9.3.

### Seleccionar un archivo de firmware

El botón **Browse .ssdr...** ha sido renombrado **Select Installer...**. Ahora acepta tres tipos de archivo:

- **.msi** — Instalador WiX de FlexRadio SmartSDR v4.2+
- **.exe** — instalador autoextraíble SmartSDR más antiguo
- **.ssdr** — archivo de firmware preextraído

El firmware stager detecta automáticamente el formato de los primeros 8 bytes del archivo (OLE/MSI magic para .msi, encabezado PE/COFF MZ para .exe) y extrae la carga útil .ssdr sin requerir herramientas externas. Un indicador de progreso y una etiqueta de estado se actualizan mientras avanza la extracción.

### Comportamiento de Check for Update

Cuando **Check for Update** encuentra una versión de firmware más nueva, la etiqueta de estado ahora lee:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com,  
> then click 'Select Installer...' to stage it.

En versiones anteriores, el botón **Check for Update** se reetiquetaba a **Download v***X.Y.Z* e activaba una descarga en la aplicación. Ese paso de descarga en la aplicación ha sido eliminado. Descargue el instalador manualmente desde flexradio.com, luego use **Select Installer...** para prepararlo.

### Pasos para actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update** para ver si hay una versión de firmware más nueva disponible.
4. Si hay una actualización disponible, descargue el instalador SmartSDR (.msi o .exe) desde flexradio.com.
5. Haga clic en **Select Installer...** y seleccione el instalador descargado o un archivo .ssdr preextraído.
6. Espere a que el stager extraiga y prepare el firmware. La etiqueta de estado muestra el progreso.
7. Haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Cambios de calibración de frecuencia en v0.9.2.1

El panel de calibración de la pestaña **RX** ha sido rediseñado. En versiones anteriores, el campo **Cal Frequency (MHz):**, el botón **Start** y los controles manuales **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. A partir de v0.9.2.1, estos controles siempre están visibles independientemente de si está instalado un GPSDO.

El indicador de estado en la parte superior del grupo de calibración ahora muestra:

- **Verde** — "GPSDO installed. Manual frequency offset calibration available." (GPSDO presente)
- **Ámbar** — "Manual frequency offset calibration available." (sin GPSDO)

### Cómo funciona la calibración ahora

Cuando hace clic en **Start**, AetherSDR:

1. Valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no procede.
2. Restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) antes de comenzar, para que cada ejecución de calibración comience desde una línea base conocida.
3. Deshabilita y reetiqueta el botón **Start** a **Busy** mientras la calibración está en progreso.
4. Envía `radio pll_start` y monitorea la respuesta. La etiqueta de estado se actualiza en vivo para reflejar el progreso (Starting… / running states / result).
5. Reabilita el botón **Start** cuando la calibración se completa o falla.

El botón **Start** es seguro de usar mientras está instalado un GPSDO; la referencia del GPSDO no se ve alterada.

Si navega fuera de la pestaña **RX** o cierra Radio Setup mientras la calibración está en ejecución, las devoluciones de llamada en progreso se descartan de forma segura — no se escribe estado parcial.

## Consejos

- Los menús desplegables Input y Output solo muestran los dispositivos que el SO expone actualmente. Si falta un dispositivo, conéctelo y reabra la pestaña Audio — la enumeración de dispositivos ocurre cuando la pestaña se muestra por primera vez.
- Si el audio de recepción suena muy bajo con su dispositivo de salida elegido, habilite **Audio Boost:** antes de aumentar el volumen del SO.
- En conexiones VPN o SmartLink, aumente **Audio Buffer:** para reducir caídas. Los valores superiores a 200 ms añaden un retraso notable.
- En la pestaña **RX**, siempre escriba una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):** antes de hacer clic en **Start**. Usar una frecuencia imprecisa produce una corrección de offset incorrecta.
- Para actualizar firmware en v0.9.3 y versiones posteriores, descargue el instalador SmartSDR desde flexradio.com primero. El paso de descarga en la aplicación ya no existe. Use **Select Installer...** para preparar el archivo que descargó.

## Solución de problemas

- **No aparecen dispositivos de audio en los menús desplegables** — La pestaña Audio enumera los dispositivos cuando se carga por primera vez. Cierre Radio Setup, verifique que el SO reconozca el dispositivo, luego reabra `Settings > Radio Setup...` y haga clic en la pestaña Audio nuevamente.
- **El audio de recepción se reproduce a través del dispositivo incorrecto** — El menú desplegable Output puede seguir establecido en un dispositivo seleccionado anteriormente. Abra la pestaña Audio y reseleccione la salida correcta.
- **El micrófono no es escuchado por la radio** — Confirme que el dispositivo correcto está seleccionado en el menú desplegable **Input:**, y que el SO no ha silenciado ni bloqueado el acceso a ese dispositivo.
- **El botón Start permanece etiquetado como Busy** — Una ejecución de calibración anterior no se completó. Cierre y reabra Radio Setup para restablecer el estado de calibración, luego intente de nuevo.
- **"Enter cal frequency" aparece cuando hago clic en Start** — Escriba una frecuencia válida en MHz en el campo **Cal Frequency (MHz):** antes de hacer clic en **Start**.
- **Select Installer... muestra un error o el botón Upload Firmware permanece deshabilitado** — El stager no pudo extraer un .ssdr válido del archivo seleccionado. Confirme que seleccionó el instalador SmartSDR correcto para su modelo de radio y que la descarga se completó sin errores, luego intente de nuevo.
- **La pestaña APD no es visible** —
