# Cambiar la MTU de red para configuraciones VPN/remotas

La configuración de MTU de red controla el tamaño máximo de paquete que envía la radio por la red. Reducirlo previene la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce la MTU disponible de la ruta.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network no está accesible cuando está desconectado.
- Conozca la MTU de su túnel VPN o ruta de red. Las MTU de VPN comunes son 1400–1450 bytes; una ruta Ethernet estándar es 1500 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro **Network MTU:**.
4. Establezca el valor para que coincida con la MTU de su ruta de red.
5. Haga clic en **Apply** para enviar la nueva MTU a la radio.

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| **Network MTU:** | Tamaño del paquete saliente en bytes. Redúzcalo cuando opere sobre una VPN o cualquier enlace con MTU reducida. | 1450 |
| **Apply** | Envía la configuración actual de la pestaña Network, incluyendo el valor de MTU, a la radio. | — |
| TX Follows Active Slice | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante operación Split. | False |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. | — |
| Auto (Voice / CW / Digital) | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. | — |
| Connect / Disconnect (TGXL) | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` en conexión para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que se rompió en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de bloqueo de hardware; no se necesita codificación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se prellenará. | — |
| Connect / Disconnect (PGXL) | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| Connect / Disconnect (Antenna Genius) | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. | — |
| Select Installer... | Abre un selector de archivos que acepta instalador WiX .msi (FlexRadio v4.2+), instalador .exe (antiguo autoextraíble) o archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. | — |
| APD (tab) | Configuración del muestreador externo de Predistorsión Adaptativa: selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña se oculta a menos que la radio indique `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| Combos muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en tiempo real a partir del subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. | INTERNAL |
| Equalizer Reset (APD) | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience nuevamente. | — |
| Themes (tab) | Pestaña de personalización de interfaz: actualmente alberga la sección Slice Colors. | — |
| Use Aether defaults / Custom colors (botón de radio) | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| Botones de color Slice A–H | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets de VFO, superposiciones de panadapter e insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. | — |
| Reset All to Defaults (Themes) | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

En v0.9.3, el flujo de trabajo de preparación de firmware cambió. AetherSDR ya no descarga firmware automáticamente cuando se detecta una actualización. En su lugar, descargue el instalador de SmartSDR desde flexradio.com usted mismo, luego préparelo manualmente.

### Preparar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, aparece un mensaje de estado indicándole la versión disponible y dirigiéndolo a descargar el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — Instalador WiX (FlexRadio SmartSDR v4.2 y posterior)
   - `.exe` — Instalador autoextraíble antiguo
   - `.ssdr` — Archivo de firmware preextraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
   - AetherSDR lee el archivo, detecta automáticamente su formato a partir de los primeros 8 bytes, y extrae la carga útil `.ssdr` si es necesario. Una etiqueta de estado muestra el progreso.
6. Cuando la preparación se completa y el botón de carga se activa, haga clic en **Upload Firmware**.
   - Una barra de progreso rastrea la carga.
   - No cierre el diálogo ni desconecte la radio mientras la carga esté en progreso.

### Mensajes de estado de firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más nueva. Descargue el instalador desde flexradio.com, luego haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se requiere acción. |
| Preparing firmware from *filename*... | El preparador está leyendo y extrayendo el archivo seleccionado. |
| (error text in red) | La preparación o carga falló. Verifique que el archivo sea un instalador o archivo de firmware SmartSDR válido e intente nuevamente. |

### Notas

- El botón **Select Installer...** se etiquetaba como **Browse .ssdr...** en versiones anteriores a v0.9.3.
- La preparación se ejecuta completamente en el cliente; no se requieren herramientas externas para desempaquetar instaladores `.msi` o `.exe`.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración de frecuencia de la pestaña RX están disponibles independientemente de si se instala un GPSDO. Anteriormente, los controles **Cal Frequency (MHz):**,  **Start** y **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. Ahora todos los campos de calibración siempre se muestran; una etiqueta de estado en la parte superior del grupo indica si un GPSDO está presente (texto verde) o no (texto ámbar).

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza conforme avanza el barrido.
   - La radio primero reinicia el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego comienza la secuencia de calibración de PLL.
5. Cuando la calibración se completa el botón se habilita nuevamente y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer el desplazamiento manualmente, ingrese un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido ha sido enviado a la radio. |
| Busy | La calibración de PLL está en progreso. |
| Enter cal frequency | El campo **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Ingrese un valor e intente nuevamente. |

### Notas

- Hacer clic en **Start** con el campo **Cal Frequency (MHz):** vacío muestra una advertencia ámbar "Enter cal frequency" y no envía comandos.
- La secuencia de calibración registra la frecuencia de calibración e ID de ejecución en el registro del protocolo de depuración (`lcProtocol`). Puede verlo en el visor de registros de AetherSDR si está habilitado el registro de diagnóstico.
- Si el diálogo Radio Setup se cierra mientras se ejecuta una calibración, la devolución de llamada en vuelo se descarta de forma segura; no se aplica estado parcial.

## Consejos

- Si no está seguro qué MTU usar, comience en 1400 bytes e incremente hasta ver pérdida de paquetes o interrupciones de audio, luego disminuya de 10–20 bytes.
- La configuración **Audio Buffer:** (encontrada en la pestaña **Audio**) puede ayudar a absorber fluctuaciones en enlaces VPN independientemente de la configuración de MTU. Vea [Turn on audio boost or enlarge the audio buffer for remote operation](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md).

## Solución de problemas

- **Apply no tiene efecto visible** — Confirme que la radio aún está conectada. Si la conexión se perdió, reconecte a través de `Settings > Connect to Radio...` y repita los pasos.
- **El audio se entrecorta después de cambiar la MTU** — El nuevo valor puede ser demasiado grande para la ruta. Reduzca **Network MTU:** por otros 20–50 bytes y haga clic en **Apply** nuevamente.
- **El botón Start permanece deshabilitado después de la calibración** — Si el diálogo se cerró y reabrió durante un barrido, haga clic en **Start** nuevamente con la frecuencia de calibración deseada. La ejecución anterior se descartó limpiamente.
- **Select Installer... no muestra progreso** — Asegúrese de que el archivo sea un SmartSDR `.msi`, `.exe` o `.ssdr` válido. Los archivos de otras fuentes no serán reconocidos por el preparador de firmware.

## Relacionado

- [Switch the radio between DHCP and static IP](switch-the-radio-between-dhcp-and-static-ip.md)
- [Turn on audio boost or enlarge the audio buffer for remote operation](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Pick Opus vs uncompressed audio for SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
