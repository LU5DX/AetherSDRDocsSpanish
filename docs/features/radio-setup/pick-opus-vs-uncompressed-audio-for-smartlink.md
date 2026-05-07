# Selección de audio Opus versus sin comprimir para SmartLink

Seleccione el códec de audio que utiliza AetherSDR a través de conexiones SmartLink o LAN. Opus reduce el ancho de banda a costa de una pequeña cantidad de compresión; el PCM sin comprimir preserva la fidelidad total cuando el ancho de banda lo permite. Auto permite que la radio elija.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible sin una conexión activa.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Audio Compression (SmartLink):**, haga clic en **Auto**, **Uncompressed** u **Opus** para seleccionar el códec.
   - **Auto** — la radio negocia el códec automáticamente (predeterminado).
   - **Uncompressed** — envía audio PCM sin procesar; utiliza más ancho de banda.
   - **Opus** — envía audio codificado en Opus; menor ancho de banda, compresión ligera.
4. Cierre el diálogo. El ajuste surte efecto inmediatamente y se guarda.

## Qué hace cada control

| Control | Predeterminado | Valores válidos |
|---|---|---|
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Auto | Auto, Uncompressed, Opus |
| **Audio Boost:** | — | Habilitado / Deshabilitado |
| **Audio Buffer:** | 200 ms | 50–1000 ms |
| **Recording:** Radio Side / Client Side | Radio Side | Radio Side, Client Side |
| **Save to:** | — | Ruta de carpeta |
| **Auto-record on TX** | — | Marcado / Desmarcado |
| **Idle timeout:** | 120 s | 10–3600 s |
| **TX Follows Active Slice** | Falso | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Falso | Cambia el slice activo cuando el TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Voice / CW / Digital filter sharpness sliders** | — | 0–3. Ajusta la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | — | Habilitado / Deshabilitado. Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Connect | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL acciona el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita señalización del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Connect | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Connect | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado Conectado solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| **Connect / Disconnect (ShackSwitch)** | Connect | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión AG. El autodescubrimiento mediante UDP también funciona sin esta fila. Fila oculta del estado 'Conectado' si Antenna Genius (que no es ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | — | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el webPort de la baliza si es > 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Cal Frequency (MHz):** | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| **Start** | — | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0, luego inicia el barrido de calibración PLL de la radio. El botón se deshabilita y etiqueta como **Busy** mientras la calibración se está ejecutando. |
| **Freq Offset (ppb):** | — | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Auto | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO / GPSDO / External 10 MHz). El combo se completa dinámicamente: las entradas TCXO y External 10 MHz aparecen siempre que la radio informa el estado del oscilador, el hardware relevante está presente, o el valor actual o configurado coincide con esa fuente. GPSDO aparece cuando se detecta un GPSDO o el valor configurado es `gpsdo`. La etiqueta de estado de bloqueo junto al combo se actualiza en vivo y refleja la resolución de Auto (por ejemplo, **Auto -> GPSDO Locked**) y si se detecta una referencia externa. |
| **Select Installer...** | — | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble anterior) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **APD (pestaña)** | — | Configuración del muestreador de pre-distorsión adaptativa externa: selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de restablecimiento del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y radios anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | INTERNAL | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | — | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (pestaña)** | — | Pestaña de personalización de la interfaz de usuario: actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Use Aether defaults | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Botones de color Slice A–H** | — | Haga clic en cualquier botón con letras (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | — | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. |

## Actualización de firmware — cambios en v0.9.3

El botón **Browse .ssdr...** en la pestaña **Radio** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo además de un archivo `.ssdr` preextraído:

- `.msi` — el instalador SmartSDR basado en WiX utilizado por FlexRadio desde v4.2.
- `.exe` — el instalador autoextraíble anterior.
- `.ssdr` — un archivo de firmware que usted ya ha extraído.

El gestor de firmware examina los primeros 8 bytes del archivo seleccionado para determinar su formato (magia OLE/MSI o cabecera PE/COFF MZ) y extrae la carga útil `.ssdr` automáticamente sin requerir herramientas externas. El progreso se muestra en el área de estado debajo de los botones.

Cuando **Check for Update** informa que hay una versión de firmware más reciente disponible, AetherSDR ya no ofrece descargar el instalador automáticamente. En su lugar, el área de estado muestra:

> Update available: v*X.Y.Z*  
> Download the SmartSDR installer from flexradio.com, then click 'Select Installer...' to stage it.

Para actualizar el firmware:

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Radio**.
2. Haga clic en **Check for Update**. Anote el número de versión mostrado en el área de estado.
3. Descargue el instalador SmartSDR para esa versión desde flexradio.com.
4. Haga clic en **Select Installer...** y elija el archivo `.msi`, `.exe` o `.ssdr` descargado.
5. AetherSDR prepara el firmware. Observe la barra de progreso y la etiqueta de estado.
6. Cuando la preparación esté completa, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Pestaña RX — cambios en la calibración de frecuencia en v0.9.2.1

En versiones anteriores, el campo **Cal Frequency (MHz):** y el botón **Start** solo se mostraban cuando no había GPSDO instalado. Desde v0.9.2.1, esos controles siempre están visibles en la pestaña **RX**. El banner de estado en la parte superior del grupo aún indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

Cuando hace clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, aparece un mensaje de advertencia junto al botón y la calibración no procede.
2. El desplazamiento de frecuencia se restablece a 0 (`radio set freq_error_ppb=0`) y la frecuencia de calibración se envía a la radio (`radio set cal_freq=<valor>`).
3. Comienza el barrido de calibración PLL de la radio (`radio pll_start`).
4. El botón **Start** se deshabilita y muestra **Busy** durante la duración del barrido.
5. Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido y muestra el resultado cuando se completa.

## Pestaña RX — cambios en la fuente del oscilador en v0.9.7

El combo **10 MHz Reference Source:** y su etiqueta de estado de bloqueo han sido rediseñados.

**Población del combo.** La lista de fuentes disponibles ahora se construye dinámicamente cada vez que se abre el diálogo o la radio informa el estado del oscilador, en lugar de ser fija al momento de la construcción del diálogo. Las reglas son:

- **Auto** siempre está presente.
- **TCXO** aparece cuando la radio informa cualquier estado del oscilador, cuando `tcxoPresent` es verdadero, o cuando el valor actual o configurado es `tcxo`.
- **GPSDO** aparece cuando `gpsdoPresent` es verdadero o el valor actual o configurado es `gpsdo`.
- **External 10 MHz** aparece cuando la radio informa cualquier estado del oscilador, cuando `extPresent` es verdadero, o cuando el valor actual o configurado es `external`. Nota: la etiqueta ha cambiado de **External** a **External 10 MHz**.

El combo preselecciona el valor que coincide con la configuración actual de la radio (`oscSetting`). Si ese valor no está en la lista, se utiliza el elemento seleccionado anteriormente; si ninguno está presente, se selecciona **Auto**.
