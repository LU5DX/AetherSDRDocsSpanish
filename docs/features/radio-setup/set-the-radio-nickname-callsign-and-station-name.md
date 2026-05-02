# Configurar el apodo, indicativo y nombre de estación del equipo

Configure un apodo legible, su indicativo y un nombre de estación en el FLEX-8600 conectado. Estos valores identifican el equipo y este cliente ante otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado al equipo. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar al equipo.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre al equipo de inmediato.
5. En el campo **Callsign**, escriba el indicativo de su estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en **Close** para cerrar el cuadro de diálogo.

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| **Nickname** | Etiqueta descriptiva para el equipo. Se envía al equipo como nombre del radio. | Nombre reportado por el equipo |
| **Callsign** | Indicativo de su estación, almacenado en el equipo. | _(vacío)_ |
| **Station Name** | Identifica este cliente de AetherSDR ante otras estaciones multiFLEX. | Nombre de host del SO |
| **TX Follows Active Slice** | La transmisión sigue al slice (canal) activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando la transmisión se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. | False |
| **Controles deslizantes Voice / CW / Digital filter sharpness** | Establece la nitidez del filtro (0=menor latencia a 3=máxima nitidez) por modo; el control se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado del equipo, que falló a partir del firmware 4.2. El TGXL controla el PTT del equipo mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo IP está vacío y el equipo ha detectado el TGXL, la IP detectada se completa automáticamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si el dispositivo conectado es un ShackSwitch (no un Antenna Genius estándar). | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre o cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (no ShackSwitch). | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el campo `webPort` de la baliza si es mayor que 1024; de lo contrario, usa `SS_WebPort` o el puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador de extracción automática anterior) o un archivo de firmware .ssdr ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. Etiqueta cambiada desde **Browse .ssdr...** en v0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador externo de predistorsión adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña se oculta a menos que el equipo reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; los equipos de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **Controles combinados ANT1 / ANT2 / XVTA / XVTB sampler (APD)** | Selecciona la ruta de retroalimentación que usa el equipo para muestrear la RF de salida en el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando use un amplificador lineal externo. Las opciones se cargan en tiempo real desde el subobjeto `apd sampler` del equipo. Vuelve a INTERNAL si el equipo reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` al equipo, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. | — |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores de los slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

Use los controles de actualización de firmware en la pestaña **Radio** para verificar y aplicar actualizaciones de firmware al equipo.

### Para verificar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión disponible e indica que debe descargar el instalador de SmartSDR desde flexradio.com y luego usar **Select Installer...** para prepararlo.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

### Para preparar y cargar el firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador de extracción automática anterior) o un archivo de firmware .ssdr ya extraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Open.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<filename\>..." y aparece la barra de progreso.
   - El preparador de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el contenido .ssdr sin herramientas externas.
   - Cuando la preparación finaliza, **Upload Firmware** se habilita.
3. Haga clic en **Upload Firmware** para enviar el firmware al equipo.
   - Una barra de progreso muestra el avance de la carga.
   - La etiqueta de estado informa el resultado cuando finaliza la carga.

> **Nota:** En v0.9.3, el botón anteriormente etiquetado como **Browse .ssdr...** fue renombrado a **Select Installer...** y extendido para aceptar paquetes de instalación .msi y .exe además de archivos .ssdr. También se eliminó la ruta de descarga y preparación automática que se activaba con un segundo clic en **Check for Update**; en su lugar, descargue el instalador manualmente desde flexradio.com.

### Controles de actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta al servidor de actualizaciones la última versión de firmware disponible. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo .msi, .exe o .ssdr. AetherSDR prepara el firmware automáticamente tras la selección. |
| **Upload Firmware** | Envía el firmware preparado al equipo. Se habilita solo después de que un archivo se haya preparado correctamente. |
| Etiqueta de estado del firmware | Vacía hasta que comienza una operación; luego muestra el progreso y el resultado. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** ofrece calibración manual de desplazamiento de frecuencia independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." en verde.
- Si no hay GPSDO instalado, la etiqueta de estado muestra "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** siempre se muestran.

### Para ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida en el campo **Cal Frequency (MHz)**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en curso.
   - Una etiqueta de estado junto al botón muestra el estado actual (por ejemplo, "Starting…").
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido de calibración.
5. Espere a que la etiqueta de estado reporte la finalización. El botón **Start** se vuelve a habilitar automáticamente.

### Comportamiento del campo Cal Frequency (MHz)

| Condición | Resultado |
|---|---|
| El campo está vacío al hacer clic en Start | La etiqueta de estado muestra "Enter cal frequency" en ámbar; la calibración no se inicia. |
| Se ingresa una frecuencia válida | AetherSDR envía `radio set cal_freq=<value>`, restablece el error de frecuencia a 0 ppb y luego inicia el barrido de calibración PLL. |

### Controles de la pestaña RX

| Control | Descripción | Predeterminado |
|---|---|---|
| **Cal Frequency (MHz)** | Frecuencia de referencia utilizada para la calibración manual. Siempre visible desde v0.9.2.1 en adelante, independientemente de la presencia de GPSDO. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. Se deshabilita y muestra la etiqueta **Busy** mientras hay una calibración en curso. | — |
| **Freq Offset (ppb)** | Desplazamiento de frecuencia manual en partes por mil millones. | — |
| **10 MHz Reference Source** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en tiempo real junto al selector. | Auto |

## Conexión a periféricos (pestaña Peripherals)

La pestaña **Peripherals** permite la conexión IP manual de dispositivos externos: TGXL, PGXL, Antenna Genius y ShackSwitch. Cada dispositivo tiene su propia fila con un botón Connect/Disconnect y un campo de dirección IP. AetherSDR guarda la IP y el puerto de cada dispositivo y reconecta automáticamente al iniciar.

### Para conectarse a un ShackSwitch
