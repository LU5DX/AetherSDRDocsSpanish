# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo seleccionar un reloj de referencia externo de 10 MHz en un FLEX-8600 conectado. Use una referencia externa cuando disponga de un oscilador disciplinado por GPS u otra fuente de precisión de 10 MHz y desee que el radio se sincronice con ella en lugar de con su oscilador interno.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El diálogo Radio Setup requiere una conexión activa con el radio.
- La señal de referencia externa de 10 MHz debe estar conectada al puerto REF IN del panel trasero del FLEX-8600 antes de cambiar la fuente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Localice el combo box `10 MHz Reference Source:`.
4. Seleccione `External` en el combo box. Para volver al oscilador interno, seleccione `Internal`.

## Qué hace cada control

| Control | Tipo | Rango válido / Comportamiento |
|---|---|---|
| `10 MHz Reference Source:` | Combo box | `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. El estado de sincronización (Locked / Unlocked) se muestra junto al combo box y se actualiza en tiempo real. |
| `TX Follows Active Slice` | Push button | La transmisión sigue al slice activo. Es mutuamente excluyente con `Active Slice Follows TX`. Se deshabilita automáticamente durante la operación en Split. |
| `Active Slice Follows TX` | Push button | Cambia el slice activo cuando la transmisión se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con `TX Follows Active Slice`. |
| `Voice / CW / Digital filter sharpness sliders` | Slider (0–3) | Establece la nitidez del filtro (0=menor latencia, 3=máxima nitidez) por modo; el slider se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| `Auto (Voice / CW / Digital)` | Toggle button | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el slider manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| `Connect / Disconnect (TGXL)` | Push button | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Al conectar, guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del radio que dejó de funcionar en el firmware 4.2. Si el campo de IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| `Connect / Disconnect (PGXL)` | Push button | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| `Connect / Disconnect (Antenna Genius)` | Push button | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado "Connected" cuando el dispositivo conectado es un ShackSwitch (en lugar de un Antenna Genius estándar). |
| `Connect / Disconnect (ShackSwitch)` | Push button | Abre o cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de difusión AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado "Connected" si el dispositivo conectado es un Antenna Genius (no ShackSwitch). |
| `⚙ Web UI (ShackSwitch)` | Push button | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` del beacon si es > 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| `Select Installer...` | Push button | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta era `Browse .ssdr...` antes de la v0.9.3. |
| `APD` (pestaña) | Pestaña | Configuración del muestreador externo de Adaptive Pre-Distortion: selección por antena TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que el radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ la expone; los radios de la serie 6000 y los anteriores a 4.2.18 mantienen la pestaña invisible. |
| `ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)` | Combo box | Selecciona la ruta de retroalimentación que usa el radio para muestrear la RF saliente en el entrenamiento APD para esa antena TX. El valor predeterminado es `INTERNAL`. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se obtienen en tiempo real del subobjeto `apd sampler` del radio. Vuelve a `INTERNAL` si el radio informa un valor no reconocido. |
| `Equalizer Reset (APD)` | Push button | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| `Themes` (pestaña) | Pestaña | Pestaña de personalización de la interfaz; actualmente aloja la sección Slice Colors. |
| `Use Aether defaults / Custom colors` | Radio button | Cambia el esquema de colores de los slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| `Slice A–H color buttons` | Push button | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones están deshabilitados cuando se selecciona `Use Aether defaults`. Hasta 8 slices (`kSliceColorCount`). |
| `Reset All to Defaults (Themes)` | Push button | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

A partir de la v0.9.3, el proceso de actualización de firmware ya no descarga los archivos del instalador automáticamente. Cuando `Check for Update` detecta una versión más reciente, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego use `Select Installer...` para prepararlo localmente. El botón anteriormente etiquetado como `Browse .ssdr...` ahora se llama `Select Installer...` y acepta archivos `.msi`, `.exe` y `.ssdr`.

### Cómo actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `Radio`.
3. Haga clic en `Check for Update`. AetherSDR contacta el servidor de actualizaciones de FlexRadio e informa la última versión disponible en la etiqueta de estado.
4. Si hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en `Select Installer...` y elija el archivo `.msi`, `.exe` o `.ssdr` ya extraído que descargó. AetherSDR detecta el formato automáticamente y extrae el firmware. La etiqueta de estado muestra el progreso de la preparación.
6. Cuando la preparación finalice, haga clic en `Upload Firmware`. Una barra de progreso y la etiqueta de estado muestran el avance de la carga.

