# Asignar un cable USB como CAT, BCD, bit o PTT

Utilice esta página para configurar los adaptadores seriales USB conectados a su FLEX-8600 y asignar a cada uno un rol — control CAT, datos de banda BCD, salida de bit individual, o PTT — junto con sus parámetros seriales y opciones de comportamiento.

## Antes de comenzar

- Conecte los adaptadores seriales USB a la computadora que ejecuta AetherSDR antes de abrir el diálogo.
- AetherSDR debe estar conectado a la radio. La pestaña USB Cables no está disponible sin una conexión activa a la radio.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña USB Cables. También puede abrir `Settings > Radio Setup...` y hacer clic en la pestaña **USB Cables**.
2. Localice la lista de cables en el lado izquierdo de la pestaña. Cada cable USB detectado aparece con su nombre y un indicador de estado **Plugged** o **Unplugged**.
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Establezca el tipo de cable usando el campo **Name:** y el selector de tipo asociado. Elija entre CAT, BCD, bit, o PTT según el rol que este cable deba servir.
5. Establezca **Enabled** para habilitar el cable. El cable no funcionará hasta que esté habilitado.
6. Configure los parámetros seriales para el cable:
   - **Speed** — velocidad en baudios para la conexión serial.
   - **Data Bits** — número de bits de datos.
   - **Parity** — configuración de paridad.
   - **Stop Bits** — número de bits de parada.
   - **Flow** — método de control de flujo.
7. Configure las opciones de comportamiento relevantes para el tipo de cable:
   - **Source** — selecciona qué impulsa la salida del cable.
   - **Auto Report** — controla si los cambios de estado se reportan automáticamente.
   - **BCD Type** — selecciona el formato de codificación BCD (solo cables BCD).
   - **Polarity** — establece lógica activa-alta o activa-baja.
   - **Bit Configuration (0–7)** — asigna funciones a bits de salida individuales (solo cables bit).
8. Repita los pasos 3–7 para cualquier cable adicional.
9. Haga clic en **Close** para cerrar el diálogo. La configuración entra en vigor inmediatamente cuando cada cable está habilitado; no se requiere un paso Apply separado.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| **Cables list / Status** | Lista todos los adaptadores seriales USB detectados con estado **Plugged** o **Unplugged**. Seleccione un cable aquí para editar su configuración. | |
| **Name:** | Etiqueta visible para el usuario del cable. | |
| **Enabled** | Activa el cable. El cable está inactivo hasta que se habilita. | |
| **Speed** | Velocidad en baudios serial. | |
| **Data Bits** | Número de bits de datos serial. | |
| **Parity** | Paridad serial: None, Even, Odd, etc. | |
| **Stop Bits** | Número de bits de parada. | |
| **Flow** | Método de control de flujo (None, Hardware, Software). | |
| **Source** | Selecciona la fuente de señal de radio que impulsa la salida del cable. | |
| **Auto Report** | Cuando está activo, la radio reporta cambios de estado al cable automáticamente. | |
| **BCD Type** | Selecciona el formato de codificación de datos de banda BCD. Se aplica solo a cables de tipo BCD. | |
| **Polarity** | Establece si la lógica de salida es activa-alta o activa-baja. | |
| **Bit Configuration (0–7)** | Mapea pines de salida individuales a funciones específicas. Se aplica solo a cables de tipo bit. | |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. | Se deshabilita automáticamente durante operación Split. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | |
| **Voice / CW / Digital filter sharpness sliders** | Establece la agudeza del filtro (0=latencia más baja a 3=más agudo) por modo; el control deslizante se deshabilita cuando Auto está habilitado. | Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el control deslizante de agudeza manual. | Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. | Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio rota en firmware 4.2. El TGXL controla PTT de radio a través de su cable de interlock de hardware; no se requiere control de teclas del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa previamente. |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión con Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. | |
| **Select Installer...** | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo), o archivo de firmware `.ssdr` preextraído. El firmware stager detecta automáticamente el formato de los primeros 8 bytes (magic OLE/MSI vs MZ PE/COFF) y extrae `.ssdr` sin herramientas externas. | La etiqueta cambió de **Browse .ssdr...** en v0.9.3. Cuando hay una actualización disponible, descargue el instalador SmartSDR de flexradio.com, luego haga clic en **Select Installer...** para colocarlo en stage. |
| **APD (tab)** | Configuración de muestreador de Pre-Distorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. | La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo FLEX-8x00 series con firmware SmartSDR 4.2.18+ expone esto; radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que la radio usa para muestrear RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando impulse un amplificador lineal externo. | Las opciones se completan en directo desde el subobjeto `apd sampler` de la radio. Retrocede a INTERNAL si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. | |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color de slice entre la paleta AetherSDR incorporada y un conjunto completo por slice personalizado. | Respaldado por `SliceColorManager::useCustomColors()`. |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y badges de canal CAT. | Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Reinicia todos los colores de slice personalizados a la paleta AetherSDR incorporada. | |

