# Cargar un Nuevo Archivo de Firmware en la Radio

Esta página explica cómo cargar una imagen de firmware en su FLEX-8600 usando el diálogo Configuración de Radio. Realizaría esto para actualizar la radio a una versión específica de firmware sin utilizar la comprobación automática de actualizaciones.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Radio (Radio) no se completará correctamente sin una conexión activa.
- Descargue el instalador de SmartSDR desde flexradio.com y anote dónde se guarda en su computadora. AetherSDR acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Select Installer...** para abrir un selector de archivos.
4. Navegue hasta el instalador o archivo de firmware en su computadora, selecciónelo y confirme. AetherSDR detecta automáticamente el formato desde el encabezado del archivo y extrae el `.ssdr` si es necesario. Aparece un mensaje de estado mientras se prepara el firmware.
5. Cuando el estado indique que el firmware está listo, haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga está completa antes de hacer cualquier otra cosa.
7. Reinicie la radio según lo indicado en las notas de la versión del firmware para aplicar el nuevo firmware.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Si se encuentra una actualización, el área de estado muestra la versión disponible y le indica que descargue el instalador de SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo. |
| **Select Installer...** | Botón | Abre un diálogo de archivos que acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs MZ PE/COFF) y extrae el `.ssdr` sin herramientas externas. Se muestra un mensaje de estado mientras se prepara el archivo. Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Botón | Inicia la carga usando el archivo preparado por **Select Installer...**. Aparecen una barra de progreso y texto de estado debajo y se actualizan a medida que avanza la transferencia. |
| TX Follows Active Slice | Botón | TX sigue al segmento activo. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia el segmento activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Deslizadores de nitidez de filtro Voice / CW / Digital | Deslizador | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Conmutador | Activa la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio que está rota en firmware 4.2. El TGXL acciona el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita señalización del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra un estado Conectado solo cuando el dispositivo conectado es un Antenna Genius genuino (no un ShackSwitch). |
| Connect / Disconnect (ShackSwitch) | Botón | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo UDP/TCP de AG en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión de AG. El descubrimiento automático a través de UDP también funciona sin esta fila. Fila oculta del estado Conectado si Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| APD (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa: selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando conduzca un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario: actualmente alberga la sección Colores de Segmento. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de color del segmento entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por segmento. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de segmento A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese segmento. Los cambios son visibles inmediatamente en los widgets de VFO, superposiciones de panadapter e insignias de canal CAT. Los botones están deshabilitados cuando está seleccionado **Use Aether defaults**. Hasta 8 segmentos. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores personalizados de los segmentos a la paleta integrada de AetherSDR. |

## Calibración de frecuencia (pestaña RX)

La pestaña RX muestra controles de calibración independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior de la pestaña cambia la redacción y el color dependiendo del hardware presente:

- **GPSDO instalado** — la etiqueta dice "GPSDO installed. Manual frequency offset calibration available." en verde. Aún puede ejecutar una calibración manual si es necesario.
- **Sin GPSDO** — la etiqueta dice "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** están siempre visibles y activos. Antes de v0.9.2.1, los controles de calibración estaban ocultos cuando se detectaba un GPSDO.

### Uso del botón Start

El botón **Start** ahora proporciona retroalimentación de estado en línea directamente en la pestaña RX en lugar de depender únicamente de la respuesta de la radio. Cuando hace clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz)** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no continúa.
2. El texto del botón cambia a **Busy** y el botón se deshabilita hasta que se complete la secuencia de comandos de calibración.
3. AetherSDR envía `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0` para restablecer cualquier compensación anterior, luego emite `radio pll_start` para comenzar el barrido de calibración.
4. La etiqueta de estado en línea junto al botón se actualiza a medida que avanza la calibración.
5. Cuando la secuencia finaliza (o falla), el botón se vuelve a habilitar y vuelve a **Start**.

La actividad de calibración se registra en el registro de protocolo a nivel de depuración, incluido el valor de la frecuencia de calibración, el restablecimiento de ppb y un identificador de ejecución interno que ayuda a correlacionar las entradas del registro cuando se realizan múltiples intentos de calibración en la misma sesión.

### Controles de frecuencia de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Campo | Ingrese la frecuencia de referencia conocida en MHz (seis decimales). Se envía como `radio set cal_freq=<value>` cuando sale del campo o hace clic en **Start**. |
| **Start** | Botón | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Deshabilitado y etiquetado como **Busy** mientras se ejecuta un barrido. |
| **Freq Offset (ppb)** | Cuadro de número | Compensación de frecuencia manual en partes por billón. Ajuste después de la calibración si se necesita un ajuste fino. |

### Fuente de Referencia de 10 MHz

El cuadro combinado **10 MHz Reference Source:** selecciona la referencia del oscilador utilizada por la radio. En v0.9.7, el combinado y su etiqueta de estado se actualizaron con el siguiente comportamiento:

- El combinado se completa dinámicamente según el hardware reportado por la radio. **Auto** siempre está presente. **TCXO** aparece cuando la radio reporta `tcxoPresent` o cuando la configuración actual o el estado activo es TCXO. **GPSDO** aparece cuando se reporta `gpsdoPresent` o la configuración actual o el estado es GPSDO. **External 10 MHz** aparece cuando se reporta `extPresent`, cuando se ha recibido el estado del oscilador de la radio, o cuando la configuración actual o el estado es External.
- El valor `ext` reportado por la radio se normaliza internamente a `external` antes de mostrarlo, por lo que el combinado siempre muestra **External 10 MHz** en lugar de una cadena `ext` sin procesar.
- La etiqueta de estado junto al combinado refleja tanto la configuración establecida como el estado activo del oscilador de la radio:
  - Cuando **Auto** está seleccionado y la radio se ha resuelto a una fuente específica, la etiqueta dice, por ejemplo, `Auto -> GPSDO`.
  - Cuando se selecciona una fuente específica pero la radio está usando activamente una diferente, la etiqueta dice, por ejemplo, `TCXO -> GPSDO`.
  - De lo contrario, la etiqueta muestra solo el nombre de la fuente activa.
  - La etiqueta agrega **Locked** (verde) o **Unlocked** (rojo) para reflejar el estado de bloqueo. Si la fuente activa es External y la radio reporta que no hay señal externa presente, la etiqueta también agrega **(not detected)**.
  - Mientras la radio no haya reportado el estado del oscilador, la etiqueta muestra `Waiting for oscillator status` en azul grisáceo.

| Control | Tipo | Comportamiento |
|---|---|---|
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Las opciones mostradas dependen del hardware instalado y del estado en vivo de la radio. Envía `radio oscillator <value>` cuando se cambia. Valores válidos: `auto`, `tcxo`, `gpsdo`, `external`. |
| Indicador de estado del oscilador | Indicador | Muestra la fuente resuelta, el estado de bloqueo y (para External) si se detecta una señal. Se actualiza en vivo a medida que la radio reporta cambios. |

## Consejos

- Si solo desea verificar si existe una versión más reciente en lugar de cargar un archivo específico, use **Check for Update** primero. El área de estado le indicará la versión disponible y lo dirigirá a descargar el instalador desde flexradio.com.
- **Select Installer...** acepta archivos `.msi`, `.exe` y `.ssdr`. No necesita extraer nada.
