# Activar grabación automática en TX y elegir una carpeta de guardado

Cuando la grabación automática en TX está habilitada, AetherSDR inicia automáticamente la grabación de audio cada vez que transmite y la detiene después de un tiempo de inactividad configurable. Esta página explica cómo activar esa función y elegir dónde se guardan las grabaciones.

## Antes de empezar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Decida si desea grabación del lado de la radio o del lado del cliente, ya que esto afecta dónde se captura el audio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio. La selección activa aparece resaltada. Esta opción se guarda en `RecordingMode`.
4. En el campo **Save to:**, escriba la ruta completa a su carpeta de grabaciones o haga clic en **...** para buscar una carpeta. La ruta se guarda en `QsoRecordingDir`.
5. Marque la casilla **Auto-record on TX**. Esto habilita la grabación automática cada vez que la radio pasa a transmitir. La configuración se guarda en `QsoRecordingAutoRecord`.
6. Establezca **Idle timeout:** en el número de segundos de silencio después del cual la grabación se detiene. El valor se guarda en `QsoRecordingIdleTimeout`.
7. Cierre el diálogo. La configuración entra en vigor inmediatamente.

## Qué hace cada control

| Control | Qué hace | Predeterminado |
|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en la radio o en esta PC. | Radio Side |
| **Save to:** | Ruta de carpeta donde se escriben los archivos de grabación. De forma predeterminada es Documents/AetherSDR/Recordings. | — |
| **...** | Abre un navegador de carpetas para seleccionar la ubicación de guardado. | — |
| **Auto-record on TX** | Cuando está marcada, la grabación se inicia automáticamente en cada transmisión y se detiene después de que transcurra el tiempo de inactividad. | Desmarcada |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga después de que TX termine. | 120 s |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. | Desactivado |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | Desactivado |
| **Deslizadores de agudeza de filtro Voice / CW / Digital** | Establece la agudeza del filtro (0=latencia más baja a 3=más agudo) por modo. El deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática de nivel de filtro para ese modo y deshabilita el deslizador de agudeza manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio dañada en firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de bloqueo de hardware; no se requiere clave del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado Connected solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra conexión a un interruptor de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El descubrimiento automático vía UDP también funciona sin esta fila. Fila oculta del estado Connected si Antenna Genius (que no es ShackSwitch) es el dispositivo conectado. | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa webPort de la baliza si > 1024, en caso contrario recurre a `SS_WebPort` o puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo .ssdr de firmware preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI vs MZ PE/COFF) y extrae el .ssdr sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; radios de series 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de retroalimentación que la radio usa para muestrear la RF saliente para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando controle un amplificador lineal externo. Las opciones se rellenan en tiempo real desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults |
| **Botones de color de slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter e insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles de actualización de firmware. En v0.9.3 el flujo de trabajo para preparar un archivo de firmware cambió.

### Verificación de actualizaciones

1. Haga clic en la pestaña **Radio** en Radio Setup.
2. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualización de FlexRadio.
3. Si una actualización está disponible, la etiqueta de estado muestra la versión disponible e indica que descargue el instalador SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo.
4. Si el firmware es actual, la etiqueta de estado confirma la versión instalada.

> **Nota:** En v0.9.3 el botón de descarga de un clic se eliminó. Debe descargar el instalador SmartSDR desde flexradio.com usted mismo, luego prepararlo usando **Select Installer...**.

### Preparación y carga de firmware

1. Descargue el instalador SmartSDR desde flexradio.com. Los tipos de archivo compatibles son .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo .ssdr de firmware preextraído.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos filtrado para esos tipos de archivo.
3. Seleccione el archivo descargado. AetherSDR detecta automáticamente el formato y extrae el .ssdr sin herramientas externas. Una barra de progreso y etiqueta de estado muestran el progreso de extracción.
4. Cuando la preparación se completa exitosamente, haga clic en **Upload Firmware** para transferir el firmware a la radio.

### Controles de actualización de firmware

| Control | Qué hace |
|---|---|
| **Check for Update** | Consulta el servidor de actualización de FlexRadio e informa si hay una versión de firmware más nueva disponible. |
| **Select Installer...** | Abre un selector de archivos que acepta archivos .msi, .exe o .ssdr. El preparador detecta automáticamente el formato y extrae el .ssdr. Cambiado de **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Transfiere el firmware preparado a la radio. Una barra de progreso y etiqueta de estado rastrean la carga. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz.

En v0.9.2.1 los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado dice "GPSDO installed. Manual frequency offset calibration available." (verde). Sin un GPSDO, la etiqueta dice "Manual frequency offset calibration available." (ámbar).

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<value>` cuando termina de editar el campo. |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración. Una etiqueta de estado junto al botón reporta el progreso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. Un indicador de estado de bloqueo en vivo (Locked / Unlocked) aparece junto al selector. |

### Inicio de una calibración

1. Haga clic en la pestaña **RX** en Radio Setup.
2. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para el progreso y resultado.
4. Cuando se completa la calibración, el botón se habilita nuevamente y la etiqueta de estado muestra el resultado.

> **Nota:** Dejar **Cal Frequency (MHz):** vacío y hacer clic en **Start** mostrará una advertencia ("Enter cal frequency") y no iniciará la calibración.

## Conexión de periféricos (pestaña Peripherals)

La pestaña **Peripherals** proporciona conexión IP manual para dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. Cada dispositivo tiene su propia fila con botones **Connect** y **Disconnect** y un campo de dirección IP.

### ShackSwitch

La fila ShackSwitch comparte la conexión AG subyacente con la fila Antenna Genius. Solo una de las dos filas muestra estado Connected a la vez, dependiendo de qué tipo de dispositivo está realmente conectado.

- La fila **Antenna Genius** muestra Connected solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch.
- La fila **ShackSwitch** muestra Connected solo cuando el dispositivo conectado es un ShackSwitch.

El botón **⚙ Web UI** abre la página de configuración web integrada del ShackSwitch directamente en el navegador de su sistema. AetherSDR determina la URL de la siguiente manera:

1. Si la baliza del dispositivo anuncia un puerto web mayor que 1024, se utiliza ese puerto.
2. En caso contrario, se utiliza el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000.
