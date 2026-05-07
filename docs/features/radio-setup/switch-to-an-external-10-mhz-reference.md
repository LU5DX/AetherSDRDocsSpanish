# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo seleccionar un reloj de referencia externo de 10 MHz en una FLEX-8600 conectada. Utilice una referencia externa cuando tenga un oscilador disciplinado por GPS u otra fuente de 10 MHz de precisión y desee que el radio se sincronice con ella en lugar de con su oscilador interno.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo de Configuración del Radio requiere una conexión activa con el radio.
- Su señal de referencia externa de 10 MHz debe estar conectada al puerto REF IN del panel posterior de la FLEX-8600 antes de cambiar la fuente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo de Configuración del Radio.
2. Haga clic en la pestaña `RX`.
3. Localice el cuadro combinado `10 MHz Reference Source:`.
4. Seleccione `External 10 MHz` en el cuadro combinado. Para volver al oscilador interno, seleccione `Auto`.

## Qué hace cada control

| Control | Tipo | Rango válido / Comportamiento |
|---|---|---|
| `10 MHz Reference Source:` | Cuadro combinado | `Auto` \| `TCXO` \| `GPSDO` \| `External 10 MHz`. Las opciones mostradas dependen del hardware instalado y del estado actual del oscilador informado por el radio. El cuadro combinado se completa dinámicamente: `TCXO` aparece cuando el hardware tiene un TCXO o cuando el radio informa actualmente TCXO como su estado activo; `GPSDO` aparece cuando hay un GPSDO presente; `External 10 MHz` aparece cuando se detecta una referencia externa o está actualmente activa. El estado de bloqueo se muestra junto al cuadro combinado y se actualiza en vivo (ver más abajo). |
| Etiqueta de estado de bloqueo | Indicador | Muestra la fuente del oscilador actual y el estado de bloqueo. Cuando se selecciona `Auto`, la etiqueta muestra `Auto -> <fuente activa>` para indicar lo que el radio ha elegido. Cuando la fuente seleccionada difiere del estado activo, se muestran ambas (ej. `TCXO -> GPSDO`). Agrega `Locked` (verde) o `Unlocked` (rojo). Si se selecciona `External 10 MHz` pero no se detecta una señal externa, la etiqueta agrega `(not detected)`. Mientras espera que el radio informe el estado, la etiqueta muestra `Waiting for oscillator status` (gris). |
| `TX Follows Active Slice` | Botón pulsador | TX sigue la slice activa. Mutuamente excluyente con `Active Slice Follows TX`. Se deshabilita automáticamente durante la operación en Split. |
| `Active Slice Follows TX` | Botón pulsador | Cambia la slice activa cuando TX se mueve externamente (ej. WSJT-X o CAT). Mutuamente excluyente con `TX Follows Active Slice`. |
| `Deslizadores de nitidez de filtro Voice / CW / Digital` | Deslizador (0–3) | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| `Auto (Voice / CW / Digital)` | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| `Connect / Disconnect (TGXL)` | Botón pulsador | Abre/cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que se rompió en el firmware 4.2. Si el campo IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se completa previamente. |
| `Connect / Disconnect (PGXL)` | Botón pulsador | Abre/cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| `Connect / Disconnect (Antenna Genius)` | Botón pulsador | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado "Conectado" cuando un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo conectado. |
| `Connect / Disconnect (ShackSwitch)` | Botón pulsador | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en el beacon de difusión de AG. El descubrimiento automático a través de UDP también funciona sin esta fila. Fila oculta del estado "Conectado" si un Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| `⚙ Web UI (ShackSwitch)` | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del beacon si es > 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| `Select Installer...` | Botón pulsador | Abre un selector de archivos que acepta `.msi` (instalador WiX FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta era `Browse .ssdr...` antes de v0.9.3. |
| `APD` (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que el radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y los radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. |
| `Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)` | Cuadro combinado | Selecciona la ruta de retroalimentación que el radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Predeterminado `INTERNAL`. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` del radio. Recurre a `INTERNAL` si el radio informa un valor no reconocido. |
| `Equalizer Reset (APD)` | Botón pulsador | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| `Themes` (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente aloja la sección de Colores de Slice. |
| `Use Aether defaults / Custom colors` | Botón de opción | Cambia el esquema de color de las slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| `Botones de color Slice A–H` | Botón pulsador | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles de inmediato en los widgets VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones se deshabilitan cuando se selecciona `Use Aether defaults`. Hasta 8 slices (`kSliceColorCount`). |
| `Reset All to Defaults (Themes)` | Botón pulsador | Restablece todos los colores personalizados de las slices a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

A partir de v0.9.3, el flujo de trabajo de actualización de firmware ya no descarga archivos de instalación automáticamente. Cuando `Check for Update` encuentra una versión más reciente, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego use `Select Installer...` para prepararlo localmente. El botón antes etiquetado como `Browse .ssdr...` ahora está etiquetado como `Select Installer...` y acepta archivos `.msi`, `.exe` y `.ssdr`.

### Cómo actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo de Configuración del Radio.
2. Haga clic en la pestaña `Radio`.
3. Haga clic en `Check for Update`. AetherSDR contacta al servidor de actualizaciones de FlexRadio e informa la última versión disponible en la etiqueta de estado.
4. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en `Select Installer...` y elija el archivo `.msi`, `.exe` o `.ssdr` preextraído descargado. AetherSDR detecta automáticamente el formato y extrae el firmware. La etiqueta de estado muestra el progreso de la preparación.
6. Cuando la preparación se complete, haga clic en `Upload Firmware`. Una barra de progreso y una etiqueta de estado rastrean la carga.

## Calibración de frecuencia (pestaña RX)

A partir de v0.9.2.1, los controles de calibración de frecuencia en la pestaña RX siempre están visibles, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (en verde). Cuando no hay un GPSDO presente, la etiqueta muestra "Manual frequency offset calibration available." (en ámbar). En versiones anteriores, los controles de calibración estaban ocultos cuando se detectaba un GPSDO.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| `Cal Frequency (MHz):` | Campo de texto | Frecuencia utilizada para la calibración manual. Ingrese la frecuencia exacta de su señal de referencia en MHz. |
| `Start` | Botón pulsador | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0 y luego inicia el barrido de calibración. El botón se deshabilita y muestra "Busy" mientras la calibración está en progreso. Una etiqueta de estado junto al botón muestra el estado actual (Starting…, texto de progreso o resultado). El campo no debe estar vacío; si lo está, la etiqueta de estado le solicita que ingrese una frecuencia antes de continuar. |
| `Freq Offset (ppb):` | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones. Ajústelo si necesita aplicar un desplazamiento conocido sin ejecutar el barrido de calibración automatizado. |

### Cómo ejecutar un barrido de calibración

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo de Configuración del Radio.
2. Haga clic en la pestaña `RX`.
3. Ingrese la frecuencia exacta de su señal de referencia en el campo `Cal Frequency (MHz):`.
4. Haga clic en `Start`. El botón se deshabilita y muestra "Busy". Observe la etiqueta de estado para ver el progreso.
5. Cuando el barrido finalice, la etiqueta de estado informa el resultado y el botón `Start` se vuelve a habilitar.

## Comportamiento del cuadro combinado de fuente de oscilador (v0.9.7)

En v0.9.7, el cuadro combinado `10 MHz Reference Source:` se completa dinámicamente según el estado en vivo que informa el radio, en lugar de basarse únicamente en los indicadores de presencia de hardware detectados al abrir el diálogo. Se aplican las siguientes reglas:

- `Auto` siempre está presente.
- `TCXO` aparece si el radio tiene un TCXO instalado, o si el radio está informando actualmente TCXO como su estado de oscilador, o si TCXO fue seleccionado previamente.
- `GPSDO` aparece si hay un GPSDO instalado, o si el radio está informando actualmente GPSDO como su estado de oscilador, o si GPSDO fue seleccionado previamente.
- `External 10 MHz` aparece si se detecta actualmente una referencia externa, o si el radio la informa como el estado activo, o si fue seleccionada previamente. La etiqueta era `External` en versiones anteriores a v0.9.7.

Cuando el cuadro combinado se abre antes de que el radio haya informado el estado del oscilador, se retienen todas las opciones que coinciden con la configuración actual o un valor seleccionado previamente para que no se pierda ninguna selección.

La etiqueta de estado de bloqueo a la derecha del cuadro combinado también gana detalles adicionales en v0.9.7:

- Cuando `Auto` es la configuración establecida, la etiqueta muestra `Auto -> <fuente resuelta>` para hacer visible la elección real del radio.
- Cuando la configuración y el estado activo difieren (por ejemplo, durante una transición de fuente), la etiqueta muestra `<configurado> -> <activo>`.
- Si se selecciona `External 10 MHz` pero el radio informa que no hay señal externa presente, la etiqueta agrega `(not detected)`.
- Antes de que el radio haya enviado cualquier estado del oscilador, la
