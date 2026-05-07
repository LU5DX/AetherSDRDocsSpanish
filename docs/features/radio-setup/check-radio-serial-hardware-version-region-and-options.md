# Verificar Número de Serie, Versión de Hardware, Región y Opciones de la Radio

La pestaña Radio en Configuración de Radio muestra información de identificación reportada directamente por la radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Utilice esta página para verificar qué hardware y opciones tiene su radio antes de solucionar problemas o contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los campos de la pestaña Radio se completan con datos en vivo de la radio.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por la radio.
   - **Region** — la región regulatoria de la radio (muestra `USA` si la radio no reporta una).
   - **Options** — las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis según lo reportado por la radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con el prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones de radio licenciadas. |
| TX Follows Active Slice | Botón pulsador | TX sigue la slice activa. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. |
| Active Slice Follows TX | Botón pulsador | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |
| Deslizadores de nitidez de filtro Voice / CW / Digital | Deslizador | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón pulsador | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que está rota en firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita ninguna activación desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón pulsador | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón pulsador | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra "Connected" solo cuando el dispositivo conectado es un Antenna Genius que no es un ShackSwitch. Si un ShackSwitch es el dispositivo conectado, el estado de esta fila se oculta. |
| Connect / Disconnect (ShackSwitch) | Botón pulsador | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de descubrimiento AG. El descubrimiento automático a través de UDP también funciona sin esta fila. La fila muestra "Connected" solo cuando el dispositivo conectado se identifica como un ShackSwitch; la fila se oculta del estado "Connected" si un Antenna Genius que no es un ShackSwitch es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. El botón lee la IP de `SS_ManualIp` o, si está vacía, de la dirección del par activo cuando el dispositivo conectado es un ShackSwitch. |
| Select Installer... | Botón pulsador | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF de salida para el entrenamiento de APD para esa antena TX. Elija una entrada externa de RX/XVTR cuando maneje un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón pulsador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente alberga la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de color de las slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón pulsador | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles de inmediato en los widgets de VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando está seleccionada la opción **Use Aether defaults**. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón pulsador | Restablece todos los colores personalizados de las slices a la paleta integrada de AetherSDR. |

Los cuatro campos de Información de la Radio son de solo lectura. No hay claves de configuración persistente asociadas a ellos.

## Pestaña Firmware — seleccionar un instalador o archivo de firmware (v0.9.3)

En v0.9.3, el botón **Browse .ssdr...** pasó a llamarse **Select Installer...**. El botón ahora acepta el paquete completo del instalador de SmartSDR además de un archivo `.ssdr` preextraído, por lo que ya no es necesario extraer el firmware manualmente antes de la carga.

**Para preparar el firmware para la carga:**

1. Haga clic en **Check for Update**. Si hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2 y posteriores, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el archivo descargado, o elija un archivo `.ssdr` preextraído si tiene uno.
4. AetherSDR lee los primeros 8 bytes del archivo para detectar si es un paquete MSI, un EXE autoextraíble o un `.ssdr` sin procesar. La carga útil `.ssdr` se extrae automáticamente sin herramientas externas. El progreso se muestra en la barra de progreso y en la etiqueta de estado.
5. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

> **Nota:** En versiones anteriores a v0.9.3, al hacer clic en **Check for Update** cuando había una actualización disponible, el botón se convertía en un botón **Download vX.Y.Z** que descargaba y preparaba el firmware automáticamente. Ese comportamiento se ha eliminado. Debe descargar el instalador desde flexradio.com usted mismo y luego usar **Select Installer...** para prepararlo.

## Pestaña RX — calibración de frecuencia

En v0.9.2.1, los controles de calibración en la pestaña **RX** son siempre visibles, independientemente de si hay un GPSDO instalado. Anteriormente, los campos Cal Frequency, Start y Freq Offset estaban ocultos cuando se detectaba un GPSDO. El banner de estado en la parte superior del grupo ahora muestra:

- **GPSDO instalado** — "GPSDO installed. Manual frequency offset calibration available." (texto verde)
- **Sin GPSDO** — "Manual frequency offset calibration available." (texto ámbar)

Los siguientes controles ahora están disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia utilizada para la calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón pulsador | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en progreso. Antes de activar el barrido PLL, AetherSDR restablece el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones, aplicado después de que se complete la calibración o se establezca directamente para una corrección manual. |

Aparece una etiqueta de estado a la derecha del botón Start y se actualiza durante toda la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Inactivo | *(vacío)* | — |
| Frecuencia de calibración no ingresada | "Enter cal frequency" | Ámbar |
| Secuencia iniciada | "Starting…" | Gris-azul |
| En progreso | Se actualiza según el estado del PLL reportado por la radio | Gris-azul |

El botón Start se vuelve a habilitar y su etiqueta vuelve a **Start** cuando la secuencia de calibración se completa o falla.

## Pestaña RX — fuente de referencia de 10 MHz (v0.9.7)

En v0.9.7, el cuadro combinado **10 MHz Reference Source:** y su etiqueta de estado de bloqueo acompañante se actualizaron para manejar una gama más amplia de estados del oscilador reportados por la radio.

**Población del cuadro combinado:** La lista de fuentes disponibles ahora se construye dinámicamente cada vez que se abre la pestaña o cambia el estado del oscilador de la radio. Las fuentes aparecen en el combinado solo si la radio reporta el hardware relevante como presente, si la configuración actual o el estado activo usa esa fuente, o si se ha recibido el estado del oscilador (en cuyo caso TCXO y External 10 MHz siempre se incluyen como opciones). Las opciones fijas de versiones anteriores, que podían mostrar fuentes que la radio no tenía, ya no se utilizan.

| Valor de fuente | Etiqueta mostrada en el combinado |
|---|---|
| `auto` | Auto |
| `tcxo` | TCXO |
| `gpsdo` | GPSDO |
| `external` / `ext` | External 10 MHz |

**Etiqueta de estado de bloqueo:** La etiqueta a la derecha del combinado ahora muestra información de estado más detallada:

| Condición | Texto mostrado | Color |
|---|---|---|
| Aún no se ha recibido el estado del oscilador | "Waiting for oscillator status" | Gris-azul |
| Fuente bloqueada | `<source> Locked` | Verde (`#00c040`) |
| Fuente desbloqueada | `<source> Unlocked` | Rojo (`#c04040`) |
| El modo Auto ha seleccionado una fuente | `Auto -> <resolved source> Locked/Unlocked` | Verde o rojo |
| La configuración y el estado activo difieren | `<setting> -> <active> Locked/Unlocked` | Verde o rojo |
| External seleccionado pero no se detecta señal | `External 10 MHz` (with a note) | (nota: el texto original se corta) |
