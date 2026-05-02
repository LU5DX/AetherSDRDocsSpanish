# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) aplica supresión de ruido basada en IA al audio de su micrófono. Use los controles de la pestaña Audio para iniciar, detener o verificar el estado del contenedor sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible cuando está desconectado.
- El contenedor NVIDIA Broadcast debe estar instalado en su sistema de forma independiente a AetherSDR. AetherSDR lo controla, pero no lo instala.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que se lance AetherSDR, haga clic en **Autostart Container** para activarlo.
5. Para iniciar el contenedor de inmediato, haga clic en **Start**.
6. Para detener un contenedor en ejecución, haga clic en **Stop**.
7. Para consultar el estado actual sin modificarlo, haga clic en **Check Status**. El indicador de estado de color junto a los controles se actualiza para reflejar Running, Stopped o Unknown.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Cuando está activo, AetherSDR inicia el contenedor NVIDIA BNR automáticamente al arrancar. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR de inmediato. |
| **Stop** | Botón | Detiene un contenedor NVIDIA BNR en ejecución de inmediato. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el indicador de estado. |
| Indicador de estado NVIDIA BNR | Indicador | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown. |
| **TX Follows Active Slice** | Botón | TX sigue al slice (receptor virtual) activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro para Voice / CW / Digital | Deslizador | Establece la nitidez del filtro (0=menor latencia a 3=mayor nitidez) por modo. El deslizador se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE con firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que no funciona en el firmware 4.2. Si el campo de IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected solo cuando el dispositivo identificado en esa conexión es un Antenna Genius (no un ShackSwitch). |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre/cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento mediante UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (que no sea ShackSwitch). |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic frente a PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta era **Browse .ssdr...** en versiones anteriores a v0.9.3. |
| Pestaña **APD** | Pestaña | Configuración del muestreador externo de Adaptive Pre-Distortion — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. |
| Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente en el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa al usar un amplificador lineal externo. Las opciones se obtienen en tiempo real del subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| Pestaña **Themes** | Pestaña | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto totalmente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de los slices A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

Use los controles de la pestaña **Radio** para buscar actualizaciones de firmware y cargar firmware en la radio.

### Verificar actualizaciones

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra "Firmware is up to date (v*x.x.x*)." en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra "Update available: v*x.x.x* — Download the SmartSDR installer from flexradio.com, then click **Select Installer...** to stage it." en ámbar.

### Preparar y cargar firmware

En v0.9.3 el botón **Browse .ssdr...** pasó a llamarse **Select Installer...** y ahora acepta el instalador completo de SmartSDR descargado desde FlexRadio, además de un archivo `.ssdr` ya extraído.

1. Descargue el instalador de SmartSDR desde flexradio.com si no lo tiene localmente.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos que acepta:
   - `.msi` — instalador WiX de FlexRadio v4.2+
   - `.exe` — instalador autoextraíble más antiguo
   - `.ssdr` — archivo de firmware ya extraído
3. Seleccione el archivo. AetherSDR prepara el firmware automáticamente. El preparador detecta el formato del archivo a partir de los primeros 8 bytes y extrae la carga útil `.ssdr` sin requerir herramientas externas. La etiqueta de estado muestra "Preparing firmware from *filename*..." mientras la preparación está en curso.
4. Cuando la preparación finalice, haga clic en **Upload Firmware**. Una barra de progreso y una etiqueta de estado registran la carga.

### Notas

- Si la etiqueta de estado no se actualiza después de hacer clic en **Select Installer...**, verifique que el archivo seleccionado sea un `.msi`, `.exe` o `.ssdr` válido.
- No se desconecte de la radio mientras haya una carga en curso.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración de frecuencia de la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, cuando se detectaba un GPSDO, los campos de calibración se ocultaban y se reemplazaban con un mensaje que indicaba que la corrección no era necesaria. La pestaña ahora siempre muestra el campo **Cal Frequency (MHz)** y el botón **Start**.

Una etiqueta de estado aparece junto a **Start** y proporciona retroalimentación en línea durante toda la secuencia de calibración:

| Texto de estado | Significado |
|---|---|
| Starting... | AetherSDR ha enviado los comandos de calibración a la radio. |
| Busy | El botón **Start** está deshabilitado; la calibración está en curso. |
| (texto de error) | Se informó un problema; verifique el valor en **Cal Frequency (MHz)**. |

Cuando el hardware GPSDO está presente, la etiqueta en la parte superior del grupo muestra "GPSDO installed. Manual frequency offset calibration available." (en verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (en ámbar). En ambos casos, los controles debajo de la etiqueta funcionan de manera idéntica.

### Para calibrar el desplazamiento de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia precisa en **Cal Frequency (MHz)** (por ejemplo, una portadora de WWV o WWVH).
4. Verifique que el valor sea correcto. Si el campo está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no se inicia.
5. Haga clic en **Start**. La etiqueta del botón cambia a **Busy** y se deshabilita hasta que la secuencia de calibración finalice.
6. Observe la etiqueta de estado para seguir el progreso. Cuando la calibración finalice, el botón se vuelve a habilitar y **Freq Offset (ppb)** refleja la corrección medida.

### Notas

- Al hacer clic en **Start** se restablece `freq_error_ppb` a 0 antes de iniciar el barrido, por lo que cualquier desplazamiento almacenado previamente se borra al comienzo de cada ejecución.
- El estado de calibración se registra por instancia de diálogo. Cerrar y volver a abrir el diálogo restablece la pantalla de estado; cualquier calibración en curso del lado de la radio continúa de forma independiente.

## Interfaz web de ShackSwitch (pestaña Peripherals)

En v0.9.4 la pestaña **Peripherals** incorporó un botón **⚙ Web UI** en la fila de ShackSwitch. Úselo para abrir la página de configuración integrada del ShackSwitch en su navegador del sistema sin necesidad de buscar manualmente la dirección IP del dispositivo.

### Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila **ShackSwitch**.
4. Haga clic en **⚙ Web UI**. AetherSDR determina la dirección y el puerto correctos y abre la página en su navegador predeterminado.

### Cómo se resuelven la dirección y el puerto

AetherSDR utiliza el siguiente orden de preferencia para construir la URL:

1. La dirección IP almacenada en `SS_ManualIp`. Si está vacía y el ShackSwitch está conectado actualmente, se usa la dirección del par activo en su lugar.
2. El puerto anunciado en la baliza del ShackSwitch (`webPort`), siempre que sea mayor que 1024.
3. Si el puerto de la baliza no es utilizable, se usa el valor almacenado en `SS_WebPort`.
4. Si ninguno está configurado, se usa el puerto 5000 como último recurso.

Si
