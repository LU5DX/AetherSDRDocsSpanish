# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo seleccionar una referencia de reloj externa de 10 MHz en un FLEX-8600 conectado. Utilice una referencia externa cuando disponga de un oscilador disciplinado por GPS u otra fuente de 10 MHz de precisión y desee que la radio se sincronice con ella en lugar de con su oscilador interno.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. El diálogo Radio Setup requiere una conexión activa a la radio.
- Su señal de referencia externa de 10 MHz debe estar conectada al puerto REF IN del panel trasero del FLEX-8600 antes de cambiar la fuente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Localice el cuadro combinado `10 MHz Reference Source:`.
4. Seleccione `External` del cuadro combinado. Para volver al oscilador integrado, seleccione `Internal`.

## Función de cada control

| Control | Tipo | Rango válido / Comportamiento |
|---|---|---|
| `10 MHz Reference Source:` | Cuadro combinado | `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. El estado de sincronización (Locked / Unlocked) se muestra junto al cuadro y se actualiza en tiempo real. |
| `TX Follows Active Slice` | Botón pulsador | TX sigue la slice activa. Mutuamente excluyente con `Active Slice Follows TX`. Se desactiva automáticamente durante operación Split. |
| `Active Slice Follows TX` | Botón pulsador | Cambia la slice activa cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con `TX Follows Active Slice`. |
| `Deslizadores de nitidez de filtro Voice / CW / Digital` | Deslizador (0–3) | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador se desactiva cuando Auto está activado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| `Auto (Voice / CW / Digital)` | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; desactiva el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| `Connect / Disconnect (TGXL)` | Botón pulsador | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que se rompió en firmware 4.2. Si el campo IP está vacío y la radio ha detectado el TGXL, la IP detectada se pre-rellena. |
| `Connect / Disconnect (PGXL)` | Botón pulsador | Abre/cierra la conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| `Connect / Disconnect (Antenna Genius)` | Botón pulsador | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado "Connected" cuando un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo conectado. |
| `Connect / Disconnect (ShackSwitch)` | Botón pulsador | Abre/cierra la conexión a un interruptor de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en el faro de descubrimiento AG. La auto-descubrimiento vía UDP también funciona sin esta fila. Fila oculta del estado "Connected" si un Antenna Genius (no-ShackSwitch) es el dispositivo conectado. |
| `⚙ Web UI (ShackSwitch)` | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza `webPort` del faro si > 1024; en caso contrario, recurre a `SS_WebPort` o puerto 5000. |
| `Select Installer...` | Botón pulsador | Abre un selector de archivos que acepta instaladores `.msi` (FlexRadio v4.2+ WiX), instalador ejecutable auto-extraíble `.exe` más antiguo, o archivo de firmware pre-extraído `.ssdr`. El preparador de firmware auto-detecta el formato a partir de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae `.ssdr` sin herramientas externas. La etiqueta fue `Browse .ssdr...` antes de v0.9.3. |
| `APD` (pestaña) | Pestaña | Configuración del muestreador Pre-Distorsión Adaptativa externa — selección por antena de TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y botón de restablecimiento del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios serie 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| `Cuadros combinados muestreador ANT1 / ANT2 / XVTA / XVTB (APD)` | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para entrenamiento APD para esa antena de TX. Predeterminado `INTERNAL`. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en tiempo real desde el subobjeto `apd sampler` de la radio. Retrocede a `INTERNAL` si la radio informa un valor no reconocido. |
| `Equalizer Reset (APD)` | Botón pulsador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| `Themes` (pestaña) | Pestaña | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. |
| `Use Aether defaults / Custom colors` | Botón de radio | Cambia el esquema de color de slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| `Botones de color Slice A–H` | Botón pulsador | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y distintivos de canal CAT. Los botones se desactivan cuando se selecciona `Use Aether defaults`. Hasta 8 slices (`kSliceColorCount`). |
| `Reset All to Defaults (Themes)` | Botón pulsador | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

A partir de v0.9.3, el flujo de trabajo de actualización de firmware ya no descarga automáticamente los archivos del instalador. Cuando `Check for Update` encuentra una versión más nueva, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com y luego use `Select Installer...` para prepararlo localmente. El botón previamente etiquetado como `Browse .ssdr...` ahora se etiqueta como `Select Installer...` y acepta archivos `.msi`, `.exe` y `.ssdr`.

### Cómo actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `Radio`.
3. Haga clic en `Check for Update`. AetherSDR se comunica con el servidor de actualización de FlexRadio e informa la versión disponible más reciente en la etiqueta de estado.
4. Si hay una actualización disponible, descargue el instalador SmartSDR desde flexradio.com.
5. Haga clic en `Select Installer...` y elija el archivo `.msi`, `.exe` o `.ssdr` pre-extraído descargado. AetherSDR auto-detecta el formato y extrae el firmware. La etiqueta de estado muestra el progreso de la preparación.
6. Cuando la preparación se complete, haga clic en `Upload Firmware`. Una barra de progreso y etiqueta de estado rastrean la carga.

## Calibración de frecuencia (pestaña RX)

A partir de v0.9.2.1, los controles de calibración de frecuencia en la pestaña RX siempre son visibles, independientemente de si un GPSDO está instalado. Cuando un GPSDO está presente, la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." (mostrado en verde). Cuando no hay GPSDO presente, la etiqueta lee "Manual frequency offset calibration available." (mostrado en ámbar). En versiones anteriores, los controles de calibración estaban ocultos cuando se detectaba un GPSDO.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| `Cal Frequency (MHz):` | Campo de texto | Frecuencia utilizada para calibración manual. Ingrese la frecuencia exacta de su señal de referencia en MHz. |
| `Start` | Botón pulsador | Establece la frecuencia de calibración, restablece `freq_error_ppb` a 0 y luego inicia el barrido de calibración. El botón está desactivado y muestra "Busy" mientras la calibración está en progreso. Una etiqueta de estado junto al botón muestra el estado actual (Starting…, texto de progreso o resultado). El campo no debe estar vacío; si lo está, la etiqueta de estado le solicita que ingrese una frecuencia antes de continuar. |
| `Freq Offset (ppb):` | Cuadro de giro | Desplazamiento manual de frecuencia en partes por mil millones. Ajuste si necesita aplicar un desplazamiento conocido sin ejecutar el barrido de calibración automatizado. |

### Cómo ejecutar un barrido de calibración

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Ingrese la frecuencia exacta de su señal de referencia en el campo `Cal Frequency (MHz):`.
4. Haga clic en `Start`. El botón se desactiva y muestra "Busy". Vea la etiqueta de estado para el progreso.
5. Cuando el barrido termine, la etiqueta de estado informa el resultado y el botón `Start` se vuelve a habilitar.

## Interfaz web de ShackSwitch

v0.9.4 añade el botón `⚙ Web UI` a la fila ShackSwitch en la pestaña Peripherals. Haga clic en él para abrir la interfaz de configuración web integrada de ShackSwitch en su navegador del sistema.

El botón determina la URL como sigue:

1. Si ShackSwitch está actualmente conectado y su faro de descubrimiento anuncia un `webPort` mayor que 1024, se utiliza ese puerto.
2. En caso contrario, se utiliza el valor almacenado en `SS_WebPort`.
3. Si ninguna fuente proporciona un puerto válido, se utiliza el puerto 5000.

La dirección IP se toma de `SS_ManualIp`. Si esa configuración está vacía y un ShackSwitch está actualmente conectado, se utiliza en su lugar la dirección del punto final en vivo. El botón no hace nada si no se puede determinar ninguna dirección IP.

### Cómo abrir la interfaz web de ShackSwitch

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `Peripherals`.
3. Confirme que la fila ShackSwitch muestre "Connected", o ingrese la IP del dispositivo y haga clic en `Connect (ShackSwitch)`.
4. Haga clic en `⚙ Web UI`. La página de configuración de ShackSwitch se abre en su navegador predeterminado.

## Consejos

- La pestaña `RX` también contiene el cuadro combinado `10 MHz Reference Source:`. Si está utilizando un oscilador disciplinado por GPS, cambie la fuente de referencia a `GPSDO` o `External` según corresponda antes de ejecutar la calibración.
- Si el campo `Cal Frequency (MHz):` está vacío cuando hace clic en `Start`, la etiqueta de estado le solicitará que ingrese una frecuencia. No se envían comandos a la radio en ese caso.
- Las filas Antenna Genius y ShackSwitch en la pestaña Peripherals comparten la misma conexión subyacente. Conectarse a una desconecta la otra. La fila para el tipo de dispositivo que no está actualmente conectado se oculta automáticamente del estado "Connected".

## Solución de problemas

- **La frecuencia de la radio parece inestable u desplazada después de cambiar a External** — La señal REF IN puede estar ausente, con un nivel demasiado bajo o no exactamente 10 MHz. Verifique que la fuente externa esté funcionando y correctamente conectada antes de seleccionar `External`. Cambie nuevamente a `Internal` mientras diagnostica.
- **El botón Start permanece desactivado / muestra "Busy" indefinidamente** — Esto puede ocurrir si la radio no responde al comando `radio pll_start`. Desconecte y reconecte a la radio e intente de nuevo.
- **`Select Installer...` muestra un error de preparación** — Asegúrese de que el archivo sea un instalador SmartSDR auténtico o archivo `.ssdr` y no haya sido dañado durante la descarga. Descargue nuevamente desde flexradio.com
