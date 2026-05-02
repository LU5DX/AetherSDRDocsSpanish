# Habilitar la grabación automática en TX y seleccionar una carpeta de destino

Cuando la grabación automática en TX está habilitada, AetherSDR inicia la grabación de audio automáticamente cada vez que transmite y la detiene tras un tiempo de inactividad configurable. Esta página explica cómo activar esa función y elegir dónde se guardan las grabaciones.

## Antes de comenzar

- El radio debe estar conectado. Radio Setup requiere una conexión activa con el radio.
- Decida si desea grabación en el lado del radio o en el lado del cliente, ya que esto afecta dónde se captura el audio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Bajo **Recording:**, haga clic en **Radio Side** o en **Client Side** para seleccionar dónde se captura el audio. La selección activa se resalta. Esta elección se guarda en `RecordingMode`.
4. En el campo **Save to:**, escriba la ruta completa a su carpeta de grabaciones, o haga clic en **...** para buscar una carpeta. La ruta se guarda en `QsoRecordingDir`.
5. Active la casilla **Auto-record on TX**. Esto habilita la grabación automática cada vez que el radio pasa al modo de transmisión. El ajuste se guarda en `QsoRecordingAutoRecord`.
6. Configure **Idle timeout:** con el número de segundos de silencio tras los cuales se detiene la grabación. El valor se guarda en `QsoRecordingIdleTimeout`.
7. Cierre el cuadro de diálogo. Los ajustes surten efecto de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado |
|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en el radio o en este PC. | Radio Side |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. Por defecto es Documents/AetherSDR/Recordings. | — |
| **...** | Abre un explorador de carpetas para seleccionar la ubicación de guardado. | — |
| **Auto-record on TX** | Cuando está activada, la grabación comienza automáticamente en cada transmisión y se detiene tras transcurrir el tiempo de inactividad. | Desactivada |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga tras finalizar el TX. | 120 s |
| **TX Follows Active Slice** | El TX sigue al slice (canal de recepción) activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. | Off |
| **Active Slice Follows TX** | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | Off |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0=menor latencia a 3=mayor nitidez) por modo. El control se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que quedó interrumpida en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de enclavamiento hardware; no se requiere manipulación en el lado del cliente. Si el campo de IP está vacío y el radio ha descubierto el TGXL, la IP detectada se rellena automáticamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre o cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de difusión AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (no ShackSwitch). | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el webPort del beacon si es > 1024; de lo contrario, usa `SS_WebPort` o el puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI frente a PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en la versión 0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de restablecimiento del ecualizador. La pestaña se oculta si el radio no reporta `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ lo expone; los radios de la serie 6000 y los anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de retroalimentación que usa el radio para muestrear la RF saliente en el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se cargan en tiempo real desde el subobjeto `apd sampler` del radio. Vuelve a INTERNAL si el radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. | — |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores del slice (canal) entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles para la actualización de firmware. En la versión 0.9.3 cambió el flujo de trabajo para preparar un archivo de firmware.

### Verificar actualizaciones

1. Haga clic en la pestaña **Radio** en Radio Setup.
2. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
3. Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que debe descargar el instalador de SmartSDR desde flexradio.com y luego usar **Select Installer...** para prepararlo.
4. Si el firmware está actualizado, la etiqueta de estado confirma la versión instalada.

> **Nota:** En la versión 0.9.3 se eliminó el botón de descarga con un solo clic. Debe descargar el instalador de SmartSDR desde flexradio.com por su cuenta y luego prepararlo con **Select Installer...**.

### Preparar y cargar el firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. Los tipos de archivo admitidos son .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo de firmware .ssdr ya extraído.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos filtrado para esos tipos de archivo.
3. Seleccione el archivo descargado. AetherSDR detecta automáticamente el formato y extrae el .ssdr sin herramientas externas. Una barra de progreso y una etiqueta de estado muestran el avance de la extracción.
4. Cuando la preparación se complete correctamente, haga clic en **Upload Firmware** para transferir el firmware al radio.

### Controles de actualización de firmware

| Control | Función |
|---|---|
| **Check for Update** | Consulta el servidor de actualizaciones de FlexRadio e informa si hay una versión de firmware más reciente disponible. |
| **Select Installer...** | Abre un selector de archivos que acepta archivos .msi, .exe o .ssdr. El preparador detecta el formato automáticamente y extrae el .ssdr. Cambió de **Browse .ssdr...** en la versión 0.9.3. |
| **Upload Firmware** | Transfiere el firmware preparado al radio. Una barra de progreso y una etiqueta de estado siguen el avance de la carga. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** ofrece calibración manual del desplazamiento de frecuencia y selección de la fuente de referencia de 10 MHz.

En la versión 0.9.2.1, los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (en verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (en ámbar).

### Controles de calibración

| Control | Función |
|---|---|
| **Cal Frequency (MHz):** | Introduzca la frecuencia de referencia conocida en MHz. El valor se envía al radio como `radio set cal_freq=<value>` al terminar de editar el campo. |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) y luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en curso. Una etiqueta de estado junto al botón informa el progreso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. Junto al selector aparece un indicador de estado de bloqueo en tiempo real (Locked / Unlocked). |

### Iniciar una calibración

1. Haga clic en la pestaña **RX** en Radio Setup.
2. Introduzca la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para ver el progreso y el resultado.
4. Cuando la calibración finalice, el botón se vuelve a habilitar y la etiqueta de estado muestra el resultado.

> **Nota:** Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, aparecerá una advertencia ("Enter cal frequency") y la calibración no comenzará.

## Conexión de periféricos (pestaña Peripherals)

La pestaña **Peripherals** permite la conexión manual por IP de dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. Cada dispositivo tiene su propia fila con botones **Connect** y **Disconnect** y un campo de dirección IP.

### ShackSwitch

La fila de ShackSwitch comparte la conexión AG subyacente con la fila de Antenna Genius. Solo una de las dos filas muestra el estado Connected en un momento dado, dependiendo del tipo de dispositivo que esté realmente conectado.

- La fila **Antenna Genius** muestra Connected solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch.
- La fila **ShackSwitch** muestra Connected solo cuando el dispositivo conectado es un ShackSwitch.

El botón **⚙ Web UI** abre la página de configuración web integrada del ShackSwitch directamente en el navegador del sistema. AetherSDR determina la URL de la siguiente manera:

1. Si el beacon del dispositivo anuncia un puerto web superior a 1024, se usa ese puerto.
2. De lo contrario, se usa el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000.