## Calibración de frecuencia (pestaña RX)

A partir de la v0.9.2.1, los controles de calibración de frecuencia en la pestaña RX son siempre visibles, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado dice "GPSDO installed. Manual frequency offset calibration available." (en verde). Cuando no hay GPSDO, la etiqueta dice "Manual frequency offset calibration available." (en ámbar). En versiones anteriores, los controles de calibración se ocultaban cuando se detectaba un GPSDO.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| `Cal Frequency (MHz):` | Campo de texto | Frecuencia utilizada para la calibración manual. Ingrese la frecuencia exacta de su señal de referencia en MHz. |
| `Start` | Push button | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0 y luego inicia el barrido de calibración. El botón se deshabilita y muestra "Busy" mientras la calibración está en curso. Una etiqueta de estado junto al botón muestra el estado actual (Starting…, texto de progreso o resultado). El campo no debe estar vacío; si lo está, la etiqueta de estado le indica que ingrese una frecuencia antes de continuar. |
| `Freq Offset (ppb):` | Spinbox | Desplazamiento manual de frecuencia en partes por mil millones. Ajústelo si necesita aplicar un desplazamiento conocido sin ejecutar el barrido de calibración automatizado. |

### Cómo ejecutar un barrido de calibración

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Ingrese la frecuencia exacta de su señal de referencia en el campo `Cal Frequency (MHz):`.
4. Haga clic en `Start`. El botón se deshabilita y muestra "Busy". Observe la etiqueta de estado para ver el progreso.
5. Cuando el barrido finalice, la etiqueta de estado informa el resultado y el botón `Start` se vuelve a habilitar.

## Interfaz web del ShackSwitch

La v0.9.4 añade el botón `⚙ Web UI` a la fila del ShackSwitch en la pestaña Peripherals. Haga clic en él para abrir la interfaz de configuración web integrada del ShackSwitch en el navegador del sistema.

El botón determina la URL de la siguiente manera:

1. Si el ShackSwitch está conectado actualmente y su beacon de descubrimiento anuncia un `webPort` mayor que 1024, se usa ese puerto.
2. De lo contrario, se usa el valor almacenado en `SS_WebPort`.
3. Si ninguna de las dos fuentes proporciona un puerto válido, se usa el puerto 5000.

La dirección IP se obtiene de `SS_ManualIp`. Si esa configuración está vacía y hay un ShackSwitch conectado actualmente, se usa la dirección del par activo. El botón no hace nada si no se puede determinar ninguna dirección IP.

### Cómo abrir la interfaz web del ShackSwitch

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `Peripherals`.
3. Confirme que la fila del ShackSwitch muestra "Connected", o ingrese la IP del dispositivo y haga clic en `Connect (ShackSwitch)`.
4. Haga clic en `⚙ Web UI`. La página de configuración del ShackSwitch se abre en su navegador predeterminado.

## Consejos

- La pestaña `RX` también contiene el combo box `10 MHz Reference Source:`. Si está usando un oscilador disciplinado por GPS, cambie la fuente de referencia a `GPSDO` o `External` según corresponda antes de ejecutar la calibración.
- Si el campo `Cal Frequency (MHz):` está vacío cuando hace clic en `Start`, la etiqueta de estado le pedirá que ingrese una frecuencia. En ese caso no se envía ningún comando al radio.
- Las filas del Antenna Genius y del ShackSwitch en la pestaña Peripherals comparten la misma conexión subyacente. Conectar uno desconecta al otro. La fila del tipo de dispositivo que no está conectado actualmente se oculta del estado "Connected" automáticamente.

## Solución de problemas

- **La frecuencia del radio parece inestable o desplazada después de cambiar a External** — La señal en REF IN puede estar ausente, tener un nivel demasiado bajo o no ser exactamente 10 MHz. Verifique que la fuente externa esté en funcionamiento y correctamente conectada antes de seleccionar `External`. Vuelva a `Internal` mientras diagnostica el problema.
- **El botón Start permanece deshabilitado o muestra "Busy" indefinidamente** — Esto puede ocurrir si el radio no responde al comando `radio pll_start`. Desconéctese y vuelva a conectarse al radio, luego inténtelo de nuevo.
- **`Select Installer...` muestra un error de preparación** — Asegúrese de que el archivo sea un instalador genuino de SmartSDR o un archivo `.ssdr` y que no haya sido corrompido durante la descarga. Descárguelo nuevamente desde flexradio.com.
