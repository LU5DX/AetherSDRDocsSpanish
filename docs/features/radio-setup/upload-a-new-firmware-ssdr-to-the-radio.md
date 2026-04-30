# Cargar un archivo de firmware nuevo en la radio

Esta página explica cómo cargar una imagen de firmware en su FLEX-8600 usando el diálogo Radio Setup. Haría esto para actualizar la radio a una versión de firmware específica sin usar la verificación de actualización automática.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Radio no se rellenará correctamente sin una conexión activa.
- Descargue el instalador de SmartSDR desde flexradio.com y anote dónde se guarda en su computadora. AetherSDR acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador antiguo autoextraíble), o un archivo de firmware `.ssdr` preextraído.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Select Installer...** para abrir un selector de archivos.
4. Navegue hasta el instalador o archivo de firmware en su computadora, selecciónelo y confirme. AetherSDR detecta automáticamente el formato desde el encabezado del archivo y extrae el `.ssdr` si es necesario. Aparece un mensaje de estado mientras se prepara el firmware.
5. Cuando el estado indique que el firmware está listo, haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado debajo del botón. Espere hasta que el estado indique que la carga está completa antes de hacer cualquier otra cosa.
7. Reinicie la radio según lo indicado por las notas de la versión del firmware para aplicar el nuevo firmware.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles. Si se encuentra una actualización, el área de estado muestra la versión disponible e instruye descargar el instalador de SmartSDR desde flexradio.com, luego usar **Select Installer...** para prepararlo. |
| **Select Installer...** | Botón | Abre un diálogo de archivo que acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador antiguo autoextraíble), o un archivo `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Se muestra un mensaje de estado mientras se prepara el archivo. Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Botón | Inicia la carga usando el archivo preparado por **Select Installer...**. Una barra de progreso y texto de estado aparecen debajo y se actualizan mientras progresa la transferencia. |
| TX Follows Active Slice | Botón | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Controles deslizantes | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Alternador | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando se conecta, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio `tgxl autotune handle=<H>` rota en firmware 4.2. El TGXL controla PTT de radio mediante su cable de interbloqueo de hardware; no se necesita activación del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se pre-completa. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |
| Pestaña APD | Pestaña | Configuración del muestreador Adaptive Pre-Distortion externo — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios de la serie 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| Combos muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa al conducir un amplificador lineal externo. Las opciones se rellenan en directo desde el subobjeto `apd sampler` de la radio. Regresa a INTERNAL si la radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Pestaña Themes | Pestaña | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Calibración de frecuencia (pestaña RX)

La pestaña RX muestra controles de calibración sin importar si se instala un GPSDO. La etiqueta de estado en la parte superior de la pestaña cambia el texto y color según el hardware presente:

- **GPSDO instalado** — la etiqueta lee "GPSDO installed. Manual frequency offset calibration available." en verde. Aún puede ejecutar una calibración manual si es necesario.
- **Sin GPSDO** — la etiqueta lee "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** siempre están visibles y activos. Antes de v0.9.2.1, los controles de calibración estaban ocultos cuando se detectaba un GPSDO.

### Usar el botón Start

El botón **Start** ahora proporciona retroalimentación de estado en línea directamente en la pestaña RX en lugar de confiar únicamente en la respuesta de la radio. Cuando hace clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz)** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no procede.
2. El texto del botón cambia a **Busy** y el botón se deshabilita hasta que se complete la secuencia de comandos de calibración.
3. AetherSDR envía `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0` para reiniciar cualquier desplazamiento anterior, luego emite `radio pll_start` para comenzar el barrido de calibración.
4. La etiqueta de estado en línea al lado del botón se actualiza según avanza la calibración.
5. Cuando la secuencia termina (o falla), el botón se vuelve a habilitar y revierte a **Start**.

La actividad de calibración se registra en el registro de protocolo a nivel de depuración, incluyendo el valor de frecuencia de calibración, el reinicio ppb, e identificador de ejecución interno que ayuda a correlacionar entradas de registro cuando se realizan múltiples intentos de calibración en la misma sesión.

### Controles de frecuencia de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Campo | Introduzca la frecuencia de referencia conocida en MHz (seis posiciones decimales). Se envía como `radio set cal_freq=<value>` cuando sale del campo o hace clic en **Start**. |
| **Start** | Botón | Restablece el error de frecuencia a 0 ppb, luego inicia el barrido de calibración. Se deshabilita y se etiqueta como **Busy** mientras se ejecuta un barrido. |
| **Freq Offset (ppb)** | Cuadro de rotación | Desplazamiento de frecuencia manual en partes por billón. Ajuste después de la calibración si se necesita ajuste fino. |

## Consejos

- Si solo desea verificar si existe una versión más nueva en lugar de cargar un archivo específico, use primero **Check for Update**. El área de estado le indicará la versión disponible y lo dirigirá a descargar el instalador desde flexradio.com.
- **Select Installer...** acepta archivos `.msi`, `.exe` y `.ssdr`. No necesita extraer un `.ssdr` de un instalador manualmente — AetherSDR lo maneja automáticamente.
- El área de estado de firmware está vacía hasta que se prepara un archivo o comienza una carga. Si no ve una barra de progreso después de hacer clic en **Upload Firmware**, confirme que un archivo fue preparado exitosamente con **Select Installer...** primero.
- Si **Start** muestra "Enter cal frequency" en ámbar, escriba un valor de frecuencia en el campo **Cal Frequency (MHz)** antes de hacer clic en **Start** nuevamente.
- Incluso con un GPSDO instalado, puede ejecutar una pasada de calibración manual si necesita verificar o anular la corrección automática.

## Solución de problemas

- **Upload Firmware no hace nada** — Ningún archivo de firmware ha sido preparado. Haga clic en **Select Installer...**, seleccione el archivo `.msi`, `.exe` o `.ssdr`, espere a que el mensaje de estado confirme que el archivo está listo, luego haga clic en **Upload Firmware**.
- **Los controles de la pestaña Radio no están rellenados o aparecen grises** — AetherSDR no está conectado a la radio. Establezca una conexión mediante `Settings > Connect to Radio...` antes de abrir Radio Setup.
- **El botón Start permanece etiquetado como Busy** — La radio no respondió al comando `radio pll_start`. Consulte el registro de protocolo para el identificador de ejecución relevante, verifique que la radio esté conectada y no transmitiendo, luego intente de nuevo.
- **La pestaña APD no es visible** — La radio conectada no reporta `apd configurable=1`. La pestaña APD solo está disponible en radios de la serie FLEX-8x00 con firmware SmartSDR 4.2.18 o posterior.

## Relacionado

- [Verificar número de serie de radio, versión de hardware, región y opciones](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
