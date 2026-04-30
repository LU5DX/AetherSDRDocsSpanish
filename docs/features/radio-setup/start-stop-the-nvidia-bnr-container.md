# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) aplica supresión de ruido basada en IA al audio de su micrófono. Use los controles en la pestaña Audio para iniciar, detener o verificar el estado del contenedor sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no está accesible cuando se desconecta.
- El contenedor NVIDIA Broadcast debe estar instalado en su sistema independientemente de AetherSDR. AetherSDR lo controla pero no lo instala.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que se inicia AetherSDR, haga clic en **Autostart Container** para activarlo.
5. Para iniciar el contenedor inmediatamente, haga clic en **Start**.
6. Para detener un contenedor en ejecución, haga clic en **Stop**.
7. Para consultar el estado actual sin cambiarlo, haga clic en **Check Status**. El indicador de estado de color junto a los controles se actualiza para reflejar Running, Stopped o Unknown.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Cuando está activo, AetherSDR inicia automáticamente el contenedor NVIDIA BNR al iniciar. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR inmediatamente. |
| **Stop** | Botón | Detiene inmediatamente un contenedor NVIDIA BNR en ejecución. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el indicador de estado. |
| Indicador de estado NVIDIA BNR | Indicador | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown. |
| **TX Follows Active Slice** | Botón | TX sigue la porción activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Cambia la porción activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo. El control deslizante se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio que se rompió en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra la conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador antiguo autoextraíble) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta era **Browse .ssdr...** en versiones anteriores a v0.9.3. |
| Pestaña **APD** | Pestaña | Configuración del muestreo externo de Predistorsión Adaptativa — selección por antena de TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestredor ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para el entrenamiento de APD para esa antena de TX. Elija una entrada RX/XVTR externa cuando conduzca un amplificador lineal externo. Las opciones se rellenan en vivo a partir del subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| Pestaña **Themes** | Pestaña | Pestaña de personalización de interfaz — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de color de la porción entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por porción. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de porción A–H | Botón | Haga clic en cualquier botón etiquetado (A–H) para abrir un selector de color y asignar un color personalizado para esa porción. Los cambios son visibles inmediatamente en widgets de VFO, superposiciones de panadapter e insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 porciones. |
| **Reset All to Defaults (Themes)** | Botón | Reinicia todos los colores personalizados de porción a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

Use los controles en la pestaña **Radio** para verificar actualizaciones de firmware y cargar firmware en la radio.

### Verificación de actualizaciones

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado lee "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado lee "Update available: v*x.x.x* — Download the SmartSDR installer from flexradio.com, then click **Select Installer...** to stage it." en ámbar.

### Preparación y carga de firmware

En v0.9.3 el botón **Browse .ssdr...** fue renombrado a **Select Installer...** y ahora acepta el instalador completo de SmartSDR tal como se descarga de FlexRadio, además de un archivo `.ssdr` preextraído.

1. Descargue el instalador de SmartSDR desde flexradio.com si aún no lo tiene localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — Instalador FlexRadio v4.2+ WiX
   - `.exe` — instalador antiguo autoextraíble
   - `.ssdr` — archivo de firmware preextraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El preparador detecta el formato del archivo a partir de los primeros 8 bytes y extrae la carga útil `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparing firmware from *filename*..." mientras la preparación está en curso.
4. Cuando la preparación se complete, haga clic en **Upload Firmware**. Una barra de progreso y una etiqueta de estado rastrean la carga.

### Notas

- Si la etiqueta de estado no se actualiza después de hacer clic en **Select Installer...**, verifique que el archivo seleccionado sea un `.msi`, `.exe` o `.ssdr` válido.
- No se desconecte de la radio mientras una carga esté en curso.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración de frecuencia de la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, cuando se detectaba un GPSDO, los campos de calibración estaban ocultos y reemplazados por un mensaje indicando que la corrección no era necesaria. La pestaña ahora siempre muestra el campo **Cal Frequency (MHz)** y el botón **Start**.

Una etiqueta de estado aparece junto a **Start** y proporciona retroalimentación en línea durante toda la secuencia de calibración:

| Texto de estado | Significado |
|---|---|
| Starting... | AetherSDR ha enviado los comandos de calibración a la radio. |
| Busy | El botón **Start** está deshabilitado; la calibración está en curso. |
| (texto de error) | Se reportó un problema; verifique el valor en **Cal Frequency (MHz)**. |

Cuando hay hardware GPSDO presente, la etiqueta en la parte superior del grupo lee "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO la etiqueta lee "Manual frequency offset calibration available." (ámbar). En ambos casos los controles debajo de la etiqueta se comportan idénticamente.

### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia de precisión conocida en **Cal Frequency (MHz)** (por ejemplo, una portadora WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no se inicia.
5. Haga clic en **Start**. La etiqueta del botón cambia a **Busy** y está deshabilitada hasta que se complete la secuencia de calibración.
6. Observe la etiqueta de estado para ver el progreso. Cuando se complete la calibración, el botón se vuelve a habilitar y **Freq Offset (ppb)** refleja la corrección medida.

### Notas

- Hacer clic en **Start** reinicia `freq_error_ppb` a 0 antes de comenzar el barrido, por lo que cualquier desplazamiento almacenado previamente se borra al inicio de cada ejecución.
- El estado de calibración se rastrea por instancia de diálogo. Cerrar y reabrir el diálogo reinicia la pantalla de estado; cualquier calibración del lado de la radio en curso continúa independientemente.

## Sugerencias

- Haga clic en **Check Status** después de hacer clic en **Start** o **Stop** si el indicador de estado no se actualiza por sí solo, para confirmar que el contenedor alcanzó el estado esperado.
- Si el botón **Start** permanece en el estado **Busy** después de una desconexión inesperada, cierre y reabra `Settings > Radio Setup...` para reiniciar el botón.

## Relacionado

- [Elegir dispositivos de entrada/salida de audio de PC](choose-pc-input-output-audio-devices.md)
- [Seleccionar Opus vs audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar autorregistro en TX y elegir una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
