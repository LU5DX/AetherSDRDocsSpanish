# Alternar entre filtros de baja latencia y filtros nítidos por ancho de banda

La pestaña Filters en Radio Setup le permite elegir entre filtros DSP de baja latencia y filtros nítidos para cada ancho de banda de recepción, y opcionalmente forzar el uso de filtros de baja latencia al usar modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Filters solo está disponible cuando hay una conexión activa con la radio.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros para el ancho de banda actual. El botón refleja la selección activa.
4. Para forzar el uso de filtros de baja latencia cuando un modo digital (DIGU o DIGL) esté activo, marque **Use Low Latency Filters for Digital Modes**.
5. Cierre el diálogo. Los ajustes surten efecto de inmediato.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre baja latencia y filtros nítidos para el ancho de banda seleccionado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está marcada, anula la elección de filtro por ancho de banda y utiliza filtros de baja latencia siempre que haya un slice DIGU o DIGL activo. |
| Deslizadores de nitidez de filtro (Voice / CW / Digital) | Deslizador | Establece la nitidez del filtro (0=mínima latencia a 3=máxima nitidez) por modo. El deslizador está deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <modo> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el deslizador manual de nitidez. Los comandos se envían como `radio filter_sharpness <modo> auto_level=1`. |
| TX Follows Active Slice | Botón pulsador | TX sigue al slice activo. Es mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante una operación en Split. |
| Active Slice Follows TX | Botón pulsador | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Es mutuamente excluyente con TX Follows Active Slice. |
| Connect / Disconnect (TGXL) | Botón pulsador | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, la cual está rota en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón pulsador | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón pulsador | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (en lugar de un Antenna Genius) es el dispositivo conectado. |
| Connect / Disconnect (ShackSwitch) | Botón pulsador | Abre o cierra una conexión a un conmutador de antenas ShackSwitch mediante el protocolo UDP/TCP de AG en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta mediante el campo ShackSwitch en el beacon de difusión de AG. El descubrimiento automático mediante UDP también funciona sin introducir manualmente una dirección. La fila se oculta del estado Conectado si un Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| Select Installer... | Botón pulsador | Abre un selector de archivos que acepta archivos `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en este botón para prepararlo. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las series 6000 y radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se cargan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. |
| Equalizer Reset (APD) | Botón pulsador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de colores de los slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color de slice A–H | Botón pulsador | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles de inmediato en los widgets de VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón pulsador | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. |

## Flujo de actualización de firmware (v0.9.3)

A partir de v0.9.3, el flujo de actualización de firmware ya no descarga el instalador automáticamente. Cuando **Check for Update** encuentra una versión más reciente, el área de estado le indica que descargue el instalador de SmartSDR desde flexradio.com usted mismo. Use **Select Installer...** para indicarle a AetherSDR el archivo que descargó.

### Formatos de instalador compatibles

| Tipo de archivo | Descripción |
|---|---|
| `.msi` | Instalador WiX de FlexRadio (SmartSDR v4.2 y posteriores). Recomendado. |
| `.exe` | Instalador autoextraíble antiguo (versiones anteriores a v4.2). |
| `.ssdr` | Archivo de firmware preextraído. |

El gestor lee los primeros 8 bytes del archivo para identificar el formato (magia OLE/MSI o cabecera PE/COFF MZ) y extrae el payload `.ssdr` sin necesidad de herramientas externas.

### Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, el área de estado muestra el número de versión y le indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com.
5. Haga clic en **Select Installer...** y localice el archivo `.msi`, `.exe` o `.ssdr` descargado. AetherSDR prepara el firmware e informa el progreso en el área de estado.
6. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1, los controles de calibración de frecuencia en la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles Cal Frequency y Start estaban ocultos cuando se detectaba un GPSDO.

- Cuando hay un GPSDO instalado, la etiqueta de estado dice "GPSDO installed. Manual frequency offset calibration available." en verde.
- Cuando no hay un GPSDO instalado, la etiqueta de estado dice "Manual frequency offset calibration available." en ámbar.

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), establece la frecuencia de calibración e inicia el barrido de calibración del PLL. El campo de estado junto al botón Start se actualiza a medida que avanza la calibración.
5. Mientras la calibración se está ejecutando, el botón **Start** está deshabilitado y muestra "Busy". Se vuelve a habilitar cuando la calibración se completa o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario después de que la calibración se complete.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Spinbox | Frecuencia utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Botón pulsador | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración del PLL. Se deshabilita y muestra "Busy" mientras una calibración está en curso. |
| **Freq Offset (ppb)** | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External 10 MHz. Las opciones mostradas dependen del hardware instalado y del estado del oscilador informado por la radio. Si Auto está seleccionado y la radio ha resuelto una fuente específica, la etiqueta de estado muestra la fuente resuelta (por ejemplo, "Auto -> GPSDO"). Si la fuente seleccionada difiere del estado activo, se muestran ambas (por ejemplo, "GPSDO -> TCXO"). El estado de bloqueo (Locked / Unlocked) se agrega a la etiqueta y se actualiza en vivo. Si External 10 MHz está seleccionado pero no se detecta ninguna referencia externa, la etiqueta además muestra "(not detected)". El color de la etiqueta es verde cuando está bloqueada y rojo cuando está desbloqueada. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento, lo que beneficia la decodificación de modos digitales en tiempo real y CW. Los filtros nítidos proporcionan una selectividad de pendiente más pronunciada, lo que es más útil para condiciones de SSB congestionadas.
- La casilla **Use Low Latency Filters for Digital Modes** se aplica a todos los anchos de banda, por lo que no necesita cambiar la configuración por ancho de banda cada vez que cambie a un modo digital.
- Si **Start** no se activa después de introducir una frecuencia de calibración, verifique que el campo Cal Frequency no esté vacío.
- Cuando **Check for Update** informa una actualización disponible, AetherSDR ya no descarga el instalador por usted. Descargue el instalador de SmartSDR desde flexradio.com, luego use **Select Installer...** para prepararlo.
- Para abrir la interfaz web del ShackSwitch directamente desde AetherSDR, haga clic en **⚙ Web UI** en la pestaña Peripherals. AetherSDR utiliza la IP de `SS_ManualIp` o la conexión activa, y el puerto del campo `webPort` del beacon (si es mayor que 1024), `SS_WebPort`, o el puerto 5000 como valor de reserva.
- La etiqueta de estado **10 MHz Reference Source** en la pestaña RX ahora muestra la ruta de resolución completa cuando el modo Auto está activo y cuando la fuente activa difiere de la fuente configurada. Revise esta etiqueta para confirmar que la radio se ha bloqueado a la referencia deseada.
