# Establezca el apodo de radio, indicativo y nombre de estación

Establezca un apodo legible, su indicativo y un nombre de estación en la FLEX-8600 conectada. Estos valores identifican la radio y este cliente ante otras estaciones multiFLEX en la red.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio inmediatamente.
5. En el campo **Callsign**, escriba su indicativo de estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como el nombre de la radio. | Nombre reportado por la radio |
| **Callsign** | Su indicativo de estación, almacenado en la radio. | _(vacío)_ |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. | Nombre de host del sistema operativo |
| **TX Follows Active Slice** | La TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia mínima a 3=más nítido) por modo; el deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta de lado de radio `tgxl autotune handle=<H>` rota en firmware 4.2. El TGXL controla PTT de la radio a través de su cable de bloqueo de hardware; no se necesita marcado de lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, se completa previamente la IP descubierta. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (no un Antenna Genius estándar) es el dispositivo conectado. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra conexión a un interruptor de antena ShackSwitch a través del protocolo AG UDP/TCP en puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en el faro AG. El descubrimiento automático a través de UDP también funciona sin esta fila. La fila se oculta del estado Connected si un Antenna Genius (sin ShackSwitch) es el dispositivo conectado. | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del faro si es mayor a 1024; de lo contrario, retrocede a `SS_WebPort` o puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta instaladores .msi (instalador WiX FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o archivo .ssdr de firmware preextraído. El planificador de firmware detecta automáticamente el formato de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta se cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador de Predistorsión Adaptativa Externa — selección de puerto de muestra de retroalimentación por antena TX (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y pre-4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que utiliza la radio para muestrear la RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa al controlar un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Retrocede a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience nuevamente. | — |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color del slice entre la paleta integrada AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter y insignias de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta integrada AetherSDR. | — |

## Actualización de firmware (Pestaña Radio)

Utilice los controles de actualización de firmware en la pestaña **Radio** para verificar e aplicar actualizaciones de firmware a la radio.

### Para verificar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e instruye descargar el instalador SmartSDR desde flexradio.com, luego usar **Select Installer...** para procesarlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

### Para procesar y cargar firmware

1. Descargue el instalador SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo), o archivo .ssdr de firmware preextraído.
2. Haga clic en **Select Installer...**
   - Se abre el selector de archivos con el filtro configurado en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Open.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<filename\>..." y aparece la barra de progreso.
   - El planificador de firmware detecta automáticamente el formato de archivo de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae la carga .ssdr sin herramientas externas.
   - Cuando el procesamiento se completa, **Upload Firmware** se habilita.
3. Haga clic en **Upload Firmware** para enviar el firmware a la radio.
   - Una barra de progreso rastrea la carga.
   - La etiqueta de estado reporta el resultado cuando la carga finaliza.

> **Nota:** En v0.9.3, el botón anteriormente etiquetado **Browse .ssdr...** se renombró a **Select Installer...** y se extendió para aceptar paquetes instaladores .msi y .exe además de archivos .ssdr. La ruta de descarga y procesamiento automático que se activaba con un segundo clic en **Check for Update** también se eliminó; descargue el instalador manualmente desde flexradio.com en su lugar.

### Controles de actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta al servidor de actualización la última versión de firmware disponible. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo .msi, .exe, o .ssdr. AetherSDR procesa el firmware automáticamente después de la selección. |
| **Upload Firmware** | Envía el firmware procesado a la radio. Se habilita solo después de que un archivo se ha procesado exitosamente. |
| Firmware status label | Vacío hasta que comienza una operación, luego muestra texto de progreso y resultado. |

## Calibración de frecuencia (Pestaña RX)

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia independientemente de si un GPSDO está instalado.

- Si un GPSDO está instalado, la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." en verde.
- Si no hay GPSDO instalado, la etiqueta de estado lee "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** siempre se muestran.

### Para ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida en el campo **Cal Frequency (MHz)**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se realiza la calibración.
   - Una etiqueta de estado junto al botón muestra el estado actual (por ejemplo, "Starting…").
   - AetherSDR reinicia el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido de calibración.
5. Espere a que la etiqueta de estado reporte finalización. El botón **Start** se habilita automáticamente.

### Comportamiento del campo Cal Frequency (MHz)

| Condición | Resultado |
|---|---|
| El campo está vacío cuando se hace clic en Start | La etiqueta de estado muestra "Enter cal frequency" en ámbar; la calibración no comienza. |
| Frecuencia válida ingresada | AetherSDR envía `radio set cal_freq=<value>`, reinicia el error de frecuencia a 0 ppb, luego inicia el barrido de calibración PLL. |

### Controles de la pestaña RX

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Cal Frequency (MHz)** | Frecuencia de referencia utilizada para calibración manual. Siempre se muestra desde v0.9.2.1 en adelante, independientemente de la presencia de GPSDO. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. Se deshabilita y se etiqueta **Busy** mientras se ejecuta una calibración. | — |
| **Freq Offset (ppb)** | Desplazamiento de frecuencia manual en partes por mil millones. | — |
| **10 MHz Reference Source** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO, o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en vivo junto al selector. | Auto |

## Conexión a periféricos (Pestaña Peripherals)

La pestaña **Peripherals** proporciona conexión manual por IP para dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. Cada dispositivo tiene su propia fila con un botón Connect/Disconnect y un campo de dirección IP. AetherSDR guarda la IP y puerto para cada dispositivo y se reconecta automáticamente al inicio.

### Para conectar a un ShackSwitch
