# Establezca el apodo de la radio, indicativo y nombre de estación

Establezca un apodo legible, su indicativo y un nombre de estación en la FLEX-8600 conectada. Estos valores identifican la radio y este cliente para otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los controles de la pestaña Radio no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar a la radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre a la radio inmediatamente.
5. En el campo **Callsign**, escriba el indicativo de su estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica este cliente para otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| **Nickname** | Etiqueta amigable para la radio. Se envía a la radio como nombre de la radio. | Nombre reportado por la radio |
| **Callsign** | Su indicativo de estación, guardado en la radio. | _(vacío)_ |
| **Station Name** | Identifica este cliente AetherSDR para otras estaciones multiFLEX. | Nombre de host del sistema operativo |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante operación Split. | False |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador se desactiva cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; desactiva el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` en la conexión para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio que está rota en firmware 4.2. El TGXL controla PTT de la radio a través de su cable de bloqueo de hardware; no se requiere modulación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se pre-completa. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. | Connect |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo .ssdr de firmware pre-extraído. El firmware stager detecta automáticamente el formato de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (tab)** | Configuración de muestreador de Pre-Distorsión Adaptativa externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de restablecimiento de ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y pre-4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Si la radio reporta un valor no reconocido, vuelve a INTERNAL. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de interfaz — actualmente aloja la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Alterna el esquema de color de slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asigne un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter y insignias de canal CAT. Los botones se desactivan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

Utilice los controles de actualización de firmware en la pestaña **Radio** para verificar e aplicar actualizaciones de firmware a la radio.

### Para verificar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si una actualización está disponible, la etiqueta de estado muestra el número de versión disponible e le instruye a descargar el instalador SmartSDR de flexradio.com, luego use **Select Installer...** para almacenarlo en caché.
   - Si el firmware está actualizado, la etiqueta de estado confirma la versión actual en verde.

### Para almacenar en caché y cargar firmware

1. Descargue el instalador SmartSDR de flexradio.com. AetherSDR acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo), o un archivo .ssdr de firmware pre-extraído.
2. Haga clic en **Select Installer...**
   - El selector de archivos se abre con el filtro establecido en `*.msi *.exe *.ssdr`.
   - Seleccione el archivo descargado y haga clic en Open.
   - AetherSDR comienza a preparar el firmware automáticamente. La etiqueta de estado muestra "Preparing firmware from \<filename\>..." y aparece la barra de progreso.
   - El firmware stager detecta automáticamente el formato de archivo de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae la carga útil .ssdr sin herramientas externas.
   - Cuando el almacenamiento en caché se complete, **Upload Firmware** se activa.
3. Haga clic en **Upload Firmware** para enviar el firmware a la radio.
   - Una barra de progreso rastrea la carga.
   - La etiqueta de estado reporta el resultado cuando la carga finaliza.

> **Nota:** En v0.9.3 el botón anteriormente etiquetado como **Browse .ssdr...** fue renombrado a **Select Installer...** y extendido para aceptar paquetes de instalador .msi y .exe además de archivos .ssdr. La ruta automática de descarga y almacenamiento en caché que había sido activada por un segundo clic en **Check for Update** también fue eliminada; descargue el instalador manualmente de flexradio.com en su lugar.

### Controles de actualización de firmware

| Control | Descripción |
|---|---|
| **Check for Update** | Consulta el servidor de actualización para la versión de firmware más reciente disponible. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo .msi, .exe, o .ssdr. AetherSDR almacena el firmware en caché automáticamente después de la selección. |
| **Upload Firmware** | Envía el firmware almacenado en caché a la radio. Se activa solo después de que un archivo haya sido almacenado en caché exitosamente. |
| Etiqueta de estado de firmware | Vacía hasta que comienza una operación, luego muestra texto de progreso y resultado. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de compensación de frecuencia independientemente de si está instalado un GPSDO.

- Si un GPSDO está instalado, la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." en verde.
- Si no hay GPSDO instalado, la etiqueta de estado lee "Manual frequency offset calibration available." en ámbar.

En ambos casos el campo **Cal Frequency (MHz)** y el botón **Start** siempre se muestran.

### Para ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida en el campo **Cal Frequency (MHz)**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se desactiva mientras la calibración está en progreso.
   - Una etiqueta de estado junto al botón muestra el estado actual (por ejemplo, "Starting…").
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido de calibración.
5. Espere a que la etiqueta de estado reporte finalización. El botón **Start** se activa automáticamente.

### Comportamiento del campo Cal Frequency (MHz)

| Condición | Resultado |
|---|---|
| El campo está vacío cuando se hace clic en Start | La etiqueta de estado muestra "Enter cal frequency" en ámbar; la calibración no comienza. |
| Frecuencia válida ingresada | AetherSDR envía `radio set cal_freq=<value>`, restablece el error freq a 0 ppb, luego inicia el barrido de calibración PLL. |

### Controles de la pestaña RX

| Control | Descripción | Predeterminado |
|---|---|---|
| **Cal Frequency (MHz)** | Frecuencia de referencia utilizada para calibración manual. Siempre se muestra a partir de v0.9.2.1 en adelante, independientemente de la presencia de GPSDO. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. Se desactiva y se etiqueta **Busy** mientras se ejecuta una calibración. | — |
| **Freq Offset (ppb)** | Compensación manual de frecuencia en partes por billón. | — |
| **10 MHz Reference Source** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO, o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en vivo junto al selector. | Auto |

## Consejos

- Si **Nickname** se deja en blanco, AetherSDR pre-completa el campo con el nombre reportado por la radio desde la red.
- **Station Name** se establece por defecto al nombre de host del sistema operativo cuando no se ha guardado ningún valor. Para restaurar el predeterminado, borre el campo y presione Tab — luego reingrese el nombre de host manualmente si es necesario.
- Los cambios en **Nickname** y **Callsign** se envían a la radio en el momento en que sale de cada campo. No se requiere un paso separado de Save o Apply.
- **Station Name** se guarda localmente en la configuración de AetherSDR y también se envía a la radio como identificador de cliente de estación para multiFLEX.
- Antes de v0.9.2.1, el campo **Cal Frequency** y el botón **Start** estaban ocultos cuando se instalaba un GPSDO. Ahora siempre están disponibles.
- En v0.9.3, **Select Installer...** reemplaza el botón anterior **Browse .ssdr...** y acepta paquetes de instalador .msi y .exe además de archivos .ssdr pre-extraídos. Si tiene un archivo .ssdr descargado previamente, aún funciona — selecciónelo de la misma manera.

## Relacionado

- [Verifique el número de serie de la radio, versión de hardware, región y opciones](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
