# Configurar la potencia TX máxima por banda y el modo Tune

Use esta página para limitar la potencia de transmisión por banda y elegir el comportamiento de la función Tune. Estos ajustes se almacenan en el radio y se aplican independientemente del cliente que se conecte.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña TX no es accesible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y sintonía por banda.
4. En la tabla por banda, ubique la banda que desea configurar.
5. Ajuste el límite de potencia para esa banda según sea necesario. El rango válido para **Max Power:** es 0–100 %.
6. Para cambiar el comportamiento de sintonía, seleccione la opción deseada en el cuadro combinado **Tune Mode:**.
7. Cierre el diálogo cuando haya terminado. Los ajustes se aplican de inmediato al radio.

## Qué hace cada control

| Control | Tipo | Rango válido / opciones |
|---|---|---|
| **TX Band Settings** | Botón | — |
| **Max Power:** | Cuadro de número | 0–100 % |
| **Tune Mode:** | Cuadro combinado | Consulte las opciones del firmware del radio |
| **Show TX in Waterfall:** | Botón de alternancia | Habilitado / Deshabilitado |
| **TX Follows Active Slice** | Botón | La TX sigue el slice (canal) activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando la TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro de Voice / CW / Digital | Control deslizante | 0–3. Establece la nitidez del filtro (0 = menor latencia, 3 = máxima nitidez) por modo. El control deslizante se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que presenta problemas en el firmware 4.2. Si el campo IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected únicamente cuando el dispositivo conectado es un Antenna Genius (no ShackSwitch). Si el dispositivo conectado es un ShackSwitch, esta fila no muestra el estado Connected. |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre o cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de difusión AG. El autodescubrimiento por UDP también funciona sin introducir una IP manualmente. La fila muestra el estado Connected únicamente cuando el dispositivo conectado es un ShackSwitch. |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de autoextracción anterior) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI frente a PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en la versión v0.9.3. |
| **APD** (pestaña) | Pestaña | Configuración del muestreador externo de Predistorsión Adaptativa (APD): selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que el radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esta funcionalidad; los radios de la serie 6000 y los anteriores a 4.2.18 mantienen la pestaña invisible. |
| Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que usa el radio para muestrear la RF saliente en el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se obtienen en tiempo real desde el subobjeto `apd sampler` del radio. Si el radio reporta un valor no reconocido, vuelve a INTERNAL. Valor predeterminado: INTERNAL. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| **Themes** (pestaña) | Pestaña | Pestaña de personalización de la interfaz; actualmente incluye la sección de colores de slice. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de colores de los slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores personalizados de slice a la paleta integrada de AetherSDR. |

## Conexión de dispositivos periféricos (pestaña Peripherals)

La pestaña **Peripherals** permite la conexión manual por IP de dispositivos externos, incluyendo el TGXL, el PGXL, el Antenna Genius y el ShackSwitch. Cada dispositivo tiene su propia fila con botones **Connect** / **Disconnect** e indicador de estado.

### ShackSwitch

La fila del ShackSwitch se comporta de la siguiente manera:

- Introduzca la dirección IP del ShackSwitch y haga clic en **Connect**. AetherSDR guarda la dirección en `SS_ManualIp` y el puerto en `SS_ControlPort`, y se conecta mediante el protocolo AG UDP/TCP en el puerto 9007.
- Si el radio ya ha descubierto el ShackSwitch mediante beacon UDP, el campo IP puede estar completado automáticamente.
- La fila muestra el estado Connected únicamente cuando el dispositivo conectado se identifica como un ShackSwitch. Si en su lugar está conectado un Antenna Genius estándar, la fila del ShackSwitch no muestra Connected, y sí lo hace la fila del Antenna Genius.
- Haga clic en **⚙ Web UI** para abrir la interfaz web local del ShackSwitch en el navegador del sistema. AetherSDR determina el puerto de la siguiente manera:
  1. Usa el `webPort` anunciado en el beacon si es mayor que 1024.
  2. Recurre al valor almacenado en `SS_WebPort`.
  3. Recurre al puerto 5000.

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** contiene controles para verificar actualizaciones de firmware y cargar firmware al radio.

### Cómo actualizar el firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que debe descargar el instalador de SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
4. Descargue el instalador de SmartSDR desde flexradio.com si hay uno disponible.
5. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de autoextracción anterior) o un archivo `.ssdr` ya extraído.
   - El preparador de firmware detecta el formato del archivo automáticamente y extrae el `.ssdr` sin requerir herramientas externas.
   - Mientras el preparador procesa el firmware, se muestra la barra de progreso y la etiqueta de estado indica "Preparing firmware from \<filename\>...".
6. Una vez completada la preparación, haga clic en **Upload Firmware** para transferir el firmware al radio. El progreso y el resultado se muestran en la etiqueta de estado.

### Controles de actualización de firmware

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Habilita o actualiza la etiqueta de estado con el resultado. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. El preparador detecta el formato automáticamente. Anteriormente denominado **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Botón | Inicia la carga del firmware. La barra de progreso y la etiqueta de estado se actualizan durante el proceso. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** contiene controles para la calibración manual del desplazamiento de frecuencia y la selección de la fuente de referencia de 10 MHz. En la versión v0.9.2.1, los controles de calibración se muestran siempre, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado indica "GPSDO installed. Manual frequency offset calibration available." (en verde). Cuando no hay GPSDO, la etiqueta indica "Manual frequency offset calibration available." (en ámbar).

### Cómo realizar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra el progreso ("Starting…" y luego el estado en tiempo real).
   - Antes de iniciar, AetherSDR restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no continúa.
5. Cuando la calibración finaliza, el botón se vuelve a habilitar y el campo de estado muestra el resultado.
6. Si necesita establecer un desplazamiento manualmente, introduzca un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control | Tipo | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de número | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en **Start**. |
| **Start** | Botón | Inicia la calibración. Restablece `freq_error_ppb` a 0 y luego emite `radio pll_start`. Deshabilitado mientras está ocupado. |
| **Freq Offset (ppb):** | Cuadro de número | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto / TCXO / GPSDO / External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo se actualiza en tiempo real. |

## Consejos

- **TX Band Settings** también es accesible directamente desde `Settings > TX Band Settings...` sin necesidad de abrir Radio Setup primero.
- El cuadro de número **Max Power:** en la pestaña TX establece un límite a nivel de radio. Los límites por banda configurados dentro de **TX Band Settings** operan sobre este límite.
- Al ejecutar la calibración de frecuencia, asegúrese de que ninguna otra estación esté transmitiendo en la frecuencia de referencia antes de hacer clic en **Start**.
- Cuando **Check for Update** reporta una vers
