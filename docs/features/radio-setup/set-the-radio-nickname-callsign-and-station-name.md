# Configurar el apodo, indicativo y nombre de estación de la radio

Configure un apodo legible, su indicativo y un nombre de estación en la FLEX-8600 conectada. Estos valores identifican la radio y este cliente para otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio inmediatamente.
5. En el campo **Callsign**, escriba el indicativo de su estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica a este cliente para otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como nombre de la radio. | Nombre reportado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(en blanco)_ |
| **Station Name** | Identifica a este cliente AetherSDR para otras estaciones multiFLEX. | Nombre de host del SO |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante una operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |
| **Deslizadores de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Es necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, rota en firmware 4.2. El TGXL maneja PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita activación desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (no un Antenna Genius estándar) es el dispositivo conectado. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antenas ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en el beacon de difusión AG. El autodescubrimiento mediante UDP también funciona sin esta fila. La fila se oculta del estado Conectado si un Antenna Genius (no ShackSwitch) es el dispositivo conectado. | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (marca OLE/MSI vs. PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **Combo de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se obtienen en vivo del subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, eliminando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz de usuario — actualmente aloja la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores de los slices entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones de panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de los slices a la paleta incorporada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

Utilice los controles de actualización de firmware en la pestaña **Radio** para verificar y aplicar actualizaciones de firmware a la radio.

### Para verificar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

### Para preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Abrir.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<nombre_archivo\>..." y aparece la barra de progreso.
   - El gestor de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (marca OLE/MSI vs. PE/COFF MZ) y extrae el payload .ssdr sin herramientas externas.
   - Cuando la preparación está completa, **Upload Firmware** se habilita.
3. Haga clic en **Upload Firmware** para enviar el firmware a la radio.
   - Una barra de progreso rastrea la carga.
   - La etiqueta de estado informa el resultado cuando la carga finaliza.

> **Nota:** En v0.9.3, el botón anteriormente etiquetado como **Browse .ssdr...** fue renombrado a **Select Installer...** y ampliado para aceptar paquetes instaladores .msi y .exe además de archivos .ssdr. También se eliminó la ruta de descarga y preparación automática que se activaba con un segundo clic en **Check for Update**; descargue el instalador manualmente desde flexradio.com.

### Controles de actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta el servidor de actualizaciones para obtener la versión de firmware más reciente disponible. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo .msi, .exe o .ssdr. AetherSDR prepara el firmware automáticamente después de la selección. |
| **Upload Firmware** | Envía el firmware preparado a la radio. Habilitado solo después de que un archivo se haya preparado exitosamente. |
| Etiqueta de estado del firmware | Vacía hasta que comienza una operación, luego muestra el progreso y el texto del resultado. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual del desplazamiento de frecuencia independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." en verde.
- Si no hay GPSDO instalado, la etiqueta de estado lee "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** siempre se muestran.

### Para ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida en el campo **Cal Frequency (MHz)**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en progreso.
   - Una etiqueta de estado junto al botón muestra el estado actual (por ejemplo, "Starting…").
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido de calibración.
5. Espere a que la etiqueta de estado indique que se ha completado. El botón **Start** se vuelve a habilitar automáticamente.

### Comportamiento del campo Cal Frequency (MHz)

| Condición | Resultado |
|---|---|
| El campo está vacío cuando se hace clic en Start | La etiqueta de estado muestra "Enter cal frequency" en ámbar; la calibración no comienza. |
| Se ingresa una frecuencia válida | AetherSDR envía `radio set cal_freq=<valor>`, restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración PLL. |

### Controles de la pestaña RX

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Cal Frequency (MHz)** | Frecuencia de referencia utilizada para la calibración manual. Siempre se muestra a partir de v0.9.2.1, independientemente de la presencia de GPSDO. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. Deshabilitado y etiquetado como **Busy** mientras se ejecuta una calibración. | — |
| **Freq Offset (ppb)** | Desplazamiento de frecuencia manual en partes por billón. | — |
| **10 MHz Reference Source** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External 10 MHz. Las opciones mostradas dependen del hardware instalado y del estado del oscilador reportado por la radio. El combo se rellena dinámicamente: Auto siempre está presente; TCXO aparece cuando la radio reporta un TCXO o el estado del oscilador está disponible; GPSDO aparece cuando hay un GPSDO presente; External 10 MHz aparece cuando se detecta una referencia externa o el estado del oscilador está disponible. Si la radio reporta `ext` como valor del oscilador, se trata como `external`. El estado de bloqueo se actualiza en vivo junto al selector — verde cuando está bloqueado, rojo cuando está desbloqueado. Cuando se selecciona Auto |
