# Alterne entre filtros de baja latencia y filtros agudos por ancho de banda

La pestaña Filters (Filtros) en Radio Setup le permite elegir entre filtros DSP de baja latencia y filtros agudos para cada ancho de banda de recepción, y opcionalmente forzar filtros de baja latencia cuando utiliza modos digitales.

## Antes de empezar

- AetherSDR debe estar conectado a la radio. La pestaña Filters solo está disponible cuando hay una conexión de radio activa.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros del ancho de banda actual. El botón refleja la selección activa.
4. Para forzar filtros de baja latencia siempre que un modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.
5. Cierre el diálogo. La configuración toma efecto inmediatamente.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre filtros de baja latencia y agudos para el ancho de banda seleccionado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, anula la opción de filtro por ancho de banda y utiliza filtros de baja latencia siempre que una slice DIGU o DIGL esté activa. |
| Controles deslizantes de agudeza de filtro Voice / CW / Digital | Control deslizante | Define la agudeza del filtro (0=latencia más baja a 3=más agudo) por modo. El control deslizante está deshabilitado cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática de nivel de filtro para ese modo y deshabilita el control deslizante de agudeza manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| TX Follows Active Slice | Botón presionador | TX sigue la slice activa. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón presionador | Cambia la slice activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |
| Connect / Disconnect (TGXL) | Botón presionador | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio rota en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de entrelace de hardware; no se necesita activación del lado del cliente. Si el campo de IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| Connect / Disconnect (PGXL) | Botón presionador | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón presionador | Abre o cierra una conexión con Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (en lugar de un Antenna Genius) es el dispositivo conectado. |
| Connect / Disconnect (ShackSwitch) | Botón presionador | Abre o cierra una conexión con un conmutador de antena ShackSwitch mediante el protocolo UDP/TCP de AG en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo ShackSwitch en la baliza de transmisión AG. La detección automática mediante UDP también funciona sin ingresar manualmente una dirección. La fila se oculta del estado Conectado si un Antenna Genius (sin ShackSwitch) es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón presionador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| Select Installer... | Botón presionador | Abre un selector de archivos que acepta instalador WiX `.msi` (FlexRadio v4.2+), instalador ejecutable antiguo `.exe` (lanzamientos pre-v4.2), o archivo de firmware previamente extraído `.ssdr`. El organizador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI frente al encabezado PE/COFF MZ) y extrae `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR de flexradio.com y luego haga clic en este botón para organizarlo. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador de predistorsión adaptativa externa — selección por antena TX de la puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña se oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear el RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando impulse un amplificador lineal externo. Las opciones se rellenan en vivo desde el sub-objeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. |
| Equalizer Reset (APD) | Botón presionador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience nuevamente. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de interfaz — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de color de slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón presionador | Haga clic en cualquier botón con letras (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y distintivos de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón presionador | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Flujo de actualización de firmware (v0.9.3)

A partir de v0.9.3, el flujo de actualización de firmware ya no descarga el instalador automáticamente. Cuando **Check for Update** encuentra una versión más reciente, el área de estado le indica que descargue usted mismo el instalador de SmartSDR de flexradio.com. Use **Select Installer...** para apuntar AetherSDR al archivo que descargó.

### Formatos de instalador compatibles

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador WiX de FlexRadio (SmartSDR v4.2 y posterior). Recomendado. |
| `.exe` | Instalador ejecutable antiguo (lanzamientos pre-v4.2). |
| `.ssdr` | Archivo de firmware previamente extraído. |

El organizador lee los primeros 8 bytes del archivo para identificar el formato (magic OLE/MSI o encabezado PE/COFF MZ) y extrae la carga `.ssdr` sin requerir herramientas externas.

### Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión e indica que descargue el instalador de flexradio.com.
4. Descargue el instalador de SmartSDR de flexradio.com.
5. Haga clic en **Select Installer...** y localice el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR organiza el firmware e informa del progreso en el área de estado.
6. Cuando la organización se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración de frecuencia en la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles Cal Frequency y Start se ocultaban cuando se detectaba un GPSDO.

- Cuando un GPSDO está instalado, la etiqueta de estado indica "GPSDO installed. Manual frequency offset calibration available." en verde.
- Cuando no hay GPSDO instalado, la etiqueta de estado indica "Manual frequency offset calibration available." en ámbar.

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), establece la frecuencia de calibración e inicia el barrido de calibración PLL. El campo de estado junto al botón Start se actualiza a medida que avanza la calibración.
5. Mientras la calibración se está ejecutando, el botón **Start** está deshabilitado y muestra "Busy". Se vuelve a habilitar cuando la calibración se completa o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario después de que se complete la calibración.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Cuadro giratorio | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Botón presionador | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración PLL. Deshabilitado y etiquetado como "Busy" mientras una calibración está en progreso. |
| **Freq Offset (ppb)** | Cuadro giratorio | Compensación de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento, lo que beneficia la decodificación de modo digital en tiempo real y CW. Los filtros agudos proporcionan una selectividad de falda más pronunciada, que es más útil en condiciones SSB concurridas.
- La casilla de verificación **Use Low Latency Filters for Digital Modes** se aplica en todos los anchos de banda, por lo que no necesita alternar la configuración por ancho de banda cada vez que cambia a un modo digital.
- Si **Start** no se activa después de ingresar una frecuencia de calibración, verifique que el campo Cal Frequency no esté vacío.
- Cuando **Check for Update** informa de una actualización disponible, AetherSDR ya no descarga el instalador para usted. Descargue el instalador de SmartSDR de flexradio.com, luego use **Select Installer...** para organizarlo.
- Para abrir la interfaz web de ShackSwitch directamente desde AetherSDR, haga clic en **⚙ Web UI** en la pestaña Peripherals. AetherSDR utiliza la IP de `SS_ManualIp` o la conexión activa, y el puerto del campo `webPort` de la baliza (si es mayor que 1024), `SS_WebPort` o el puerto 5000 como alternativa.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Seleccione el modo iámbico A o B para el sintonizador de la radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)
