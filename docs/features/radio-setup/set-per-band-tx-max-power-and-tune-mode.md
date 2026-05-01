# Establecer potencia TX máxima por banda y modo de ajuste

Use esta página para limitar la potencia de transmisión por banda y elegir cómo se comporta la función Tune. Estas configuraciones se almacenan en la radio y se aplican independientemente de qué cliente se conecte.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña TX no es accesible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y ajuste por banda.
4. En la tabla por banda, localice la banda que desea configurar.
5. Ajuste el límite de potencia para esa banda según sea necesario. El rango válido para **Max Power:** es 0–100 %.
6. Para cambiar el comportamiento del ajuste, seleccione la opción deseada del cuadro combinado **Tune Mode:**.
7. Cierre el diálogo cuando haya terminado. Los cambios se aplican inmediatamente a la radio.

## Qué hace cada control

| Control | Tipo | Rango válido / Opciones |
|---|---|---|
| **TX Band Settings** | Botón | — |
| **Max Power:** | Cuadro de número | 0–100 % |
| **Tune Mode:** | Cuadro combinado | Véase las opciones de firmware de la radio |
| **Show TX in Waterfall:** | Botón de alternancia | Habilitado / Deshabilitado |
| **TX Follows Active Slice** | Botón | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Regulador | 0–3. Establece la nitidez del filtro (0 = latencia más baja, 3 = más nítido) por modo. El regulador se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el regulador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Se requiere para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa previamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra la conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado Connected solo cuando el dispositivo conectado es Antenna Genius (que no sea ShackSwitch). Si un ShackSwitch es el dispositivo conectado, esta fila se oculta del estado Connected. |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de difusión AG. El autodescubrimiento mediante UDP también funciona sin ingresar manualmente una IP. La fila muestra estado Connected solo cuando el dispositivo conectado es un ShackSwitch. |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o puerto 5000. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de extracción automática antiguo) o un archivo de firmware `.ssdr` pre-extraído. El gestor de firmware detecta automáticamente el formato desde los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **APD** (pestaña) | Pestaña | Configuración de muestreador de pre-distorsión adaptativa externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear el RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se completan en tiempo real desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. Predeterminado: INTERNAL. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes** (pestaña) | Pestaña | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y insignias de canal CAT. Los botones están deshabilitados cuando está seleccionado **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Conexión de dispositivos periféricos (pestaña Peripherals)

La pestaña **Peripherals** proporciona conexión IP manual para dispositivos externos incluyendo TGXL, PGXL, Antenna Genius y ShackSwitch. Cada dispositivo tiene su propia fila con botones **Connect** / **Disconnect** e indicador de estado.

### ShackSwitch

La fila ShackSwitch se comporta como sigue:

- Ingrese la dirección IP de ShackSwitch y haga clic en **Connect**. AetherSDR guarda la dirección en `SS_ManualIp` y el puerto en `SS_ControlPort` y se conecta utilizando el protocolo AG UDP/TCP en el puerto 9007.
- Si la radio ya ha descubierto el ShackSwitch mediante beacon UDP, el campo IP puede rellenarse previamente.
- La fila muestra estado Connected solo cuando el dispositivo conectado se identifica como ShackSwitch. Si en su lugar está conectado un Antenna Genius estándar, la fila ShackSwitch no muestra Connected, y lo hace la fila Antenna Genius.
- Haga clic en **⚙ Web UI** para abrir la interfaz web local de ShackSwitch en su navegador del sistema. AetherSDR determina el puerto como sigue:
  1. Utiliza el `webPort` anunciado en el beacon si es mayor que 1024.
  2. Recurre al valor almacenado en `SS_WebPort`.
  3. Recurre al puerto 5000.

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** contiene controles para verificar actualizaciones de firmware y cargar firmware a la radio.

### Cómo actualizar el firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que descargue el instalador SmartSDR desde flexradio.com.
   - Si el firmware ya está actualizado, la etiqueta de estado muestra "Firmware is up to date."
4. Descargue el instalador SmartSDR desde flexradio.com si hay uno disponible.
5. Haga clic en **Select Installer...**.
   - El selector de archivos acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de extracción automática antiguo) o archivo `.ssdr` pre-extraído.
   - El gestor de firmware detecta automáticamente el formato de archivo y extrae el `.ssdr` sin requerir herramientas externas.
   - Mientras el gestor prepara el firmware, se muestra la barra de progreso y la etiqueta de estado muestra "Preparing firmware from \<filename\>...".
6. Una vez completada la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio. El progreso y el resultado se muestran en la etiqueta de estado.

### Controles de actualización de firmware

| Control | Tipo | Notas |
|---|---|---|
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Habilita o actualiza la etiqueta de estado con el resultado. |
| **Select Installer...** | Botón | Abre un selector de archivos. Acepta `.msi`, `.exe` o `.ssdr`. El gestor detecta automáticamente el formato. Previamente etiquetado como **Browse .ssdr...** (cambiado en v0.9.3). |
| **Upload Firmware** | Botón | Inicia la carga de firmware. La barra de progreso y la etiqueta de estado se actualizan a lo largo del proceso. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** contiene controles para calibración manual de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz. En v0.9.2.1 los controles de calibración siempre se muestran independientemente de si hay un GPSDO instalado. Cuando un GPSDO está presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Cuando no hay GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Cómo ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra texto de progreso ("Starting…" luego estado en vivo).
   - Antes de comenzar, AetherSDR reinicia el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no continúa.
5. Cuando se completa la calibración, el botón se vuelve a habilitar y el campo de estado muestra el resultado.
6. Si necesita establecer un desplazamiento manualmente, ingrese un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control | Tipo | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Cuadro de número | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en **Start**. |
| **Start** | Botón | Inicia la calibración. Reinicia `freq_error_ppb` a 0, luego emite `radio pll_start`. Se deshabilita mientras está ocupado. |
| **Freq Offset (ppb):** | Cuadro de número | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Cuadro combinado | Auto / TCXO / GPSDO / External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo se actualiza en vivo. |

## Consejos

- **TX Band Settings** también es accesible directamente desde `Settings > TX Band Settings...` sin abrir primero Radio Setup.
- El cuadro de número **Max Power:** en la pestaña TX establece un límite a nivel de radio. Los límites por banda establecidos dentro de **TX Band Settings** operan además de este límite.
- Cuando ejecute calibración de frecuencia, asegúrese de que ninguna otra estación esté transmitiendo en la frecuencia de referencia antes de hacer clic en **Start**.
- Cuando **Check for Update** reporta una versión de firmware disponible,
