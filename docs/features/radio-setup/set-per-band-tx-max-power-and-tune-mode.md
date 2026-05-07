# Establecer la potencia máxima de TX por banda y el modo de sintonía

Use esta página para limitar la potencia de transmisión por banda y elegir cómo se comporta la función de sintonía (Tune). Estos ajustes se almacenan en la radio y se aplican independientemente de qué cliente esté conectado.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña TX no es accesible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia por banda y sintonía.
4. En la tabla por banda, localice la banda que desea configurar.
5. Ajuste el límite de potencia para esa banda según sea necesario. El rango válido para **Max Power:** es 0–100 %.
6. Para cambiar el comportamiento de sintonía, seleccione la opción deseada en el cuadro combinado **Tune Mode:**.
7. Cierre el diálogo cuando haya terminado. Los ajustes se aplican inmediatamente a la radio.

## Qué hace cada control

| Control | Tipo | Rango válido / opciones |
|---|---|---|
| **TX Band Settings** | Botón | — |
| **Max Power:** | Cuadro de giro | 0–100 % |
| **Tune Mode:** | Cuadro combinado | Consulte las opciones del firmware de la radio |
| **Show TX in Waterfall:** | Botón de alternancia | Habilitado / Deshabilitado |
| **TX Follows Active Slice** | Botón | TX sigue la slice activa. Es mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. |
| **Active Slice Follows TX** | Botón | Cambia la slice activa cuando TX se mueve externamente (p.ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. |
| Deslizadores de nitidez de filtro Voz / CW / Digital | Deslizador | 0–3. Establece la nitidez del filtro (0 = latencia más baja, 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| Auto (Voz / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en el firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado de Conectado solo cuando el dispositivo conectado es un Antenna Genius (no ShackSwitch). Si un ShackSwitch es el dispositivo conectado, esta fila se oculta del estado Conectado. |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de difusión de AG. El descubrimiento automático a través de UDP también funciona sin ingresar una IP manualmente. La fila muestra el estado Conectado solo cuando el dispositivo conectado es un ShackSwitch. |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD** (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena de TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena de TX. Elija una entrada RX/XVTR externa cuando esté manejando un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. Predeterminado: INTERNAL. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes** (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente alberga la sección de Colores de Slice. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de color de las slices entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en los widgets de VFO, superposiciones del panadapter e insignias de canal CAT. Los botones se deshabilitan cuando está seleccionado **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores personalizados de las slices a la paleta incorporada de AetherSDR. |

## Conexión de dispositivos periféricos (pestaña Peripherals)

La pestaña **Peripherals** proporciona conexión IP manual para dispositivos externos, incluidos TGXL, PGXL, Antenna Genius y ShackSwitch. Cada dispositivo tiene su propia fila con botones **Connect** / **Disconnect** y un indicador de estado.

### ShackSwitch

La fila de ShackSwitch se comporta de la siguiente manera:

- Ingrese la dirección IP del ShackSwitch y haga clic en **Connect**. AetherSDR guarda la dirección en `SS_ManualIp` y el puerto en `SS_ControlPort` y se conecta utilizando el protocolo AG UDP/TCP en el puerto 9007.
- Si la radio ya ha descubierto el ShackSwitch a través de la baliza UDP, el campo IP puede estar previamente rellenado.
- La fila muestra un estado de Conectado solo cuando el dispositivo conectado se identifica como un ShackSwitch. Si se conecta un Antenna Genius estándar en su lugar, la fila de ShackSwitch no muestra Conectado, pero la fila de Antenna Genius sí.
- Haga clic en **⚙ Web UI** para abrir la interfaz web local del ShackSwitch en su navegador del sistema. AetherSDR determina el puerto de la siguiente manera:
  1. Utiliza el `webPort` anunciado en la baliza si es mayor que 1024.
  2. Recurre al valor almacenado en `SS_WebPort`.
  3. Recurre al puerto 5000.

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** contiene controles para verificar actualizaciones de firmware y cargar firmware en la radio.

### Cómo actualizar el firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
4. Descargue el instalador de SmartSDR desde flexradio.com si hay uno disponible.
5. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo `.ssdr` preextraído.
   - El preparador de firmware detecta el formato del archivo automáticamente y extrae el `.ssdr` sin requerir herramientas externas.
   - Mientras el preparador prepara el firmware, se muestra la barra de progreso y la etiqueta de estado indica "Preparing firmware from <nombre_de_archivo>...".
6. Una vez que la preparación se completa, haga clic en **Upload Firmware** para transferir el firmware a la radio. El progreso y el resultado se muestran en la etiqueta de estado.

### Controles de actualización de firmware

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Habilita o actualiza la etiqueta de estado con el resultado. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. El preparador detecta el formato automáticamente. Anteriormente etiquetado como **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Botón | Inicia la carga del firmware. La barra de progreso y la etiqueta de estado se actualizan durante el proceso. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** contiene controles para la calibración manual de desplazamiento de frecuencia y la selección de la fuente de referencia de 10 MHz. En v0.9.2.1 los controles de calibración siempre se muestran independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado indica "GPSDO installed. Manual frequency offset calibration available." (verde). Cuando no hay un GPSDO presente, la etiqueta indica "Manual frequency offset calibration available." (ámbar).

### Cómo realizar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra texto de progreso ("Starting…" y luego el estado en vivo).
   - Antes de comenzar, AetherSDR restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no continúa.
5. Cuando la calibración se completa, el botón se vuelve a habilitar y el campo de estado muestra el resultado.
6. Si necesita establecer un desplazamiento manualmente, ingrese un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control | Tipo | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de giro | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en **Start**. |
| **Start** | Botón | Comienza la calibración. Restablece `freq_error_ppb` a 0, luego emite `radio pll_start`. Se deshabilita mientras está ocupado. |
| **Freq Offset (ppb):** | Cuadro de giro | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la referencia del oscilador. Las opciones disponibles dependen del hardware instalado. El cuadro combinado se rellena dinámicamente: Auto está siempre presente; TCXO y External 10 MHz aparecen cuando la radio informa que esas fuentes están presentes o estuvieron activas anteriormente; GPSDO aparece cuando se detecta un GPSDO. La etiqueta "External" de versiones de firmware anteriores se normaliza a "External 10 MHz". El indicador de estado de bloqueo junto al cuadro combinado se actualiza en vivo. Cuando la fuente seleccionada es Auto, el texto de estado muestra la fuente resuelta (p.ej., "Auto -> GPSDO"). Cuando la fuente configurada difiere de la fuente activa. |
