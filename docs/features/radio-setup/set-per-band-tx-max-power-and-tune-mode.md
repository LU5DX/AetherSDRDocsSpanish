# Establecer potencia TX máxima por banda y modo de sintonización

Use esta página para limitar la potencia de transmisión por banda y elegir cómo se comporta la función Tune. Estos ajustes se almacenan en la radio y se aplican independientemente del cliente que se conecte.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña TX no es accesible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y sintonización por banda.
4. En la tabla por banda, localice la banda que desea configurar.
5. Ajuste el límite de potencia para esa banda según sea necesario. El rango válido para **Max Power:** es 0–100 %.
6. Para cambiar el comportamiento de sintonización, seleccione la opción deseada en el cuadro desplegable **Tune Mode:**.
7. Cierre el diálogo cuando termine. Los ajustes se aplican inmediatamente a la radio.

## Qué hace cada control

| Control | Tipo | Rango válido / opciones |
|---|---|---|
| **TX Band Settings** | Botón | — |
| **Max Power:** | Cuadro de rotación | 0–100 % |
| **Tune Mode:** | Cuadro desplegable | Consulte las opciones de firmware de la radio |
| **Show TX in Waterfall:** | Botón de alternancia | Habilitado / Deshabilitado |
| **TX Follows Active Slice** | Botón | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación de división. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de agudeza de filtro Voice / CW / Digital | Control deslizante | 0–3. Establece la agudeza del filtro (0 = latencia más baja, 3 = más agudo) por modo. El control deslizante se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el control deslizante de agudeza manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, por lo que AetherSDR se reconecta automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que se rompió en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de extracción automática antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **APD** (pestaña) | Pestaña | Configuración del muestreador de predistorsión adaptativa externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de restablecimiento del ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo las radios FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro desplegable | Selecciona la ruta de retroalimentación que usa la radio para muestrear el RF saliente para entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. Predeterminado: INTERNAL. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience nuevamente. |
| **Themes** (pestaña) | Pestaña | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets de VFO, superposiciones de panadapter y distintivos de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores personalizados del slice a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** contiene controles para verificar actualizaciones de firmware y cargar firmware en la radio.

### Cómo actualizar el firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si una actualización está disponible, la etiqueta de estado muestra la versión disponible e instruye descargar el instalador SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
4. Descargue el instalador SmartSDR desde flexradio.com si hay uno disponible.
5. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de extracción automática antiguo) o un archivo `.ssdr` preextraído.
   - El preparador de firmware detecta automáticamente el formato de archivo y extrae el `.ssdr` sin requerir herramientas externas.
   - Mientras el preparador prepara el firmware, se muestra la barra de progreso y la etiqueta de estado lee "Preparing firmware from \<filename\>...".
6. Una vez completada la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio. El progreso y resultado se muestran en la etiqueta de estado.

### Controles de actualización de firmware

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta actualizaciones de firmware disponibles. Habilita o actualiza la etiqueta de estado con el resultado. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. El preparador detecta automáticamente el formato. Etiquetado previamente como **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Botón | Inicia la carga de firmware. Barra de progreso y etiqueta de estado se actualizan durante todo el proceso. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** contiene controles para calibración manual de compensación de frecuencia y selección de fuente de referencia de 10 MHz. En v0.9.2.1 los controles de calibración siempre se muestran independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." (verde). Cuando no hay GPSDO presente, la etiqueta lee "Manual frequency offset calibration available." (ámbar).

### Cómo ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra texto de progreso ("Starting…" luego estado en vivo).
   - Antes de iniciar, AetherSDR restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no procede.
5. Cuando la calibración se complete, el botón se vuelve a habilitar y el campo de estado muestra el resultado.
6. Si necesita establecer una compensación manualmente, ingrese un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control | Tipo | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de rotación | Frecuencia utilizada para calibración. No debe estar vacío antes de hacer clic en **Start**. |
| **Start** | Botón | Comienza la calibración. Restablece `freq_error_ppb` a 0, luego emite `radio pll_start`. Deshabilitado mientras esté ocupado. |
| **Freq Offset (ppb):** | Cuadro de rotación | Compensación de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Cuadro desplegable | Auto / TCXO / GPSDO / External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo se actualiza en vivo. |

## Consejos

- **TX Band Settings** también es accesible directamente desde `Settings > TX Band Settings...` sin abrir Radio Setup primero.
- El cuadro de rotación **Max Power:** en la pestaña TX establece un límite a nivel de radio. Los límites por banda establecidos dentro de **TX Band Settings** operan encima de este límite.
- Cuando ejecute calibración de frecuencia, asegúrese de que ninguna otra estación esté transmitiendo en la frecuencia de referencia antes de hacer clic en **Start**.
- Cuando **Check for Update** reporta una versión de firmware disponible, AetherSDR ya no descarga el instalador automáticamente. Descargue el instalador SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo.

## Relacionado

- [Radio Setup overview](overview.md)
- [Upload a new firmware .ssdr to the radio](upload-a-new-firmware-ssdr-to-the-radio.md)
