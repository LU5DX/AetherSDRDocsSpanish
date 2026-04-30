# Habilitar grabación automática en TX y seleccionar una carpeta de guardado

Cuando la grabación automática en TX está habilitada, AetherSDR comienza a grabar audio automáticamente cada vez que transmite y se detiene después de un tiempo de inactividad configurable. Esta página explica cómo activar esa función y elegir dónde se guardan las grabaciones.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Decida si desea grabación del lado de la radio o del lado del cliente, ya que esto afecta dónde se captura el audio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio. La selección activa está resaltada. Esta opción se guarda en `RecordingMode`.
4. En el campo **Save to:**, escriba la ruta completa a su carpeta de grabaciones o haga clic en **...** para examinar una carpeta. La ruta se guarda en `QsoRecordingDir`.
5. Marque la casilla **Auto-record on TX**. Esto habilita la grabación automática cada vez que la radio pasa a transmisión. La configuración se guarda en `QsoRecordingAutoRecord`.
6. Establezca **Idle timeout:** al número de segundos de silencio después de los cuales se detiene la grabación. El valor se guarda en `QsoRecordingIdleTimeout`.
7. Cierre el diálogo. Las configuraciones toman efecto inmediatamente.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado |
|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en la radio o en esta PC. | Radio Side |
| **Save to:** | Ruta de carpeta donde se escriben los archivos de grabación. Por defecto Documents/AetherSDR/Recordings. | — |
| **...** | Abre un explorador de carpetas para seleccionar la ubicación de guardado. | — |
| **Auto-record on TX** | Cuando se marca, la grabación comienza automáticamente en cada transmisión y se detiene después de que transcurre el tiempo de inactividad. | Sin marcar |
| **Idle timeout:** | Segundos de silencio antes de que se detenga la grabación después de que termina TX. | 120 s |
| **TX Follows Active Slice** | TX sigue la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. | Desactivado |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | Desactivado |
| **Deslizadores de agudeza de filtro Voice / CW / Digital** | Establece la agudeza del filtro (0=latencia más baja a 3=más agudo) por modo. El deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática de nivel de filtro para ese modo y deshabilita el deslizador de agudeza manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Se requiere para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en firmware 4.2. El TGXL controla PTT de radio a través de su cable de bloqueo de hardware; no se necesita encendido del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. | Connect |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo .ssdr firmware preextraído. El gestor de firmware detecta automáticamente el formato de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador externo de Predistorsión Adaptativa — selección por antenna TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **Combos muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de retroalimentación que la radio usa para muestrear la RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando conduzca un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color de slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter e insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — |

## Actualización de firmware (pestaña Radio)

La pestaña **Radio** incluye controles de actualización de firmware. En v0.9.3 el flujo de trabajo para preparar un archivo de firmware cambió.

### Verificar actualizaciones

1. Haga clic en la pestaña **Radio** en Radio Setup.
2. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
3. Si hay una actualización disponible, la etiqueta de estado muestra la versión disponible e instruye descargar el instalador SmartSDR de flexradio.com, luego use **Select Installer...** para prepararlo.
4. Si el firmware es actual, la etiqueta de estado confirma la versión instalada.

> **Nota:** En v0.9.3 se eliminó el botón de descarga de un clic. Debe descargar el instalador SmartSDR de flexradio.com usted mismo, luego prepararlo usando **Select Installer...**.

### Preparar y cargar firmware

1. Descargue el instalador SmartSDR de flexradio.com. Los tipos de archivo admitidos son .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo) o un archivo .ssdr firmware preextraído.
2. Haga clic en **Select Installer...**. Se abre un selector de archivos filtrado para esos tipos de archivo.
3. Seleccione el archivo descargado. AetherSDR detecta automáticamente el formato y extrae el .ssdr sin herramientas externas. Una barra de progreso y etiqueta de estado muestran el progreso de extracción.
4. Cuando la preparación se completa correctamente, haga clic en **Upload Firmware** para transferir el firmware a la radio.

### Controles de actualización de firmware

| Control | Qué hace |
|---|---|
| **Check for Update** | Consulta el servidor de actualizaciones de FlexRadio e informa si hay una versión de firmware más nueva disponible. |
| **Select Installer...** | Abre un selector de archivos que acepta archivos .msi, .exe o .ssdr. El gestor detecta automáticamente el formato y extrae el .ssdr. Cambiado de **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Transfiere el firmware preparado a la radio. Una barra de progreso y etiqueta de estado rastrean la carga. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de compensación de frecuencia y selección de fuente de referencia de 10 MHz.

En v0.9.2.1 los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." (verde). Sin un GPSDO la etiqueta lee "Manual frequency offset calibration available." (ámbar).

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<value>` cuando termina de editar el campo. |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración. Una etiqueta de estado junto al botón reporta el progreso. |
| **Freq Offset (ppb):** | Compensación manual de frecuencia en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. Un indicador de estado de bloqueo en vivo (Locked / Unlocked) aparece junto al selector. |

### Iniciar una calibración

1. Haga clic en la pestaña **RX** en Radio Setup.
2. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para el progreso y resultado.
4. Cuando la calibración se completa, el botón se vuelve a habilitar y la etiqueta de estado muestra el resultado.

> **Nota:** Dejar **Cal Frequency (MHz):** vacío y hacer clic en **Start** mostrará una advertencia ("Enter cal frequency") y no iniciará la calibración.

## Consejos

- Si usa SmartLink o una VPN, considere si **Radio Side** o **Client Side** coincide mejor con dónde desea almacenar los archivos. Las grabaciones del lado de la radio permanecen en el FLEX-8600; las grabaciones del lado del cliente van a la carpeta establecida en **Save to:**.
- Establezca **Idle timeout:** a un valor bajo (unos pocos segundos) si desea que cada transmisión se capture como un archivo separado. Un valor más alto fusiona pausas dentro de un QSO en un archivo.
- Al preparar firmware, los instaladores .msi y .exe se aceptan directamente — no necesita extraer el archivo .ssdr manualmente.

## Solución de problemas

- **No aparecen archivos en la carpeta de guardado después de transmitir** — Confirme que **Auto-record on TX** esté marcado y que la ruta en **Save to:** exista y sea escribible. Si la carpeta no existe, AetherSDR no puede crear el archivo.
- **El campo Save to: no muestra ruta** — Haga clic en **...** y seleccione una carpeta explícitamente. Dejar el campo vacío puede impedir que la grabación comience.
- **El botón Start permanece deshabilitado después de hacer clic** — Verifique que **Cal Frequency (MHz):** contenga un valor de frecuencia válido. El botón se vuelve a habilitar automáticamente cuando la calibración termina o falla.
- **El botón Upload Firmware está deshabilitado después de hacer clic en Select Installer...** — El gestor aún está extrayendo el .ssdr del instalador. Espere a que la barra de progreso se complete y la etiqueta de estado confirme que el firmware está listo, luego haga clic en **Upload Firmware**.
- **La pestaña APD no es visible** — La pestaña APD solo aparece en radios de serie FLEX-8x00 que ejecutan firmware SmartSDR 4.2.18 o posterior. Si la pestaña está ausente, su modelo de radio o versión de firmware no admite APD configurable.

## Relacionado

- [Choose PC input/output audio devices](choose-pc-input-output-audio-devices.md)
- [Turn on audio boost or enlarge the audio buffer for remote operation](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Pick Opus vs](pick-opus-vs)
