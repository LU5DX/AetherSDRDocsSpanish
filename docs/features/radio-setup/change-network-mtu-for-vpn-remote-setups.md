# Cambiar la MTU de red para configuraciones VPN/remotas

El ajuste de MTU de red controla el tamaño máximo de paquete que la radio envía a través de la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que reduce la MTU de ruta disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network no es accesible cuando está desconectado.
- Conozca la MTU de su túnel VPN o ruta de red. Las MTU comunes de VPN son 1400–1450 bytes; una ruta Ethernet estándar es de 1500 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el cuadro de ajuste **Network MTU:**.
4. Establezca el valor para que coincida con la MTU de su ruta de red.
5. Haga clic en **Apply** para enviar la nueva MTU a la radio.

## Función de cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Network MTU:** | Tamaño del paquete saliente en bytes. Reduzca este valor cuando opere a través de una VPN o cualquier enlace con una MTU reducida. | 1450 |
| **Apply** | Envía la configuración actual de la pestaña Network, incluido el valor de MTU, a la radio. | — |
| TX Follows Active Slice | TX sigue al receptor activo. Excluyente con Active Slice Follows TX. Se desactiva automáticamente durante la operación en Split. | False |
| Active Slice Follows TX | Cambia el receptor activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Excluyente con TX Follows Active Slice. | False |
| Deslizadores de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| Auto (Voice / CW / Digital) | Activa la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| Connect / Disconnect (TGXL) | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL activa el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita activación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. | — |
| Connect / Disconnect (PGXL) | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| Connect / Disconnect (Antenna Genius) | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado Connected solo cuando el dispositivo conectado es un Antenna Genius propiamente dicho (no un ShackSwitch). | — |
| Connect / Disconnect (ShackSwitch) | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en el beacon de difusión AG. El descubrimiento automático a través de UDP también funciona sin esta fila. La fila se oculta del estado Connected si un Antenna Genius (que no sea ShackSwitch) es el dispositivo conectado. | — |
| ⚙ Web UI (ShackSwitch) | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| Select Installer... | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs. PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| APD (pestaña) | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. | INTERNAL |
| Equalizer Reset (APD) | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| Themes (pestaña) | Pestaña de personalización de la interfaz de usuario: actualmente aloja la sección Slice Colors. | — |
| Use Aether defaults / Custom colors (botón de opción) | Cambia el esquema de color del receptor entre la paleta integrada de AetherSDR y un conjunto personalizado completamente por receptor. Respaldado por `SliceColorManager::useCustomColors()`. | Use Aether defaults |
| Botones de color de receptor A–H | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese receptor. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando está seleccionado **Use Aether defaults**. Hasta 8 receptores. | — |
| Reset All to Defaults (Themes) | Restablece todos los colores personalizados del receptor a la paleta integrada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

En v0.9.3, el flujo de trabajo de preparación del firmware cambió. AetherSDR ya no descarga firmware automáticamente cuando se detecta una actualización. En su lugar, descargue el instalador de SmartSDR desde flexradio.com usted mismo y luego prepárelo manualmente.

### Preparación de una actualización de firmware

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**.
   - Si hay una actualización disponible, aparece un mensaje de estado que indica la versión disponible y le indica que descargue el instalador desde flexradio.com.
   - Si el firmware está actualizado, un mensaje de estado verde confirma la versión instalada.
4. Descargue el instalador de SmartSDR desde flexradio.com. Formatos aceptados:
   - `.msi`: instalador WiX (FlexRadio SmartSDR v4.2 y posterior)
   - `.exe`: instalador autoextraíble más antiguo
   - `.ssdr`: archivo de firmware preextraído
5. Haga clic en **Select Installer...**.
   - Se abre un selector de archivos filtrado para `*.msi`, `*.exe` y `*.ssdr`.
   - Seleccione el archivo que descargó.
   - AetherSDR lee el archivo, detecta automáticamente su formato a partir de los primeros 8 bytes y extrae la carga útil `.ssdr` si es necesario. Una etiqueta de estado muestra el progreso.
6. Cuando la preparación se complete y el botón de carga se active, haga clic en **Upload Firmware**.
   - Una barra de progreso rastrea la carga.
   - No cierre el diálogo ni se desconecte de la radio mientras la carga está en curso.

### Mensajes de estado del firmware

| Mensaje | Significado |
|---|---|
| Update available: v*x.y.z* | Existe una versión de firmware más reciente. Descargue el instalador desde flexradio.com, luego haga clic en **Select Installer...**. |
| Firmware is up to date (v*x.y.z*) | No se necesita ninguna acción. |
| Preparing firmware from *filename*... | El preparador está leyendo y extrayendo el archivo seleccionado. |
| (texto de error en rojo) | La preparación o carga falló. Verifique que el archivo sea un instalador o archivo de firmware SmartSDR válido e intente nuevamente. |

### Notas

- El botón **Select Installer...** se llamaba **Browse .ssdr...** en versiones anteriores a v0.9.3.
- La preparación se ejecuta completamente en el cliente; no se requieren herramientas externas para descomprimir los instaladores `.msi` o `.exe`.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1, los controles de calibración de frecuencia de la pestaña RX están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. Ahora todos los campos de calibración se muestran siempre; una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

### Fuente de referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** en la pestaña RX selecciona la referencia de oscilador utilizada por la radio. En v0.9.7, el cuadro combinado y su etiqueta de estado de bloqueo se actualizaron con los siguientes cambios de comportamiento:

- El cuadro combinado se completa dinámicamente. Solo aparecen las fuentes compatibles con el hardware conectado. Las entradas **TCXO** y **External 10 MHz** se muestran cuando la radio informa que esas fuentes están presentes o cuando el estado del oscilador actual o activo las involucra, incluso si los indicadores de presencia de hardware aún no se han informado. **Auto** está siempre disponible.
- La etiqueta junto al cuadro combinado ahora muestra la fuente resuelta así como el estado de bloqueo. Cuando **Auto** está seleccionado y la radio ha elegido una fuente específica, la etiqueta muestra `Auto -> <source>`. Cuando se selecciona una fuente específica y la radio está usando una diferente, la etiqueta muestra `<selected> -> <active>`. Cuando la configuración y el estado coinciden, solo se muestra la fuente activa.
- El estado de bloqueo se agrega: `Locked` (verde) o `Unlocked` (rojo).
- Si **External 10 MHz** está seleccionado o activo pero no se detecta ninguna referencia externa, la etiqueta agrega `(not detected)`.
- Mientras la radio aún no ha informado el estado del oscilador, la etiqueta muestra `Waiting for oscillator status` en gris.
- La etiqueta del cuadro combinado para la fuente externa cambió de **External** a **External 10 MHz**.

#### Opciones del cuadro combinado 10 MHz Reference Source

| Opción | Cuándo se muestra |
|---|---|
| Auto | Siempre. |
| TCXO | Cuando se ha recibido el estado del oscilador, o cuando la radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Cuando la radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Cuando se ha recibido el estado del oscilador, o cuando la radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido.
   - La radio primero restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego comienza la secuencia de calibración PLL.
5. Cuando la calibración se completa, el botón se vuelve a habilitar y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer el desplazamiento manualmente, ingrese un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido se ha enviado a la radio. |
| Busy | La calibración PLL está en curso. |
| Enter cal frequency | El campo **Cal Frequency (MHz):** estaba
