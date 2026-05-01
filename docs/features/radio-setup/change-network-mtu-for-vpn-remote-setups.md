# Cambiar la MTU de red para configuraciones de VPN/remoto

La configuración de MTU de red controla el tamaño máximo de paquete que la radio envía por la red. Bajarlo previene fragmentación cuando se conecta a través de una VPN u otro túnel que reduce la MTU disponible en la ruta.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La pestaña Network no es accesible cuando está desconectado.
- Conozca la MTU de su túnel VPN o ruta de red. Las MTU VPN comunes son 1400–1450 bytes; una ruta Ethernet estándar es 1500 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el spinbox **Network MTU:**.
4. Establezca el valor que coincida con la MTU de su ruta de red.
5. Haga clic en **Apply** para enviar la nueva MTU a la radio.

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| **Network MTU:** | Tamaño de paquete saliente en bytes. Bájelo cuando opere sobre una VPN o cualquier enlace con una MTU reducida. | 1450 |
| **Apply** | Envía la configuración actual de la pestaña Network, incluido el valor de MTU, a la radio. | — |
| TX Follows Active Slice | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante operación Split. | False |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | False |
| Voice / CW / Digital filter sharpness sliders | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. | — |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. | — |
| Connect / Disconnect (TGXL) | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL controla PTT de la radio mediante su cable de interlock de hardware; no se requiere keying del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. | — |
| Connect / Disconnect (PGXL) | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| Connect / Disconnect (Antenna Genius) | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado Connected solo cuando el dispositivo conectado es un Antenna Genius real (no un ShackSwitch). | — |
| Connect / Disconnect (ShackSwitch) | Abre/cierra conexión a un switch de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de difusión AG. El autodescubrimiento via UDP también funciona sin esta fila. La fila se oculta del estado Connected si un Antenna Genius (no ShackSwitch) es el dispositivo conectado. | — |
| ⚙ Web UI (ShackSwitch) | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa `webPort` del beacon si es mayor a 1024; en caso contrario, vuelve a `SS_WebPort` o puerto 5000. | — |
| Select Installer... | Abre un selector de archivo que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o archivo firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. | — |
| APD (tab) | Configuración del muestreador de Predistorsión Adaptiva Externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios 6000-series y pre-4.2.18 mantienen la pestaña invisible. | — |
| ANT1 / ANT2 / XVTA / XVTB sampler combos (APD) | Selecciona la ruta de retroalimentación que la radio usa para muestrear la RF saliente para entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| Equalizer Reset (APD) | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| Themes (tab) | Pestaña de personalización de interfaz — actualmente alberga la sección Slice Colors. | — |
| Use Aether defaults / Custom colors (radio button) | Cambia el esquema de color de slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| Slice A–H color buttons | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y insignias de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. | — |
| Reset All to Defaults (Themes) | Reinicia todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

En v0.9.3, el flujo de trabajo de preparación de firmware cambió. AetherSDR ya no descarga firmware automáticamente cuando se detecta una actualización. En su lugar, descargue el instalador de SmartSDR de flexradio.com usted mismo y luego prépárelo manualmente.

### Preparar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si una actualización está disponible, aparece un mensaje de estado indicándole la versión disponible y dirigiéndole a descargar el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — Instalador WiX (FlexRadio SmartSDR v4.2 y posterior)
   - `.exe` — instalador autoextraíble antiguo
   - `.ssdr` — archivo firmware preextraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivo filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
   - AetherSDR lee el archivo, detecta automáticamente su formato a partir de los primeros 8 bytes y extrae el payload `.ssdr` si es necesario. Una etiqueta de estado muestra el progreso.
6. Cuando la preparación se completa y el botón de carga se activa, haga clic en **Upload Firmware**.
   - Una barra de progreso rastrea la carga.
   - No cierre el diálogo ni desconecte de la radio mientras la carga esté en curso.

### Mensajes de estado de firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más nueva. Descargue el instalador desde flexradio.com, luego haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se requiere acción. |
| Preparing firmware from *filename*... | El preparador está leyendo y extrayendo el archivo seleccionado. |
| (error text in red) | La preparación o carga falló. Verifique que el archivo sea un instalador de SmartSDR válido o archivo firmware e intente de nuevo. |

### Notas

- El botón **Select Installer...** se etiquetaba como **Browse .ssdr...** en versiones anteriores a v0.9.3.
- La preparación se ejecuta completamente en el cliente; no se requieren herramientas externas para desempacar instaladores `.msi` o `.exe`.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración de frecuencia de la pestaña RX están disponibles independientemente de si un GPSDO está instalado. Anteriormente, los controles **Cal Frequency (MHz):** **Start** y **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. Ahora todos los campos de calibración se muestran siempre; una etiqueta de estado en la parte superior del grupo indica si un GPSDO está presente (texto verde) o no (texto ámbar).

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido.
   - La radio primero reinicia el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego comienza la secuencia de calibración PLL.
5. Cuando la calibración se completa, el botón se rehabilita y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer el desplazamiento manualmente, introduzca un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido ha sido enviado a la radio. |
| Busy | La calibración PLL está en progreso. |
| Enter cal frequency | El campo **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Introduzca un valor e intente de nuevo. |

### Notas

- Hacer clic en **Start** con el campo **Cal Frequency (MHz):** vacío muestra una advertencia ámbar "Enter cal frequency" y no envía comandos.
- La secuencia de calibración registra la frecuencia cal e ID de ejecución en el registro de protocolo de depuración (`lcProtocol`). Puede verlo en el visor de registros de AetherSDR si el registro de diagnóstico está habilitado.
- Si el diálogo Radio Setup se cierra mientras se ejecuta una calibración, el callback en vuelo se descarta de forma segura; no se aplica estado parcial.

## Conectar a un ShackSwitch (pestaña Peripherals)

El switch de antena ShackSwitch usa el mismo protocolo de control AG UDP/TCP que el Antenna Genius. En v0.9.4, la pestaña Peripherals ganó una fila dedicada de ShackSwitch separada de la fila Antenna Genius, junto con un botón **⚙ Web UI**.

### Conectar manualmente

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila **ShackSwitch**.
   - Si la radio ya ha descubierto el ShackSwitch mediante beacon UDP, el campo IP está rellenado previamente.
   - En caso contrario, escriba la dirección IP del ShackSwitch en el campo IP.
4. Haga clic en **Connect**.
   - AetherSDR se conecta en el puerto 9007 usando el protocolo de control AG.
   - La IP se guarda en `SS_ManualIp` y el puerto en `SS_ControlPort` para que AetherSDR se reconecte automáticamente al siguiente inicio.
5. La fila muestra estado Connected. La fila Antenna Genius se mostrará como no conectada para la misma sesión porque las dos filas son mutuamente excluyentes — solo una puede mostrar Connected a la vez.

### Abrir la interfaz web de ShackSwitch

1. Confirme que ShackSwitch está conectado (estado Connected mostrado en la fila ShackSwitch).
2. Haga clic en **⚙ Web UI**.
   - Aet
