# Seleccionar audio Opus vs sin comprimir para SmartLink

Seleccione el códec de audio que AetherSDR utiliza a través de conexiones SmartLink o LAN. Opus reduce el ancho de banda a costa de una pequeña compresión; PCM sin comprimir preserva la fidelidad total cuando el ancho de banda lo permite. Auto permite que la radio elija.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible sin una conexión activa.
- Abra `Settings > Radio Setup...` y haga clic en la pestaña **Audio**.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Audio Compression (SmartLink):**, haga clic en **Auto**, **Uncompressed** u **Opus** para seleccionar el códec.
   - **Auto**: la radio negocia el códec automáticamente (predeterminado).
   - **Uncompressed**: envía audio PCM sin procesar; utiliza más ancho de banda.
   - **Opus**: envía audio codificado en Opus; menor ancho de banda, compresión ligera.
4. Cierre el cuadro de diálogo. El ajuste surte efecto inmediatamente y se guarda.

## Qué hace cada control

| Control | Predeterminado | Valores válidos |
|---|---|---|
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Auto | Auto, Uncompressed, Opus |
| **Audio Boost:** | — | Activado / Desactivado |
| **Audio Buffer:** | 200 ms | 50–1000 ms |
| **Recording:** Radio Side / Client Side | Radio Side | Radio Side, Client Side |
| **Save to:** | — | Ruta de carpeta |
| **Auto-record on TX** | — | Marcado / Desmarcado |
| **Idle timeout:** | 120 seg | 10–3600 seg |
| **TX Follows Active Slice** | Falso | TX sigue a la slice activa. Es mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Falso | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. |
| **Voice / CW / Digital filter sharpness sliders** | — | 0–3. Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se desactiva cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | — | Activado / Desactivado. Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Connect | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL controla PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita señalización del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. Borrar el campo IP y hacer clic en **Connect** elimina la IP y el puerto manuales guardados de la configuración. |
| **Connect / Disconnect (PGXL)** | Connect | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. Borrar el campo IP y hacer clic en **Connect** elimina la IP y el puerto manuales guardados de la configuración. |
| **Connect / Disconnect (Antenna Genius)** | Connect | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. Borrar el campo IP y hacer clic en **Connect** elimina la IP y el puerto manuales guardados de la configuración. |
| **Connect / Disconnect (ShackSwitch)** | Connect | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. Borrar el campo IP y hacer clic en **Connect** elimina la IP y el puerto manuales guardados de la configuración. |
| **Cal Frequency (MHz):** | — | Frecuencia utilizada para la calibración manual. Disponible independientemente de si hay un GPSDO instalado. Si el campo está vacío al hacer clic en **Start**, aparece una advertencia y la calibración no comienza. |
| **Start** | — | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0, luego inicia el barrido de calibración PLL de la radio. El botón se desactiva y se etiqueta **Busy** mientras la calibración está en ejecución. |
| **Freq Offset (ppb):** | — | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Auto | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado (TCXO / GPSDO / External 10 MHz). El combo se rellena dinámicamente: las entradas TCXO y External 10 MHz aparecen siempre que la radio informe el estado del oscilador, el hardware relevante esté presente, o el valor actual o configurado coincida con esa fuente. GPSDO aparece cuando se detecta un GPSDO o el valor configurado es `gpsdo`. La etiqueta de estado de bloqueo junto al combo se actualiza en vivo y refleja la resolución de Auto (por ejemplo, **Auto -> GPSDO Locked**) y si se detecta una referencia externa. |
| **Select Installer...** | — | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs cabecera PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | — | Configuración del muestreador de predistorsión adaptativa externa: selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de restablecimiento del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ lo expone; las series 6000 y radios anteriores a 4.2.18 mantienen la pestaña invisible. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | INTERNAL | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | — | Envía `apd reset` a la radio, eliminando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (tab)** | — | Pestaña de personalización de la interfaz de usuario; actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Use Aether defaults | Cambia el esquema de colores de las slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| **Slice A–H color buttons** | — | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter e insignias de canal CAT. Los botones están desactivados cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | — | Restablece todos los colores personalizados de las slices a la paleta integrada de AetherSDR. |
| **FlexControl: Tuning Knob actions** | — | Acciones de botón disponibles para mapear: StepUp, StepDown, Equal, ToggleTune, ToggleMute, ToggleLock, NextSlice, PrevSlice, ToggleAgc, VolumeUp, VolumeDown, WheelFrequency, WheelVolume, WheelPower, WheelRit, WheelXit. |

