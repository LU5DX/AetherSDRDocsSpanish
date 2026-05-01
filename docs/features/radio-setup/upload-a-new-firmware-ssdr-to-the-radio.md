# Cargue un nuevo archivo de firmware en la radio

Esta página explica cómo cargar una imagen de firmware en su FLEX-8600 mediante el diálogo Radio Setup. Haría esto para actualizar la radio a una versión de firmware específica sin usar la verificación automática de actualizaciones.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La pestaña Radio no se poblará correctamente sin una conexión activa.
- Descargue el instalador de SmartSDR desde flexradio.com y anote dónde se guarda en su computadora. AetherSDR acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador antiguo autoextraíble) o un archivo de firmware `.ssdr` preextraído.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Select Installer...** para abrir un selector de archivos.
4. Navegue al instalador o archivo de firmware en su computadora, selecciónelo y confirme. AetherSDR detecta automáticamente el formato desde el encabezado del archivo y extrae el `.ssdr` si es necesario. Aparece un mensaje de estado mientras se prepara el firmware.
5. Cuando el estado indique que el firmware está listo, haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga está completa antes de hacer cualquier otra cosa.
7. Reinicie la radio como se indica en las notas de la versión del firmware para aplicar el nuevo firmware.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón | Consulta actualizaciones de firmware disponibles. Si se encuentra una actualización, el área de estado muestra la versión disponible e instruye descargar el instalador de SmartSDR desde flexradio.com, luego usar **Select Installer...** para prepararlo. |
| **Select Installer...** | Botón | Abre un diálogo de archivo que acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador autoextraíble antiguo) o un archivo `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Se muestra un mensaje de estado mientras se prepara el archivo. Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Botón | Inicia la carga usando el archivo preparado por **Select Installer...**. Debajo aparecen una barra de progreso y texto de estado que se actualizan a medida que avanza la transferencia. |
| TX Follows Active Slice | Botón | TX sigue la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=latencia más baja a 3=más nitidez) por modo; el control deslizante se desactiva cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Alternador | Habilita la selección automática del nivel de filtro para ese modo; desactiva el control deslizante manual de nitidez. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` rota en firmware 4.2. El TGXL controla PTT de la radio mediante su cable de bloqueo de hardware; no se necesita modulación del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, se rellena previamente la IP descubierta. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado Connected solo cuando el dispositivo conectado es un Antenna Genius genuino (no un ShackSwitch). |
| Connect / Disconnect (ShackSwitch) | Botón | Abre/cierra conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de transmisión AG. El descubrimiento automático por UDP también funciona sin esta fila. Fila oculta del estado Connected si Antenna Genius (no-ShackSwitch) es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa `webPort` de la baliza si es mayor que 1024, de lo contrario retrocede a `SS_WebPort` o puerto 5000. |
| APD (pestaña) | Pestaña | Configuración del muestreador Adaptive Pre-Distortion externo — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios serie 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| Combos muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando conduzca un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Retrocede a INTERNAL si la radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de color de slice entre la paleta AetherSDR integrada y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter e insignias de canal CAT. Los botones están deshabilitados cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores de slice personalizados a la paleta AetherSDR integrada. |

## Calibración de frecuencia (pestaña RX)

La pestaña RX muestra controles de calibración independientemente de si GPSDO está instalado. La etiqueta de estado en la parte superior de la pestaña cambia de redacción y color según el hardware presente:

- **GPSDO installed** — la etiqueta dice "GPSDO installed. Manual frequency offset calibration available." en verde. Aún puede ejecutar una calibración manual si es necesario.
- **No GPSDO** — la etiqueta dice "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** siempre están visibles y activos. Antes de v0.9.2.1, los controles de calibración se ocultaban cuando se detectaba un GPSDO.

### Usando el botón Start