## Pestaña RX — calibración de frecuencia (v0.9.2.1)

La pestaña **RX** ahora muestra los controles de calibración de frecuencia independientemente de si un GPSDO está instalado. En versiones anteriores, los campos de calibración estaban ocultos cuando se detectaba un GPSDO.

- Si un GPSDO está instalado, una línea de estado verde dice "GPSDO installed. Manual frequency offset calibration available."
- Si no hay GPSDO instalado, una línea de estado amarilla dice "Manual frequency offset calibration available."

En ambos casos los controles **Cal Frequency (MHz):**, **Start**, y **Freq Offset (ppb):** siempre están visibles.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras la calibración se ejecuta. Una etiqueta de estado a la derecha del botón muestra texto de progreso.
   - "Starting…" aparece inmediatamente.
   - La radio recibe `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0`, luego `radio pll_start` para comenzar el barrido.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no comienza.
4. Espere a que la etiqueta de estado indique finalización. El botón **Start** se rehabilita automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

### Controles de la pestaña RX

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia usada para calibración, ingresada en MHz con seis decimales. | Enviada a la radio como `radio set cal_freq=<value>`. |
| **Start** | Comienza el barrido de calibración. Se deshabilita y se etiqueta como **Busy** mientras una calibración está en progreso. | Reinicia `freq_error_ppb` a 0 antes de comenzar. Requiere frecuencia cal no vacía. |
| **Freq Offset (ppb):** | Corrección manual de desplazamiento de frecuencia en partes por billón. | |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO, o External. Las opciones disponibles dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al selector y se actualiza en directo. |

## Actualización de firmware (v0.9.3)

En v0.9.3, el flujo de trabajo de actualización de firmware cambió. AetherSDR ya no descarga el instalador automáticamente. Cuando **Check for Update** reporta que hay una versión más nueva disponible, descargue el instalador SmartSDR de flexradio.com usted mismo, luego use **Select Installer...** para colocarlo en stage localmente.

### Formatos de instalador soportados

| Formato | Extensión | Notas |
|---|---|---|
| Instalador WiX MSI | `.msi` | FlexRadio v4.2 y posterior. |
| Instalador EXE autoextraíble | `.exe` | Versiones antiguas de SmartSDR. |
| Archivo de firmware preextraído | `.ssdr` | Archivo de firmware directo, si ya lo tiene. |

El firmware stager detecta automáticamente el formato de los primeros 8 bytes del archivo (magic OLE/MSI vs encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` sin requerir herramientas externas.

### Procedimiento de actualización de firmware

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Radio**.
2. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualización e informa el resultado en la etiqueta de estado.
   - Si el firmware es actual, la etiqueta muestra "Firmware is up to date."
   - Si hay una actualización disponible, la etiqueta le instruye descargar el instalador SmartSDR de flexradio.com.
3. Descargue el instalador SmartSDR de flexradio.com.
4. Haga clic en **Select Installer...**. En el selector de archivos, seleccione el archivo `.msi`, `.exe`, o `.ssdr` que descargó. El stager comienza a extraer y colocar en stage el firmware inmediatamente; el progreso se muestra en la barra de progreso y etiqueta de estado.
5.