## Pestaña Peripherals: borrar IP guardadas

Cuando se hace clic en el botón **Connect / Disconnect** mientras el campo IP está vacío, la IP y el puerto manuales guardados para ese dispositivo se eliminan de la configuración. Esto evita que AetherSDR se conecte automáticamente a un dispositivo cuya IP se ha borrado intencionalmente.

Si cierra el cuadro de diálogo Radio Setup con un campo IP vacío y existe una IP manual guardada previamente, AetherSDR elimina automáticamente esa IP y puerto guardados de la configuración y desconecta el dispositivo si está actualmente conectado.

## Cambios en ventanas de diálogo en v26.5.1

El cuadro de diálogo Radio Setup ahora utiliza una ventana sin marco cuando el ajuste `FramelessWindow` está habilitado. Se muestra una barra de título personalizada en la parte superior del diálogo, que proporciona los controles de ventana estándar (cerrar, minimizar, maximizar/restaurar). La barra de título muestra "Radio Setup".

Cuando el modo sin marco está activo:
- La barra de título aparece en la parte superior del diálogo.
- El área de contenido del cuerpo tiene un margen superior reducido (7 px en lugar de 9 px) para compensar la barra de título.
- El diálogo se puede arrastrar mediante la barra de título.
- Se instalan controladores de redimensionamiento en todos los bordes y esquinas mediante `FramelessResizer`.

Cuando el modo sin marco está deshabilitado, el diálogo utiliza la decoración de ventana nativa del sistema operativo y la barra de título personalizada está oculta.

## Actualización de firmware: cambios en v0.9.3

El botón **Browse .ssdr...** en la pestaña **Radio** ha sido renombrado a **Select Installer...**. Ahora acepta tres tipos de archivo además de un archivo `.ssdr` preextraído:

- `.msi`: el instalador SmartSDR basado en WiX utilizado por FlexRadio desde v4.2.
- `.exe`: el instalador autoextraíble antiguo.
- `.ssdr`: un archivo de firmware que ya ha extraído usted mismo.

El preparador de firmware examina los primeros 8 bytes del archivo seleccionado para determinar su formato (magia OLE/MSI o cabecera PE/COFF MZ) y extrae la carga útil `.ssdr` automáticamente sin requerir herramientas externas. El progreso se muestra en el área de estado debajo de los botones.

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

## Pestaña RX: cambios en calibración de frecuencia en v0.9.2.1

En versiones anteriores, el campo **Cal Frequency (MHz):** y el botón **Start** solo se mostraban cuando no había GPSDO instalado. A partir de v0.9.2.1, esos controles siempre son visibles en la pestaña **RX**. El banner de estado en la parte superior del grupo aún indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

Al hacer clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, aparece un mensaje de advertencia junto al botón y la calibración no continúa.
2. El desplazamiento de frecuencia se restablece a 0 (`radio set freq_error_ppb=0`) y la frecuencia de calibración se envía a la radio (`radio set cal_freq=<valor>`).
3. Comienza el barrido de calibración PLL de la radio (`radio pll_start`).
4. El botón **Start** se desactiva y muestra **Busy** durante la duración del barrido.
5. Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido y muestra el resultado cuando se completa.

## Pestaña RX: cambios en fuente del oscilador en v0.9.7

El combo **10 MHz Reference Source:** y su etiqueta de estado de bloqueo han sido rediseñados.

**Relleno del combo.** La lista de fuentes disponibles ahora se construye dinámicamente cada vez que se abre el diálogo o la radio informa el estado del oscilador, en lugar de ser fija al construir el diálogo. Las reglas son:

- **Auto** siempre está presente.
- **TCXO** aparece cuando la radio informa cualquier estado del oscilador, cuando `tcxoPresent` es verdadero, o cuando el valor actual o configurado es `tcxo`.
- **GPSDO** aparece cuando `gpsdoPresent` es verdadero o el valor actual o configurado es `gpsdo`.
- **External 10 MHz** aparece cuando la radio informa cualquier estado del oscilador, cuando `extPresent` es verdadero, o cuando el valor actual o configurado es `external`. Nota: la etiqueta ha cambiado de **External** a **External 10 MHz**.

El combo preselecciona el valor que coincide con el ajuste configurado actual de la radio (`oscSetting`). Si ese valor no está en la lista, se utiliza el elemento previamente seleccionado; si ninguno está presente, se selecciona **Auto**.