El botón **Start** ahora proporciona retroalimentación de estado en línea directamente en la pestaña RX en lugar de depender únicamente de la respuesta de la radio. Cuando hace clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz)** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no continúa.
2. El texto del botón cambia a **Busy** y el botón se desactiva hasta que se complete la secuencia del comando de calibración.
3. AetherSDR envía `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0` para reiniciar cualquier desplazamiento anterior, luego emite `radio pll_start` para comenzar el barrido de calibración.
4. La etiqueta de estado en línea junto al botón se actualiza a medida que avanza la calibración.
5. Cuando la secuencia termina (o falla), el botón se habilita nuevamente y vuelve a **Start**.

La actividad de calibración se registra en el registro de protocolo a nivel de depuración, incluido el valor de frecuencia de calibración, el reinicio ppb y un identificador de ejecución interno que ayuda a correlacionar entradas de registro cuando se realizan múltiples intentos de calibración en la misma sesión.

### Controles de frecuencia de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Campo | Ingrese la frecuencia de referencia conocida en MHz (seis decimales). Se envía como `radio set cal_freq=<value>` cuando deja el campo o hace clic en **Start**. |
| **Start** | Botón | Reinicia el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Deshabilitado y etiquetado como **Busy** mientras se ejecuta un barrido. |
| **Freq Offset (ppb)** | Spinbox | Desplazamiento manual de frecuencia en partes por mil millones. Ajuste después de la calibración si se necesita ajuste fino. |

## Consejos

- Si solo desea verificar si existe una versión más nueva en lugar de cargar un archivo específico, use **Check for Update** primero. El área de estado le dirá la versión disponible y lo dirigirá a descargar el instalador desde flexradio.com.
- **Select Installer...** acepta archivos `.msi`, `.exe` y `.ssdr`. No necesita extraer un `.ssdr` de un instalador manualmente — AetherSDR lo maneja automáticamente.
- El área de estado del firmware está vacía hasta que se prepara un archivo o comienza una carga. Si no ve una barra de progreso después de hacer clic en **Upload Firmware**, confirme que un archivo se preparó exitosamente con **Select Installer...** primero.
- Si **Start** muestra "Enter cal frequency" en ámbar, escriba un valor de frecuencia en el campo **Cal Frequency (MHz)** antes de hacer clic en **Start** nuevamente.
- Incluso con GPSDO instalado, puede ejecutar un paso de calibración manual si necesita verificar o anular la corrección automática.
- Para abrir la interfaz web de ShackSwitch, haga clic en **⚙ Web UI** en la fila de ShackSwitch de la pestaña Peripherals. Si el dispositivo aún no se ha conectado, ingrese primero su dirección IP en el campo `SS_ManualIp`.

## Solución de problemas

- **Upload Firmware no hace nada** — No se ha preparado ningún archivo de firmware. Haga clic en **Select Installer...**, seleccione el archivo `.msi`, `.exe` o `.ssdr`, espere el mensaje de estado que confirme que el archivo está listo, luego haga clic en **Upload Firmware**.
- **Los controles de la pestaña Radio están sin rellenar o atenuados** — AetherSDR no está conectado a la radio. Establezca una conexión mediante `Settings > Connect to Radio...` antes de abrir Radio Setup.
- **El botón Start permanece etiquetado como Busy** — La radio no respondió al comando `radio pll_start`. Consulte el registro de protocolo para el identificador de ejecución relevante, verifique que la radio está conectada y no transmitiendo, luego intente nuevamente.
- **La pestaña APD no es visible** — La radio conectada no reporta `apd configurable=1`. La pestaña APD solo está disponible en radios de la serie FLEX-8x00 ejecutando firmware SmartSDR 4.2.18 o posterior.
- **⚙ Web UI abre la dirección incorrecta o no hace nada** — Verifique que `SS_ManualIp` contenga la IP correcta para ShackSwitch. Si la baliza anuncia un `webPort` de 1024 o inferior, AetherSDR retrocede a `SS_WebPort` o puerto 5000. Establezca `SS_WebPort` en configuración si su dispositivo usa un puerto web no predeterminado.
- **La fila Antenna Genius no muestra Connected** —
