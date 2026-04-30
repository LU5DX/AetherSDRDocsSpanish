# Alternar entre filtros de baja latencia y filtros agudos por ancho de banda

La pestaña Filters en Radio Setup le permite elegir entre filtros DSP de baja latencia y filtros agudos para cada ancho de banda de recepción, y opcionalmente forzar filtros de baja latencia al usar modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Filters solo está disponible cuando existe una conexión activa a la radio.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros para el ancho de banda actual. El botón refleja la selección activa.
4. Para forzar filtros de baja latencia cuando cualquier modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.
5. Cierre el diálogo. Los ajustes entran en vigor inmediatamente.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre filtros de baja latencia y filtros agudos para el ancho de banda seleccionado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando se marca, anula la opción de filtro por ancho de banda y utiliza filtros de baja latencia siempre que un slice DIGU o DIGL esté activo. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=latencia más baja a 3=más agudo) por modo. El control deslizante se desactiva cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo y desactiva el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| TX Follows Active Slice | Botón de acción | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón de acción | Cambia el slice activo cuando TX se mueve externamente (por ejemplo WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |
| Connect / Disconnect (TGXL) | Botón de acción | Abre o cierra una conexión TCP directa a TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente a TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio que se rompió en firmware 4.2. TGXL controla PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita activación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto TGXL, la IP descubierta se rellena previamente. |
| Connect / Disconnect (PGXL) | Botón de acción | Abre o cierra una conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón de acción | Abre o cierra una conexión a Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |
| Select Installer... | Botón de acción | Abre un selector de archivos que acepta instaladores WiX `.msi` (FlexRadio v4.2+), instaladores autoextraíbles `.exe` (versiones anteriores), o un archivo de firmware `.ssdr` preextraído. El organizador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (firma OLE/MSI o encabezado PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en este botón para organizarlo. Etiqueta cambiada desde **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador Adaptive Pre-Distortion externo — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| Combinados de muestreo ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón de acción | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de color de slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón de acción | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en los widgets VFO, superpuestos de panadapter y distintivos de canal CAT. Los botones se desactivan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón de acción | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Flujo de actualización de firmware (v0.9.3)

A partir de v0.9.3, el flujo de actualización de firmware ya no descarga el instalador automáticamente. Cuando **Check for Update** encuentra una versión más nueva, el área de estado le indica que descargue el instalador de SmartSDR desde flexradio.com por su cuenta. Use **Select Installer...** para apuntar AetherSDR al archivo que descargó.

### Formatos de instalador compatibles

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador WiX de FlexRadio (SmartSDR v4.2 y posterior). Recomendado. |
| `.exe` | Instalador autoextraíble antiguo (versiones pre-v4.2). |
| `.ssdr` | Archivo de firmware preextraído. |

El organizador lee los primeros 8 bytes del archivo para identificar el formato (firma OLE/MSI o encabezado PE/COFF MZ) y extrae la carga útil `.ssdr` sin requerir ninguna herramienta externa.

### Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión e indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en **Select Installer...** y localice el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR organiza el firmware e informa el progreso en el área de estado.
6. Cuando la organización se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración de frecuencia en la pestaña **RX** están disponibles independientemente de si se instala un GPSDO. Anteriormente, los controles Cal Frequency y Start estaban ocultos cuando se detectaba un GPSDO.

- Cuando se instala un GPSDO, la etiqueta de estado lee "GPSDO installed. Manual frequency offset calibration available." en verde.
- Cuando no se instala un GPSDO, la etiqueta de estado lee "Manual frequency offset calibration available." en ámbar.

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), establece la frecuencia de calibración e inicia el barrido de calibración PLL. El campo de estado junto al botón Start se actualiza a medida que avanza la calibración.
5. Mientras se ejecuta la calibración, el botón **Start** está desactivado y muestra "Busy". Se reactiva cuando la calibración se completa o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario después de que se complete la calibración.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Cuadro giratorio | Frecuencia utilizada para calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Botón de acción | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración PLL. Desactivado y etiquetado como "Busy" mientras hay una calibración en progreso. |
| **Freq Offset (ppb)** | Cuadro giratorio | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Consejos

- Los filtros de baja latencia reducen el retraso de procesamiento, lo que beneficia la decodificación de modo digital en tiempo real y CW. Los filtros agudos proporcionan una selectividad de falda más pronunciada, que es más útil en condiciones SSB concurridas.
- La casilla de verificación **Use Low Latency Filters for Digital Modes** se aplica en todos los anchos de banda, por lo que no necesita alternar la configuración por ancho de banda cada vez que cambia a un modo digital.
- Si **Start** no se activa después de ingresar una frecuencia de calibración, verifique que el campo Cal Frequency no esté vacío.
- Cuando **Check for Update** reporta una actualización disponible, AetherSDR ya no descarga el instalador por usted. Descargue el instalador de SmartSDR desde flexradio.com y luego use **Select Installer...** para organizarlo.

## Relacionado

- [Radio Setup overview](overview.md)
- [Select iambic mode A or B for the radio keyer](select-iambic-mode-a-or-b-for-the-radio-keyer.md)
