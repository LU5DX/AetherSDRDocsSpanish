# Selecciona Opus o Audio sin Comprimir para SmartLink

Elige el códec de audio que AetherSDR usa en conexiones SmartLink o LAN. Opus reduce el ancho de banda a costa de una pequeña compresión; PCM sin comprimir preserva la fidelidad completa cuando el ancho de banda lo permite. Auto permite que la radio elija.

## Antes de empezar

- AetherSDR debe estar conectada a la radio. La pestaña Audio no es accesible sin una conexión activa.
- Abre `Settings > Radio Setup...` y haz clic en la pestaña **Audio**.

## Pasos

1. Abre `Settings > Radio Setup...`.
2. Haz clic en la pestaña **Audio**.
3. En **Audio Compression (SmartLink):** haz clic en **Auto**, **Uncompressed** u **Opus** para seleccionar el códec.
   - **Auto** — la radio negocia el códec automáticamente (predeterminado).
   - **Uncompressed** — envía audio PCM sin procesar; usa más ancho de banda.
   - **Opus** — envía audio codificado con Opus; menor ancho de banda, compresión leve.
4. Cierra el diálogo. La configuración toma efecto inmediatamente y se guarda.

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
| **TX Follows Active Slice** | False | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. |
| **Active Slice Follows TX** | False | Cambia el slice activo cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Voice / CW / Digital filter sharpness sliders** | — | 0–3. Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | — | Enabled / Disabled. Habilita la selección automática de nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Connect | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL controla PTT de la radio a través de su cable de bloqueo de hardware; no se necesita manipulación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Connect | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Connect | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado Connected solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| **Connect / Disconnect (ShackSwitch)** | Connect | Abre/cierra conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión AG. La autodescubrimiento vía UDP también funciona sin esta fila. Fila oculta del estado 'Connected' si Antenna Genius (no-ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | — | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa webPort de la baliza si es > 1024; de lo contrario, recurre a `SS_WebPort` o puerto 5000. |
| **Cal Frequency (MHz):** | — | Frecuencia usada para calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío cuando haces clic en **Start**, aparece una advertencia y la calibración no comienza. |
| **Start** | — | Establece la frecuencia de calibración, reinicia `freq_error_ppb` a 0, luego inicia el barrido de calibración PLL de la radio. El botón se deshabilita y se etiqueta como **Busy** mientras se ejecuta la calibración. |
| **Freq Offset (ppb):** | — | Desplazamiento de frecuencia manual en partes por mil millones. |
| **Select Installer...** | — | Abre un explorador de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El organizador de firmware detecta automáticamente el formato de los primeros 8 bytes (magia OLE/MSI frente a encabezado PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | — | Configuración del muestreador Adaptive Pre-Distortion externo — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | INTERNAL | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para entrenamiento APD de esa antena TX. Elige una entrada RX/XVTR externa cuando impulses un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | — | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (tab)** | — | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Use Aether defaults | Cambia el esquema de color del slice entre la paleta AetherSDR incorporada y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Slice A–H color buttons** | — | Haz clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | — | Reinicia todos los colores de slice personalizados a la paleta AetherSDR incorporada. |

## Actualización de firmware — cambios en v0.9.3

El botón **Browse .ssdr...** en la pestaña **Radio** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo además de un archivo `.ssdr` preextraído:

- `.msi` — el instalador SmartSDR basado en WiX usado por FlexRadio desde v4.2 en adelante.
- `.exe` — el instalador autoextraíble más antiguo.
- `.ssdr` — un archivo de firmware que ya has extraído tú mismo.

El organizador de firmware examina los primeros 8 bytes del archivo seleccionado para determinar su formato (magia OLE/MSI o encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` automáticamente sin requerir herramientas externas. El progreso se muestra en el área de estado debajo de los botones.

Cuando **Check for Update** informa que hay una versión de firmware más nueva disponible, AetherSDR ya no ofrece descargar el instalador automáticamente. En su lugar, el área de estado muestra:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.

Para actualizar el firmware:

1. Abre `Settings > Radio Setup...` y haz clic en la pestaña **Radio**.
2. Haz clic en **Check for Update**. Ten en cuenta el número de versión mostrado en el área de estado.
3. Descarga el instalador SmartSDR para esa versión desde flexradio.com.
4. Haz clic en **Select Installer...** y elige el archivo `.msi`, `.exe` o `.ssdr` descargado.
5. AetherSDR prepara el firmware. Observa la barra de progreso y la etiqueta de estado.
6. Cuando la preparación se complete, haz clic en **Upload Firmware** para transferir el firmware a la radio.

## Pestaña RX — cambios de calibración de frecuencia en v0.9.2.1

En versiones anteriores, el campo **Cal Frequency (MHz):** y el botón **Start** solo se mostraban cuando no había un GPSDO instalado. A partir de v0.9.2.1, esos controles siempre están visibles en la pestaña **RX**. El banner de estado en la parte superior del grupo aún indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

Cuando haces clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, aparece un mensaje de advertencia al lado del botón y la calibración no continúa.
2. El desplazamiento de frecuencia se reinicia a 0 (`radio set freq_error_ppb=0`) y la frecuencia de calibración se envía a la radio (`radio set cal_freq=<value>`).
3. Comienza el barrido de calibración PLL de la radio (`radio pll_start`).
4. El botón **Start** se deshabilita y muestra **Busy** durante el barrido.
5. Una etiqueta de estado al lado del botón se actualiza mientras el barrido progresa y muestra el resultado cuando se completa.

## Pestaña Peripherals — cambios de ShackSwitch en v0.9.4

La fila **Antenna Genius** ahora muestra un estado Connected solo cuando el dispositivo identificado en la conexión es un Antenna Genius que no es ShackSwitch. Si un ShackSwitch es el dispositivo conectado, la fila Antenna Genius oculta su indicador Connected y la fila **ShackSwitch** muestra Connected en su lugar.

Se ha añadido un nuevo botón **⚙ Web UI** a la fila ShackSwitch. Haz clic en él para abrir la interfaz de configuración web incorporada del dispositivo ShackSwitch en el navegador del sistema. La URL se construye de la siguiente manera:

1. AetherSDR usa la IP de `SS_ManualIp`, o si está vacía y un ShackSwitch está actualmente conectado, la dirección de par en vivo.
2. El puerto se toma del campo `webPort` de la baliza cuando ese valor es mayor que 1024. Si no es así, AetherSDR recurre a la configuración `SS_WebPort` o puerto 5000.

Si no hay dirección IP disponible (no conectado y `SS_ManualIp` está vacío), hacer clic en **⚙ Web UI** no hace nada.

## Consejos

- En una LAN local rápida, **Uncompressed** evita artefactos de códec y es la mejor opción para escucha crítica o decodificación de modo digital.
- En un enlace lento o congestionado (VPN, SmartLink celular), **Opus** reduce los descartes de audio. Emparejalo con un valor más grande de **Audio Buffer:** (50–1000 ms) para absorber variabilidad.
- Si el audio suena delgado o bajo sobre SmartLink, intenta habilitar **Audio Boost:** junto con Opus.
- Si hay un GPSDO instalado, la calibración de frecuencia rara vez es necesaria, pero los controles siguen disponibles si deseas verificar o ajustar manualmente el desplazamiento.
