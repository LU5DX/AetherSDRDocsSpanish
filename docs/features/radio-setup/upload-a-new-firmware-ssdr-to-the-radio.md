# Cargar un Nuevo Archivo de Firmware en la Radio

Esta página explica cómo cargar una imagen de firmware en su FLEX-8600 usando el diálogo Radio Setup. Realice este procedimiento para actualizar la radio a una versión de firmware específica sin usar la verificación de actualizaciones automática.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Radio (tab) no se llenará correctamente sin una conexión activa.
- Descargue el instalador de SmartSDR desde flexradio.com y anote dónde se guarda en su computadora. AetherSDR acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` previamente extraído.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Select Installer...** para abrir un selector de archivos.
4. Navegue hasta el instalador o archivo de firmware en su computadora, selecciónelo y confirme. AetherSDR detecta automáticamente el formato a partir del encabezado del archivo y extrae el `.ssdr` si es necesario. Aparece un mensaje de estado mientras se prepara el firmware.
5. Cuando el estado indique que el firmware está listo, haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga se ha completado antes de realizar cualquier otra acción.
7. Reinicie la radio según las instrucciones de las notas de la versión del firmware para aplicar el nuevo firmware.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Si se encuentra una actualización, el área de estado muestra la versión disponible e indica que descargue el instalador de SmartSDR desde flexradio.com y luego use **Select Installer...** para prepararlo. |
| **Select Installer...** | Botón | Abre un diálogo de archivo que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo `.ssdr` previamente extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Se muestra un mensaje de estado mientras se prepara el archivo. Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Botón | Inicia la carga usando el archivo preparado por **Select Installer...**. Aparecen una barra de progreso y un texto de estado debajo que se actualizan conforme avanza la transferencia. |
| TX Follows Active Slice | Botón | El TX sigue al slice (canal de recepción) activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Deslizador | Establece la nitidez del filtro (0=latencia mínima a 3=máxima nitidez) por modo; el deslizador se deshabilita cuando Auto está activado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Conmutador | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que no funciona en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y la radio ya ha descubierto el TGXL, se rellena previamente con la IP descubierta. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected solo cuando el dispositivo conectado es un Antenna Genius genuino (no un ShackSwitch). |
| Connect / Disconnect (ShackSwitch) | Botón | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión AG. El autodescubrimiento mediante UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (que no sea ShackSwitch). |
| ⚙ Web UI (ShackSwitch) | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| APD (tab) | Pestaña | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las radios de la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Lista desplegable | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente en el entrenamiento APD para esa antena TX. Elija una entrada externa de RX/XVTR cuando use un amplificador lineal externo. Las opciones se obtienen en tiempo real del subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| Themes (tab) | Pestaña | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets de VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones están deshabilitados cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores personalizados de slice a la paleta integrada de AetherSDR. |

## Calibración de frecuencia (pestaña RX)

La pestaña RX muestra los controles de calibración independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior de la pestaña cambia de texto y color según el hardware presente:

- **GPSDO instalado** — la etiqueta indica "GPSDO installed. Manual frequency offset calibration available." en verde. Aun así, puede ejecutar una calibración manual si es necesario.
- **Sin GPSDO** — la etiqueta indica "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** siempre están visibles y activos. Antes de v0.9.2.1, los controles de calibración estaban ocultos cuando se detectaba un GPSDO.

### Uso del botón Start

El botón **Start** ahora proporciona retroalimentación de estado en línea directamente en la pestaña RX, sin depender únicamente de la respuesta de la radio. Cuando hace clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz)** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no continúa.
2. El texto del botón cambia a **Busy** y el botón se deshabilita hasta que la secuencia de comandos de calibración se complete.
3. AetherSDR envía `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0` para restablecer cualquier desplazamiento previo, y luego emite `radio pll_start` para iniciar el barrido de calibración.
4. La etiqueta de estado en línea junto al botón se actualiza conforme avanza la calibración.
5. Cuando la secuencia termina (o falla), el botón se vuelve a habilitar y regresa a **Start**.

La actividad de calibración se registra en el log de protocolo a nivel de depuración, incluyendo el valor de frecuencia de calibración, el reinicio de ppb y un identificador de ejecución interno que ayuda a correlacionar las entradas del log cuando se realizan múltiples intentos de calibración en la misma sesión.

### Controles de frecuencia de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Campo | Ingrese la frecuencia de referencia conocida en MHz (seis decimales). Se envía como `radio set cal_freq=<value>` al salir del campo o al hacer clic en **Start**. |
| **Start** | Botón | Restablece el error de frecuencia a 0 ppb y luego inicia el barrido de calibración. Se deshabilita y se etiqueta como **Busy** mientras se ejecuta un barrido. |
| **Freq Offset (ppb)** | Caja de ajuste | Desplazamiento de frecuencia manual en partes por mil millones. Ajuste después de la calibración si se necesita un ajuste fino. |

## Consejos

- Si solo desea verificar si existe una versión más reciente en lugar de cargar un archivo específico, use primero **Check for Update**. El área de estado le indicará la versión disponible y lo dirigirá a descargar el instalador desde flexradio.com.
- **Select Installer...** acepta archivos `.msi`, `.exe` y `.ssdr`. No es necesario extraer manualmente un `.ssdr` de un instalador — AetherSDR lo hace automáticamente.
- El área de estado del firmware está vacía hasta que se prepara un archivo o comienza una carga. Si no aparece ninguna barra de progreso después de hacer clic en **Upload Firmware**, confirme primero que un archivo fue preparado correctamente con **Select Installer...**.
- Si **Start** muestra "Enter cal frequency" en ámbar, escriba un valor de frecuencia en el campo **Cal Frequency (MHz)** antes de hacer clic en **Start** nuevamente.
- Incluso con un GPSDO instalado, puede ejecutar una calibración manual si necesita verificar o anular la corrección automática.
- Para abrir la interfaz web del ShackSwitch, haga clic en **⚙ Web UI** en la fila ShackSwitch de la pestaña Peripherals. Si el dispositivo aún no ha sido conectado, ingrese primero su dirección IP en el campo `SS_ManualIp`.

## Solución de problemas

- **Upload Firmware no hace nada** — No se ha preparado ningún archivo de firmware. Haga clic en **Select Installer...**, seleccione el archivo `.msi`, `.exe` o `.ssdr`, espere a que el mensaje de estado confirme que el archivo está listo y luego haga clic en **Upload Firmware**.
- **Los controles de la pestaña Radio no están poblados o están atenuados** — AetherSDR no está conectado a la radio. Establezca una conexión mediante `Settings > Connect to Radio...` antes de abrir Radio Setup.
- **El botón Start permanece etiquetado como Busy** — La radio no respondió al comando `radio pll_start`. Verifique en el log de protocolo el identificador de ejecución correspondiente, compruebe que la radio esté conectada y no esté transmitiendo, y vuelva a intentarlo.
- **La pestaña APD no está visible** — La radio conectada no informa `apd configurable=1`. La pestaña APD solo está disponible en radios de la serie FLEX-8x00 con firmware SmartSDR 4.2.18 o posterior.
- **⚙ Web UI abre una dirección incorrecta o no hace nada** — Verifique que `SS_ManualIp` contenga la IP correcta para el ShackSwitch. Si la baliza anuncia un `webPort` de 1024 o inferior, AetherSDR recurre a `SS_WebPort` o al puerto 5000. Configure `SS_WebPort` en los ajustes si su dispositivo usa un puerto web no predeterminado.
- **La fila de Antenna Genius no muestra Connected**
