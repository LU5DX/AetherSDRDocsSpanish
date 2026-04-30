# Seleccionar Opus o audio sin comprimir para SmartLink

Seleccione el códec de audio que AetherSDR usa en conexiones SmartLink o LAN. Opus reduce el ancho de banda a costa de una pequeña cantidad de compresión; PCM sin comprimir preserva fidelidad completa cuando el ancho de banda lo permite. Auto permite que la radio elija.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible sin una conexión activa.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Audio Compression (SmartLink):**, haga clic en **Auto**, **Uncompressed** u **Opus** para seleccionar el códec.
   - **Auto** — la radio negocia el códec automáticamente (predeterminado).
   - **Uncompressed** — envía audio PCM sin procesar; usa más ancho de banda.
   - **Opus** — envía audio codificado en Opus; menor ancho de banda, compresión ligera.
4. Cierre el diálogo. La configuración toma efecto inmediatamente y se guarda.

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
| **Voice / CW / Digital filter sharpness sliders** | — | 0–3. Establece la agudeza del filtro (0 = menor latencia a 3 = más agudo) por modo. El control deslizante se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | — | Enabled / Disabled. Habilita selección automática de nivel de filtro para ese modo; deshabilita el control deslizante de agudeza manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Connect | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL controla PTT de la radio a través de su cable de interbloqueo de hardware; no se requiere modulación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se pre-completa. |
| **Connect / Disconnect (PGXL)** | Connect | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Connect | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |
| **Cal Frequency (MHz):** | — | Frecuencia usada para calibración manual. Disponible sin importar si un GPSDO está instalado. Si el campo está vacío cuando haga clic en **Start**, aparece una advertencia y la calibración no comienza. |
| **Start** | — | Establece la frecuencia de calibración, reinicia `freq_error_ppb` a 0, luego inicia el barrido de calibración PLL de la radio. El botón está deshabilitado y etiquetado como **Busy** mientras se ejecuta la calibración. |
| **Freq Offset (ppb):** | — | Compensación de frecuencia manual en partes por mil millones. |
| **Select Installer...** | — | Abre un selector de archivos que acepta instalador WiX `.msi` (SmartSDR v4.2+ de FlexRadio), instalador autoextraíble `.exe` (más antiguo), o archivo de firmware `.ssdr` pre-extraído. El gestor de firmware detecta automáticamente el formato de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | — | Configuración de muestreador Pre-Distorsión Adaptativa externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo radios serie FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; radios serie 6000 y firmware anterior a 4.2.18 mantienen la pestaña invisible. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | INTERNAL | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | — | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (tab)** | — | Pestaña de personalización de interfaz — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Use Aether defaults | Cambia el esquema de color del slice entre la paleta AetherSDR incorporada y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Slice A–H color buttons** | — | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter y insignias de canal CAT. Los botones están deshabilitados cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | — | Reinicia todos los colores de slice personalizados a la paleta AetherSDR incorporada. |

## Actualización de firmware — cambios en v0.9.3

El botón **Browse .ssdr...** en la pestaña **Radio** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo además de un archivo `.ssdr` pre-extraído:

- `.msi` — el instalador SmartSDR basado en WiX usado por FlexRadio desde v4.2 en adelante.
- `.exe` — el instalador autoextraíble más antiguo.
- `.ssdr` — un archivo de firmware que ya ha extraído usted mismo.

