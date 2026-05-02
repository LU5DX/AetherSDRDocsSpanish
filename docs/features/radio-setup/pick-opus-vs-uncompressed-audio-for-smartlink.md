# Seleccionar Opus o audio sin comprimir para SmartLink

Seleccione el códec de audio que AetherSDR utiliza sobre conexiones SmartLink o LAN. Opus reduce el ancho de banda a costa de una pequeña compresión; el PCM sin comprimir preserva la fidelidad total cuando el ancho de banda lo permite. Auto permite que el radio elija.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio no es accesible sin una conexión activa.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Bajo **Audio Compression (SmartLink):**, haga clic en **Auto**, **Uncompressed** u **Opus** para seleccionar el códec.
   - **Auto** — el radio negocia el códec automáticamente (valor predeterminado).
   - **Uncompressed** — envía audio PCM sin procesar; utiliza más ancho de banda.
   - **Opus** — envía audio codificado con Opus; menor ancho de banda, ligera compresión.
4. Cierre el diálogo. La configuración surte efecto inmediatamente y se guarda.

## Qué hace cada control

| Control | Predeterminado | Valores válidos |
|---|---|---|
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Auto | Auto, Uncompressed, Opus |
| **Audio Boost:** | — | Enabled / Disabled |
| **Audio Buffer:** | 200 ms | 50–1000 ms |
| **Recording:** Radio Side / Client Side | Radio Side | Radio Side, Client Side |
| **Save to:** | — | Ruta de carpeta |
| **Auto-record on TX** | — | Checked / Unchecked |
| **Idle timeout:** | 120 sec | 10–3600 sec |
| **TX Follows Active Slice** | False | TX sigue el slice (rebanada de frecuencia) activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | False | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | — | 0–3. Establece la nitidez del filtro (0 = menor latencia, 3 = máxima nitidez) por modo. El control deslizante se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | — | Enabled / Disabled. Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Connect | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que falló en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo hardware; no se necesita cierre de clave del lado del cliente. Si el campo de IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Connect | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Connect | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected únicamente cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| **Connect / Disconnect (ShackSwitch)** | Connect | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo UDP/TCP del AG en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión del AG. El autodescubrimiento mediante UDP también funciona sin esta fila. La fila oculta el estado 'Connected' si el dispositivo conectado es un Antenna Genius (no ShackSwitch). |
| **⚙ Web UI (ShackSwitch)** | — | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el webPort de la baliza si es > 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Cal Frequency (MHz):** | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| **Start** | — | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0 y luego inicia el barrido de calibración del PLL del radio. El botón se deshabilita y se etiqueta como **Busy** mientras la calibración está en curso. |
| **Freq Offset (ppb):** | — | Desplazamiento de frecuencia manual en partes por mil millones. |
| **Select Installer...** | — | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (número mágico OLE/MSI frente a PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | — | Configuración del muestreador externo de predistorsión adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de restablecimiento del ecualizador. La pestaña se oculta a menos que el radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; los radios de la serie 6000 y los anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Combinaciones de muestreadores ANT1 / ANT2 / XVTA / XVTB (APD)** | INTERNAL | Selecciona la ruta de retroalimentación que el radio utiliza para muestrear la RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se obtienen en tiempo real del subobjeto `apd sampler` del radio. Vuelve a INTERNAL si el radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | — | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| **Themes (tab)** | — | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Use Aether defaults | Cambia el esquema de colores de los slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Botones de color de Slice A–H** | — | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | — | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. |

## Actualización de firmware — cambios en v0.9.3

El botón **Browse .ssdr...** de la pestaña **Radio** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo además de un archivo `.ssdr` ya extraído:

- `.msi` — el instalador SmartSDR basado en WiX que usa FlexRadio desde la v4.2 en adelante.
- `.exe` — el instalador autoextraíble antiguo.
- `.ssdr` — un archivo de firmware que usted ya ha extraído.

El preparador de firmware examina los primeros 8 bytes del archivo seleccionado para determinar su formato (número mágico OLE/MSI o encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` automáticamente sin necesidad de herramientas externas. El progreso se muestra en el área de estado debajo de los botones.

Cuando **Check for Update** informa que hay una versión de firmware más reciente disponible, AetherSDR ya no ofrece descargar el instalador automáticamente. En su lugar, el área de estado muestra:

> Actualización disponible: v*X.Y.Z*  
> Descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en 'Select Installer...' para prepararlo.

Para actualizar el firmware:

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Radio**.
2. Haga clic en **Check for Update**. Tome nota del número de versión que aparece en el área de estado.
3. Descargue el instalador de SmartSDR para esa versión desde flexradio.com.
4. Haga clic en **Select Installer...** y elija el archivo `.msi`, `.exe` o `.ssdr` descargado.
5. AetherSDR prepara el firmware. Observe la barra de progreso y la etiqueta de estado.
6. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware al radio.

## Pestaña RX — cambios en la calibración de frecuencia en v0.9.2.1

En versiones anteriores, el campo **Cal Frequency (MHz):** y el botón **Start** solo se mostraban cuando no había un GPSDO instalado. A partir de v0.9.2.1, esos controles siempre son visibles en la pestaña **RX**. El banner de estado en la parte superior del grupo sigue indicando si hay un GPSDO presente (texto verde) o no (texto ámbar).

Al hacer clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, aparece un mensaje de advertencia junto al botón y la calibración no continúa.
2. El desplazamiento de frecuencia se restablece a 0 (`radio set freq_error_ppb=0`) y la frecuencia de calibración se envía al radio (`radio set cal_freq=<value>`).
3. Comienza el barrido de calibración del PLL del radio (`radio pll_start`).
4. El botón **Start** se deshabilita y muestra **Busy** durante el barrido.
5. Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido y muestra el resultado al completarse.

## Pestaña Peripherals — cambios de ShackSwitch en v0.9.4

La fila **Antenna Genius** ahora muestra el estado Connected únicamente cuando el dispositivo identificado en la conexión es un Antenna Genius que no es ShackSwitch. Si el dispositivo conectado es un ShackSwitch, la fila Antenna Genius oculta su indicador Connected y la fila **ShackSwitch** muestra Connected en su lugar.

Se ha agregado un nuevo botón **⚙ Web UI** a la fila ShackSwitch. Haga clic en él para abrir la interfaz de configuración web integrada del dispositivo ShackSwitch en su navegador del sistema. La URL se construye de la siguiente manera:

1. AetherSDR utiliza la IP de `SS_ManualIp`, o si está vacía y hay un ShackSwitch conectado actualmente, la dirección del par activo.
2. El puerto se toma del campo `webPort` de la baliza cuando ese valor es mayor que 1024. De lo contrario, AetherSDR recurre a la configuración `SS_WebPort` o al puerto 5000.

Si no hay ninguna dirección IP disponible (sin conexión y `SS_ManualIp` está vacío), hacer clic en **⚙ Web UI** no tiene ningún efecto.

## Consejos

- En una LAN local rápida, **Uncompressed** evita cualquier artefacto del códec y es la mejor opción para escucha crítica o decodificación de modos digitales.
- En un enlace lento o congestionado (VPN, SmartLink celular), **Opus** reduce las interrupciones de audio. Combínelo con un valor mayor de **Audio Buffer:** (50–1000 ms) para absorber el jitter.
- Si el audio suena débil o bajo durante SmartLink, pruebe habilitar **Audio Boost:** junto con Opus.
- Si hay un GPSDO instalado, la calibración de frecuencia rara vez es necesaria, pero los controles siguen disponibles si desea verificar o ajustar manualmente el desplazamiento.
