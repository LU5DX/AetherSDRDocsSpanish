# Habilitar la grabación automática en TX y elegir una carpeta de guardado

Cuando la grabación automática en TX está activada, AetherSDR comienza a grabar audio automáticamente cada vez que transmite y se detiene tras un tiempo de inactividad configurable. Esta página explica cómo activar esa función y elegir dónde se guardan las grabaciones.

## Antes de comenzar

- La radio debe estar conectada. Configuración de radio requiere una conexión de radio activa.
- Decida si desea grabación del lado de la radio o del lado del cliente, ya que esto afecta dónde se captura el audio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio. La selección activa se resalta. Esta elección se guarda en `RecordingMode`.
4. En el campo **Save to:**, escriba la ruta completa a su carpeta de grabaciones, o haga clic en **...** para buscar una carpeta. La ruta se guarda en `QsoRecordingDir`.
5. Marque la casilla **Auto-record on TX**. Esto habilita la grabación automática cada vez que la radio cambia a transmitir. La configuración se guarda en `QsoRecordingAutoRecord`.
6. Establezca **Idle timeout:** en el número de segundos de silencio tras los cuales se detiene la grabación. El valor se guarda en `QsoRecordingIdleTimeout`.
7. Cierre el diálogo. Los ajustes surten efecto inmediatamente.

## Qué hace cada control

| Control | Qué hace | Por defecto |
|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en la radio o en este PC. | Radio Side |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. Por defecto es Documents/AetherSDR/Recordings. | — |
| **...** | Abre un explorador de carpetas para seleccionar la ubicación de guardado. | — |
| **Auto-record on TX** | Cuando está marcado, la grabación comienza automáticamente en cada transmisión y se detiene tras el tiempo de inactividad configurado. | Sin marcar |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga después de terminar la TX. | 120 s |
| **TX Follows Active Slice** | TX sigue a la franja activa. Excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante operación en Split. | Off |
| **Active Slice Follows TX** | Cambia la franja activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Excluyente con **TX Follows Active Slice**. | Off |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0=mínima latencia a 3=máxima nitidez) por modo. El control deslizante se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL maneja PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita manipulación de PTT del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado Connected solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. | Connect |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de difusión de AG. El autodescubrimiento mediante UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es Antenna Genius (no ShackSwitch). | Connect |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el webPort de la baliza si es > 1024; de lo contrario, usa `SS_WebPort` o el puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El gestor de preparación detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador de Predistorsión Adaptativa Externa: selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. | — |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de realimentación que la radio usa para muestrear la RF de salida para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz de usuario: actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores de las franjas entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por franja. | Use Aether defaults |
| **Botones de color de franja A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa franja. Los cambios son visibles inmediatamente en los widgets de VFO, superposiciones del panadapter y etiquetas de canal CAT. Los botones están deshabilitados cuando **Use Aether defaults** está seleccionado. Hasta 8 franjas. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de las franjas a la paleta incorporada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles de actualización de firmware. En v0.9.3 el flujo de trabajo para preparar un archivo de firmware cambió.

### Verificar actualizaciones

1. Haga clic en la pestaña **Radio** en Radio Setup.
2. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
3. Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e indica que debe descargar el instalador de SmartSDR desde flexradio.com y luego usar **Select Installer...** para prepararlo.
4. Si el firmware está actualizado, la etiqueta de estado confirma la versión instalada.

> **Nota:** En v0.9.3 se eliminó el botón de descarga con un solo clic. Debe descargar el instalador de SmartSDR desde flexradio.com usted mismo y luego prepararlo usando **Select Installer...**.

### Preparar y cargar firmware

1. Descargue el instalador de SmartSDR desde flexradio.com. Los tipos de archivo compatibles son .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos filtrado para esos tipos de archivo.
3. Seleccione el archivo descargado. AetherSDR detecta automáticamente el formato y extrae el .ssdr sin herramientas externas. Una barra de progreso y una etiqueta de estado muestran el progreso de la extracción.
4. Cuando la preparación se complete con éxito, haga clic en **Upload Firmware** para transferir el firmware a la radio.

### Controles de actualización de firmware

| Control | Qué hace |
|---|---|
| **Check for Update** | Consulta el servidor de actualizaciones de FlexRadio e informa si hay una versión de firmware más reciente disponible. |
| **Select Installer...** | Abre un selector de archivos que acepta archivos .msi, .exe o .ssdr. El gestor de preparación detecta automáticamente el formato y extrae el .ssdr. Cambió de **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Transfiere el firmware preparado a la radio. Una barra de progreso y una etiqueta de estado siguen la carga. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de desviación de frecuencia y selección de la fuente de referencia de 10 MHz.

En v0.9.2.1 los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (verde). Sin GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (ámbar).

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<value>` cuando termina de editar el campo. |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración se ejecuta. Una etiqueta de estado junto al botón informa el progreso. |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External 10 MHz. Las opciones mostradas dependen del hardware instalado y del estado del oscilador informado por la radio. Aparece un indicador de estado de bloqueo en vivo junto al selector que muestra la fuente activa y el estado de bloqueo (ver más abajo). |

### Indicador de fuente de referencia de 10 MHz

En v0.9.7 la etiqueta de estado de bloqueo junto a **10 MHz Reference Source:** se actualizó para mostrar información más rica. El texto y el color de la etiqueta se actualizan en vivo a medida que la radio informa cambios en el estado del oscilador.

**Formato del texto de la etiqueta:**

| Condición | Texto de ejemplo |
|---|---|
| Modo Auto resolviendo a una fuente | `Auto -> GPSDO Locked` |
| Configuración anulada por la radio | `TCXO -> GPSDO Locked` |
| Fuente coincide con la configuración | `GPSDO Locked` |
| External seleccionado pero no detectado | `External 10 MHz Unlocked (not detected)` |
| Esperando el primer informe de estado | `Waiting for oscillator status` |

**Color de la etiqueta:**

| Estado | Color |
|---|---|
| Bloqueado | Verde |
| Desbloqueado | Rojo |
| Aún no se ha recibido estado | Gris/azul |

El cuadro combinado **10 MHz Reference Source:** también se llena de forma más dinámica en v0.9.7. Las opciones se agregan según el hardware que la radio informa como presente, la configuración actual y el estado activo del oscilador. La entrada **External** está etiquetada como **External 10 MHz** (anteriormente **External**). Si la radio envía el valor `ext`, se trata como equivalente a `external`.

### Iniciar una calibración

1. Haga clic en la pestaña **RX** en Radio Setup.
2. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para ver el progreso y el resultado.
4. Cuando la calibración se completa, el botón se vuelve a habilitar.
