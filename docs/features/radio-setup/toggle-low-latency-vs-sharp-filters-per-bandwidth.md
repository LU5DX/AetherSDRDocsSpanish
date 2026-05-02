# Alternar filtros de baja latencia o filtros selectivos por ancho de banda

La pestaña Filters en Radio Setup permite elegir entre filtros DSP de baja latencia y filtros selectivos para cada ancho de banda de recepción, y opcionalmente forzar filtros de baja latencia al usar modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Filters solo está disponible cuando hay una conexión de radio activa.
- Abra Radio Setup desde `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros para el ancho de banda actual. El botón refleja la selección activa.
4. Para forzar filtros de baja latencia siempre que un modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.
5. Cierre el cuadro de diálogo. Los ajustes surten efecto inmediatamente.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre baja latencia y filtros selectivos para el ancho de banda seleccionado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, anula la elección de filtro por ancho de banda y usa filtros de baja latencia siempre que un slice DIGU o DIGL esté activo. |
| Controles deslizantes de selectividad de filtro para Voice / CW / Digital | Control deslizante | Establece la selectividad del filtro (0=menor latencia a 3=mayor selectividad) por modo. El control se deshabilita cuando Auto está activado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de selectividad manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| TX Follows Active Slice | Botón de acción | TX sigue al slice activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón de acción | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. |
| Connect / Disconnect (TGXL) | Botón de acción | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecta automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en el firmware 4.2. El TGXL controla el PTT del radio a través de su cable de enclavamiento de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. |
| Connect / Disconnect (PGXL) | Botón de acción | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón de acción | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si el dispositivo conectado es un ShackSwitch (en lugar de un Antenna Genius). |
| Connect / Disconnect (ShackSwitch) | Botón de acción | Abre o cierra una conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo ShackSwitch en el beacon de difusión AG. El descubrimiento automático por UDP también funciona sin introducir una dirección manualmente. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (no ShackSwitch). |
| ⚙ Web UI (ShackSwitch) | Botón de acción | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| Select Installer... | Botón de acción | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic frente a PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado indica que debe descargar el instalador de SmartSDR desde flexradio.com y luego hacer clic en este botón para prepararlo. La etiqueta cambió de **Browse .ssdr...** en la versión v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador externo de predistorsión adaptativa (APD): selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña se oculta a menos que el radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esta función; los radios de la serie 6000 y los anteriores a 4.2.18 mantienen la pestaña invisible. |
| Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que usa el radio para muestrear la RF de salida en el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando conecte un amplificador lineal externo. Las opciones se obtienen en tiempo real del sub-objeto `apd sampler` del radio. Si el radio informa un valor no reconocido, vuelve a INTERNAL. |
| Equalizer Reset (APD) | Botón de acción | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz; actualmente incluye la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de Slice A–H | Botón de acción | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón de acción | Restablece todos los colores personalizados de slice a la paleta integrada de AetherSDR. |

## Flujo de trabajo de actualización de firmware (v0.9.3)

A partir de la versión v0.9.3, el flujo de actualización de firmware ya no descarga el instalador automáticamente. Cuando **Check for Update** encuentra una versión más reciente, el área de estado le indica que descargue usted mismo el instalador de SmartSDR desde flexradio.com. Use **Select Installer...** para indicarle a AetherSDR la ubicación del archivo descargado.

### Formatos de instalador compatibles

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador WiX de FlexRadio (SmartSDR v4.2 y posteriores). Recomendado. |
| `.exe` | Instalador autoextraíble más antiguo (versiones anteriores a v4.2). |
| `.ssdr` | Archivo de firmware ya extraído. |

El preparador lee los primeros 8 bytes del archivo para identificar el formato (OLE/MSI magic o encabezado PE/COFF MZ) y extrae el contenido `.ssdr` sin requerir ninguna herramienta externa.

### Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión e indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en **Select Installer...** y localice el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR prepara el firmware e informa el progreso en el área de estado.
6. Cuando la preparación finalice, haga clic en **Upload Firmware** para transferir el firmware al radio.

## Calibración de frecuencia (pestaña RX)

En la versión v0.9.2.1, los controles de calibración de frecuencia en la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles Cal Frequency y Start se ocultaban cuando se detectaba un GPSDO.

- Cuando hay un GPSDO instalado, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." en verde.
- Cuando no hay GPSDO instalado, la etiqueta de estado muestra "Manual frequency offset calibration available." en ámbar.

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia precisa y conocida en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), establece la frecuencia de calibración e inicia el barrido de calibración PLL. El campo de estado junto al botón Start se actualiza a medida que avanza la calibración.
5. Mientras la calibración está en curso, el botón **Start** se deshabilita y muestra "Busy". Se vuelve a habilitar cuando la calibración finaliza o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario una vez que la calibración haya concluido.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Cuadro de número | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Botón de acción | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración PLL. Se deshabilita y muestra "Busy" mientras hay una calibración en curso. |
| **Freq Offset (ppb)** | Cuadro de número | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en tiempo real. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento, lo que beneficia la decodificación de modos digitales en tiempo real y el CW. Los filtros selectivos proporcionan una mayor selectividad de flancos, lo que resulta más útil en condiciones de banda SSB congestionada.
- La casilla **Use Low Latency Filters for Digital Modes** se aplica a todos los anchos de banda, por lo que no es necesario cambiar el ajuste por ancho de banda cada vez que cambie a un modo digital.
- Si **Start** no se activa después de introducir una frecuencia de calibración, verifique que el campo Cal Frequency no esté vacío.
- Cuando **Check for Update** informa una actualización disponible, AetherSDR ya no descarga el instalador por usted. Descargue el instalador de SmartSDR desde flexradio.com y luego use **Select Installer...** para prepararlo.
- Para abrir la interfaz web del ShackSwitch directamente desde AetherSDR, haga clic en **⚙ Web UI** en la pestaña Peripherals. AetherSDR usa la IP de `SS_ManualIp` o la conexión activa, y el puerto del campo `webPort` del beacon (si es mayor que 1024), `SS_WebPort` o el puerto 5000 como valor de reserva.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Seleccionar el modo iámbico A o B para el manipulador del radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)
