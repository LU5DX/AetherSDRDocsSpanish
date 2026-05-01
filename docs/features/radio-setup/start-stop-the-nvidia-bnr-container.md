# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) aplica supresión de ruido basada en IA a su audio de micrófono. Use los controles en la pestaña Audio para iniciar, detener o verificar el estado del contenedor sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible cuando está desconectada.
- El contenedor NVIDIA Broadcast debe estar instalado en su sistema independientemente de AetherSDR. AetherSDR lo controla pero no lo instala.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Ubique la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que AetherSDR se lance, haga clic en **Autostart Container** para que esté activo.
5. Para iniciar el contenedor inmediatamente, haga clic en **Start**.
6. Para detener un contenedor en ejecución, haga clic en **Stop**.
7. Para consultar el estado actual sin cambiarlo, haga clic en **Check Status**. El punto de estado de color junto a los controles se actualiza para reflejar Running, Stopped o Unknown.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Cuando está activo, AetherSDR inicia el contenedor NVIDIA BNR automáticamente al iniciarse. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR inmediatamente. |
| **Stop** | Botón | Detiene un contenedor NVIDIA BNR en ejecución inmediatamente. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el punto de estado. |
| Punto de estado NVIDIA BNR | Indicador | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown. |
| **TX Follows Active Slice** | Botón | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante operación Split. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo. El control se desactiva cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón | Habilita la selección automática de nivel de filtro para ese modo y desactiva el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta de lado de radio rota en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado Connected solo cuando el dispositivo identificado en esa conexión es un Antenna Genius (no un ShackSwitch). |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre/cierra conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de radiodifusión AG. La auto-descubrimiento via UDP también funciona sin esta fila. La fila se oculta del estado Connected si un Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa `webPort` de la baliza si es mayor a 1024; de lo contrario, recurre a `SS_WebPort` o puerto 5000. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX FlexRadio v4.2+), `.exe` (instalador de auto-extracción antiguo) o archivo de firmware pre-extraído `.ssdr`. El preparador de firmware auto-detecta el formato de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae `.ssdr` sin herramientas externas. La etiqueta era **Browse .ssdr...** en versiones anteriores a v0.9.3. |
| Pestaña **APD** | Pestaña | Configuración del muestreador Adaptive Pre-Distortion externo — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que usa la radio para muestrear el RF saliente para entrenamiento APD en esa antena TX. Elija una entrada RX/XVTR externa al usar un amplificador lineal externo. Las opciones se rellenan en vivo del sub-objeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Pestaña **Themes** | Pestaña | Pestaña de personalización de interfaz — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de radio | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completo personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter y insignias de canal CAT. Los botones se desactivan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

Use los controles en la pestaña **Radio** para verificar actualizaciones de firmware y cargar firmware en la radio.

### Verificar actualizaciones

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado dice "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado dice "Update available: v*x.x.x* — Download the SmartSDR installer from flexradio.com, then click **Select Installer...** to stage it." en ámbar.

### Preparar y cargar firmware

En v0.9.3 el botón **Browse .ssdr...** fue renombrado a **Select Installer...** y ahora acepta el instalador SmartSDR completo tal como se descarga de FlexRadio, además de un archivo `.ssdr` pre-extraído.

1. Descargue el instalador SmartSDR de flexradio.com si no lo tiene ya localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — instalador WiX FlexRadio v4.2+
   - `.exe` — instalador de auto-extracción antiguo
   - `.ssdr` — archivo de firmware pre-extraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El preparador detecta el formato de archivo de los primeros 8 bytes y extrae la carga útil `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparing firmware from *filename*..." mientras la preparación está en progreso.
4. Cuando la preparación se complete, haga clic en **Upload Firmware**. Una barra de progreso y etiqueta de estado rastrean la carga.

### Notas

- Si la etiqueta de estado no se actualiza después de hacer clic en **Select Installer...**, verifique que el archivo seleccionado sea un `.msi`, `.exe` o `.ssdr` válido.
- No desconecte de la radio mientras una carga esté en progreso.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración de frecuencia de la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, cuando se detectaba un GPSDO, los campos de calibración se ocultaban y se reemplazaban con un mensaje indicando que no se requería corrección. La pestaña ahora siempre muestra el campo **Cal Frequency (MHz)** y el botón **Start**.

Una etiqueta de estado aparece junto a **Start** y proporciona retroalimentación en línea durante toda la secuencia de calibración:

| Texto de estado | Significado |
|---|---|
| Starting... | AetherSDR ha enviado los comandos de calibración a la radio. |
| Busy | El botón **Start** está desactivado; la calibración está en progreso. |
| (texto de error) | Se reportó un problema; verifique el valor en **Cal Frequency (MHz)**. |

Cuando hay hardware GPSDO presente, la etiqueta en la parte superior del grupo dice "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO la etiqueta dice "Manual frequency offset calibration available." (ámbar). En ambos casos los controles debajo de la etiqueta se comportan idénticamente.

### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)** (por ejemplo, una portadora WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no se inicia.
5. Haga clic en **Start**. La etiqueta del botón cambia a **Busy** y se desactiva hasta que se complete la secuencia de calibración.
6. Observe la etiqueta de estado para el progreso. Cuando se complete la calibración, el botón se reactiva y **Freq Offset (ppb)** refleja la corrección medida.

### Notas

- Hacer clic en **Start** restablece `freq_error_ppb` a 0 antes de comenzar el barrido, por lo que cualquier desplazamiento almacenado previamente se borra al inicio de cada ejecución.
- El estado de calibración se rastrea por instancia de diálogo. Cerrar y reabrir el diálogo restablece la pantalla de estado; cualquier calibración en progreso del lado de la radio continúa de forma independiente.

## Interfaz web ShackSwitch (pestaña Peripherals)

En v0.9.4 la pestaña **Peripherals** ganó un botón **⚙ Web UI** en la fila ShackSwitch. Úselo para abrir la página de configuración integrada del ShackSwitch en su navegador del sistema sin tener que buscar manualmente la dirección IP del dispositivo.

### Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Ubique la fila **ShackSwitch**.
4. Haga clic en **⚙ Web UI**. AetherSDR determina la dirección y puerto correctos y abre la página en su navegador predeterminado.

### Cómo se resuelven la dirección y el puerto

AetherSDR usa el siguiente orden de preferencia para construir la URL:

1. La dirección IP almacenada en `SS_ManualIp`. Si esa está vacía y ShackSwitch está actualmente conectado, se usa la dirección de par en vivo.
2. El puerto anunciado en la baliza ShackSwitch (`webPort`), siempre que sea mayor a 1024.
3. Si el puerto de baliza no es utilizable, el valor almacenado en `SS_WebPort`.
4. Si ninguno está establecido, el puerto 5000 se usa como fallback final.

Si
