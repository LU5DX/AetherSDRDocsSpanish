# Cambiar el MTU de red para configuraciones VPN/remotas

La configuración de MTU de red controla el tamaño máximo de paquete que la radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que disminuye el MTU de ruta disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network no es accesible cuando está desconectado.
- Conozca el MTU de su túnel VPN o ruta de red. Los MTU comunes de VPN son 1400–1450 bytes; una ruta Ethernet estándar es de 1500 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de número **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## Qué hace cada control

| Control | Descripción | Predeterminado |
|---|---|---|
| **Network MTU:** | Tamaño del paquete saliente en bytes. Reduzca este valor cuando opere a través de una VPN o cualquier enlace con un MTU reducido. | 1450 |
| **Apply** | Envía la configuración actual de la pestaña Network, incluido el valor de MTU, a la radio. | — |
| TX Follows Active Slice | TX sigue el slice (canal de recepción) activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. | False |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. | False |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0=menor latencia a 3=máxima nitidez) por modo; el control se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| Connect / Disconnect (TGXL) | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que dejó de funcionar en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita cierre de clave desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP detectada se rellena automáticamente. | — |
| Connect / Disconnect (PGXL) | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| Connect / Disconnect (Antenna Genius) | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho (no un ShackSwitch). | — |
| Connect / Disconnect (ShackSwitch) | Abre/cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (no ShackSwitch). | — |
| ⚙ Web UI (ShackSwitch) | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| Select Installer... | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` previamente extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en la versión v0.9.3. | — |
| APD (pestaña) | Configuración del muestreador externo de predistorsión adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de restablecimiento del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente en el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se obtienen en tiempo real del subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. | INTERNAL |
| Equalizer Reset (APD) | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. | — |
| Themes (pestaña) | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. | — |
| Use Aether defaults / Custom colors (botón de opción) | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| Botones de color del Slice A–H | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los controles VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. | — |
| Reset All to Defaults (Themes) | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

En la versión v0.9.3, el flujo de trabajo de preparación de firmware cambió. AetherSDR ya no descarga el firmware automáticamente cuando detecta una actualización. En su lugar, descargue usted mismo el instalador de SmartSDR desde flexradio.com y luego prepárelo manualmente.

### Preparar una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, aparece un mensaje de estado que indica la versión disponible y le indica que descargue el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado en verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi` — instalador WiX (FlexRadio SmartSDR v4.2 y posteriores)
   - `.exe` — instalador autoextraíble más antiguo
   - `.ssdr` — archivo de firmware previamente extraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado a `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
   - AetherSDR lee el archivo, detecta automáticamente su formato a partir de los primeros 8 bytes y extrae el contenido `.ssdr` si es necesario. Una etiqueta de estado muestra el progreso.
6. Cuando la preparación se complete y el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso sigue el proceso de carga.
   - No cierre el diálogo ni se desconecte de la radio mientras la carga esté en curso.

### Mensajes de estado del firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com y haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se requiere ninguna acción. |
| Preparing firmware from *filename*... | El preparador está leyendo y extrayendo el archivo seleccionado. |
| (texto de error en rojo) | La preparación o la carga falló. Verifique que el archivo sea un instalador o archivo de firmware SmartSDR válido e inténtelo de nuevo. |

### Notas

- El botón **Select Installer...** se llamaba **Browse .ssdr...** en versiones anteriores a v0.9.3.
- La preparación se ejecuta completamente en el cliente; no se requieren herramientas externas para desempaquetar los instaladores `.msi` o `.exe`.

## Calibración de frecuencia (pestaña RX)

En la versión v0.9.2.1, los controles de calibración de frecuencia de la pestaña RX están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. Ahora todos los campos de calibración siempre se muestran; una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido.
   - La radio primero restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) y luego inicia la secuencia de calibración del PLL.
5. Cuando la calibración se complete, el botón se vuelve a habilitar y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer el desplazamiento manualmente, introduzca un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido se ha enviado a la radio. |
| Busy | La calibración del PLL está en curso. |
| Enter cal frequency | El campo **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Introduzca un valor e inténtelo de nuevo. |

### Notas

- Al hacer clic en **Start** con el campo **Cal Frequency (MHz):** vacío se muestra una advertencia ámbar "Enter cal frequency" y no se envía ningún comando.
- La secuencia de calibración registra la frecuencia de calibración y el ID de ejecución en el registro de protocolo de depuración (`lcProtocol`). Puede verlo en el visor de registros de AetherSDR si el registro de diagnóstico está habilitado.
- Si el diálogo Radio Setup se cierra mientras hay una calibración en curso, la llamada de retorno en vuelo se descarta de forma segura; no se aplica ningún estado parcial.

## Conexión a un ShackSwitch (pestaña Peripherals)

El conmutador de antenas ShackSwitch utiliza el mismo protocolo de control AG UDP/TCP que el Antenna Genius. En la versión v0.9.4, la pestaña Peripherals incorporó una fila dedicada al ShackSwitch, separada de la fila del Antenna Genius, junto con un botón **⚙ Web UI**.

### Conectar manualmente

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Localice la fila **ShackSwitch**.
   - Si la radio ya ha descubierto el ShackSwitch mediante la baliza UDP, el campo IP se rellena automáticamente.
   - De lo contrario, escriba la dirección IP del ShackSwitch en el campo IP.
4. Haga clic en **Connect**.
   - AetherSDR se conecta en el puerto 9007 utilizando el protocolo de control AG.
   - La IP se guarda en `SS_ManualIp` y el puerto en `SS_ControlPort` para que AetherSDR se reconecte automáticamente en el siguiente inicio.
5. La fila muestra el estado Connected. La fila del Antenna Genius se mostrará como no conectada durante la misma sesión, ya que las dos filas son mutuamente exclusivas — solo una puede mostrar Connected a la vez.

### Abrir la interfaz web del ShackSwitch

1. Confirme que el ShackSwitch está conectado (estado Connected mostrado en la fila ShackSwitch).
2. Haga clic en **⚙ Web UI**.
   - Aet