El gestor de firmware examina los primeros 8 bytes del archivo seleccionado para determinar su formato (magic OLE/MSI o encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` automáticamente sin requerir herramientas externas. El progreso se muestra en el área de estado debajo de los botones.

Cuando **Check for Update** reporta que una versión de firmware más nueva está disponible, AetherSDR ya no ofrece descargar el instalador automáticamente. En su lugar el área de estado muestra:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.

Para actualizar firmware:

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Radio**.
2. Haga clic en **Check for Update**. Anote el número de versión mostrado en el área de estado.
3. Descargue el instalador SmartSDR para esa versión desde flexradio.com.
4. Haga clic en **Select Installer...** y elija el archivo `.msi`, `.exe` o `.ssdr` descargado.
5. AetherSDR prepara el firmware. Observe la barra de progreso y la etiqueta de estado.
6. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Pestaña RX — cambios de calibración de frecuencia en v0.9.2.1

En versiones anteriores, el campo **Cal Frequency (MHz):** y el botón **Start** solo se mostraban cuando ningún GPSDO estaba instalado. A partir de v0.9.2.1, esos controles siempre están visibles en la pestaña **RX**. El banner de estado en la parte superior del grupo aún indica si un GPSDO está presente (texto verde) o no (texto ámbar).

Cuando haga clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, aparece un mensaje de advertencia junto al botón y la calibración no procede.
2. La compensación de frecuencia se reinicia a 0 (`radio set freq_error_ppb=0`) y la frecuencia de calibración se envía a la radio (`radio set cal_freq=<value>`).
3. El barrido de calibración PLL de la radio comienza (`radio pll_start`).
4. El botón **Start** está deshabilitado y muestra **Busy** durante el barrido.
5. Una etiqueta de estado junto al botón se actualiza mientras el barrido progresa y muestra el resultado cuando está completo.

## Consejos

- En una LAN local rápida, **Uncompressed** evita cualquier artefacto de códec y es la mejor opción para escucha crítica o decodificación de modo digital.
- En un enlace lento o congestionado (VPN, SmartLink celular), **Opus** reduce interrupciones de audio. Combínelo con un valor **Audio Buffer:** más grande (50–1000 ms) para absorber jitter.
- Si el audio suena delgado o silencioso en SmartLink, intente habilitar **Audio Boost:** junto con Opus.
- Si un GPSDO está instalado, la calibración de frecuencia raramente es necesaria, pero los controles aún están disponibles si desea verificar o ajustar manualmente la compensación.
- Al preparar firmware desde un instalador completo SmartSDR `.msi` o `.exe`, la preparación puede tomar algunos segundos más que cargar un archivo `.ssdr` pre-extraído directamente.

## Solución de problemas

- **Los botones Audio Compression están atenuados o faltando** — la pestaña Audio solo se construye después de hacer clic en ella, y solo cuando una radio está conectada. Verifique la conexión, luego haga clic en la pestaña Audio nuevamente.
- **La calidad de audio es pobre incluso con Uncompressed seleccionado** — verifique el ancho de banda y latencia de la red. Considere aumentar **Audio Buffer:** para reducir subestéticas. Vea [Turn on audio boost or enlarge the audio buffer for remote operation](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md).
- **El botón Start muestra "Busy" y no vuelve** — si el barrido PLL no se completa, cierre y reabra el diálogo Radio Setup para reiniciar el estado del botón, luego intente nuevamente.
- **Aparece advertencia "Enter cal frequency" al hacer clic en Start** — escriba una frecuencia válida (en MHz) en el campo **Cal Frequency (MHz):** antes de hacer clic en **Start**.
- **Select Installer... no prepara nada / la barra de progreso se queda en cero** — confirme que el archivo sea un SmartSDR `.msi`, `.exe` o `.ssdr` válido. Los instaladores corruptos o parcialmente descargados causarán que la preparación falle. Descargue el archivo nuevamente desde flexradio.com e intente nuevamente.
- **La pestaña APD no es visible** — la pestaña **APD** solo aparece en radios serie FLEX-8x00 ejecutando SmartSDR 4.2.18 o posterior. No está disponible en radios serie 6000 o firmware anterior.

## Relacionado

- [Turn on audio boost or enlarge the audio buffer for remote operation](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Choose PC input/output audio devices](choose-pc-input-output-audio-devices.md)
- [Enable auto-record on TX and pick a save folder](enable-auto-record-on-tx-)
