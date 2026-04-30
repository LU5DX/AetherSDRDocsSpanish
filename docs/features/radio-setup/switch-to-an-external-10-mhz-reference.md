# Cambiar a una referencia externa de 10 MHz

Esta página explica cómo seleccionar una referencia de reloj externa de 10 MHz en un FLEX-8600 conectado. Use una referencia externa cuando tenga un oscilador disciplinado por GPS u otra fuente de 10 MHz de precisión y quiera que la radio se bloquee en ella en lugar de en su oscilador interno.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El diálogo Radio Setup requiere una conexión activa con la radio.
- Su señal de referencia externa de 10 MHz debe estar conectada al puerto REF IN del panel trasero en el FLEX-8600 antes de cambiar la fuente.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Localice el cuadro combinado `10 MHz Reference Source:`.
4. Seleccione `External` del cuadro combinado. Para volver al oscilador integrado, seleccione `Internal`.

## Qué hace cada control

| Control | Tipo | Rango válido / Comportamiento |
|---|---|---|
| `10 MHz Reference Source:` | Cuadro combinado | `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en tiempo real. |
| `TX Follows Active Slice` | Botón | TX sigue el slice activo. Mutuamente excluyente con `Active Slice Follows TX`. Se deshabilita automáticamente durante operación de Split. |
| `Active Slice Follows TX` | Botón | Cambia el slice activo cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con `TX Follows Active Slice`. |
| `Voice / CW / Digital filter sharpness sliders` | Regulador (0–3) | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el regulador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| `Auto (Voice / CW / Digital)` | Botón de conmutación | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el regulador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| `Connect / Disconnect (TGXL)` | Botón | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que se rompió en firmware 4.2. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa previamente. |
| `Connect / Disconnect (PGXL)` | Botón | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| `Connect / Disconnect (Antenna Genius)` | Botón | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |
| `Select Installer...` | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta era `Browse .ssdr...` antes de v0.9.3. |
| `APD` (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| `ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)` | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para entrenamiento de APD para esa antena TX. Predeterminado `INTERNAL`. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en tiempo real desde el subobjeto `apd sampler` de la radio. Vuelve a `INTERNAL` si la radio reporta un valor no reconocido. |
| `Equalizer Reset (APD)` | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| `Themes` (pestaña) | Pestaña | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| `Use Aether defaults / Custom colors` | Botón de radio | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| `Slice A–H color buttons` | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de colores y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter e insignias de canal CAT. Los botones se deshabilitan cuando se selecciona `Use Aether defaults`. Hasta 8 slices (`kSliceColorCount`). |
| `Reset All to Defaults (Themes)` | Botón | Restablece todos los colores personalizados del slice a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

A partir de v0.9.3, el flujo de trabajo de actualización de firmware ya no descarga archivos de instalador automáticamente. Cuando `Check for Update` encuentra una versión más nueva, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com y luego use `Select Installer...` para almacenarlo localmente. El botón previamente etiquetado como `Browse .ssdr...` ahora está etiquetado como `Select Installer...` y acepta archivos `.msi`, `.exe` y `.ssdr`.

### Cómo actualizar el firmware

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `Radio`.
3. Haga clic en `Check for Update`. AetherSDR contacta al servidor de actualización de FlexRadio e informa la versión más reciente disponible en la etiqueta de estado.
4. Si hay una actualización disponible, descargue el instalador SmartSDR desde flexradio.com.
5. Haga clic en `Select Installer...` y elija el archivo `.msi`, `.exe` o `.ssdr` descargado y preextraído. AetherSDR detecta automáticamente el formato y extrae el firmware. La etiqueta de estado muestra el progreso de preparación.
6. Cuando el almacenamiento se complete, haga clic en `Upload Firmware`. Una barra de progreso y etiqueta de estado rastrean la carga.

## Calibración de frecuencia (pestaña RX)

A partir de v0.9.2.1, los controles de calibración de frecuencia en la pestaña RX siempre son visibles, independientemente de si un GPSDO está instalado. Cuando un GPSDO está presente, la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." (mostrado en verde). Cuando no hay GPSDO presente, la etiqueta lee "Manual frequency offset calibration available." (mostrado en ámbar). En versiones anteriores, los controles de calibración estaban ocultos cuando se detectaba un GPSDO.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| `Cal Frequency (MHz):` | Campo de texto | Frecuencia utilizada para calibración manual. Ingrese la frecuencia exacta de su señal de referencia en MHz. |
| `Start` | Botón | Establece la frecuencia de calibración, reinicia `freq_error_ppb` a 0, luego inicia el barrido de calibración. El botón se deshabilita y muestra "Busy" mientras la calibración está en progreso. Una etiqueta de estado junto al botón muestra el estado actual (Starting…, texto de progreso o resultado). El campo no debe estar vacío; si lo está, la etiqueta de estado le solicita que ingrese una frecuencia antes de proceder. |
| `Freq Offset (ppb):` | Cuadro de desplazamiento | Desplazamiento de frecuencia manual en partes por mil millones. Ajuste si necesita aplicar un desplazamiento conocido sin ejecutar el barrido de calibración automatizado. |

### Cómo ejecutar un barrido de calibración

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña `RX`.
3. Ingrese la frecuencia exacta de su señal de referencia en el campo `Cal Frequency (MHz):`.
4. Haga clic en `Start`. El botón se deshabilita y muestra "Busy". Observe la etiqueta de estado para ver el progreso.
5. Cuando el barrido finaliza, la etiqueta de estado reporta el resultado y el botón `Start` se vuelve a habilitar.

## Consejos

- La pestaña `RX` también contiene el cuadro combinado `10 MHz Reference Source:`. Si está usando un oscilador disciplinado por GPS, cambie la fuente de referencia a `GPSDO` o `External` según corresponda antes de ejecutar la calibración.
- Si el campo `Cal Frequency (MHz):` está vacío cuando hace clic en `Start`, la etiqueta de estado le solicitará que ingrese una frecuencia. No se envían comandos a la radio en ese caso.

## Solución de problemas

- **La frecuencia de la radio aparece inestable u offset después de cambiar a External** — La señal REF IN puede estar ausente, tener un nivel demasiado bajo o no ser exactamente 10 MHz. Verifique que la fuente externa esté funcionando y correctamente conectada antes de seleccionar `External`. Cambie de vuelta a `Internal` mientras diagnóstica.
- **El botón Start permanece deshabilitado / muestra "Busy" indefinidamente** — Esto puede ocurrir si la radio no responde al comando `radio pll_start`. Desconecte y reconecte a la radio, luego inténtelo de nuevo.
- **`Select Installer...` muestra un error de preparación** — Asegúrese de que el archivo es un instalador SmartSDR genuino o archivo `.ssdr` y no ha sido corrompido durante la descarga. Descargue nuevamente desde flexradio.com e inténtelo de nuevo.

## Relacionado

- [Calibrate the GPSDO frequency offset](calibrate-the-gpsdo-frequency-offset.md)
