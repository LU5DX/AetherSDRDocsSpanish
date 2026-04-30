# Crear una nueva entrada de transvertor

Use esta página para agregar una definición de transvertor a su FLEX-8600 de modo que AetherSDR conozca el desplazamiento de frecuencia IF-a-RF y los parámetros de funcionamiento de su banda de transvertor.

## Antes de comenzar

- El radio debe estar conectado. Radio Setup requiere una conexión de radio activa.
- Conozca el rango de frecuencia IF que utiliza su transvertor y el desplazamiento de frecuencia RF que desea mostrar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.
4. Aparece una nueva pestaña anidada. Configure los campos para la nueva entrada en esa pestaña.
5. Para restringir la entrada a recepción solamente, establezca **RX Only:** en el estado habilitado.
6. Para eliminar una entrada que ya no necesita, haga clic en **Remove** en la pestaña de esa entrada.
7. Cierre el diálogo con **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Agrega una nueva entrada de transvertor y abre su pestaña de configuración. |
| **RX Only:** | Botón de alternancia | Obliga al transvertor a ser de solo recepción, evitando TX a través de él. |
| **Remove** | Botón | Elimina permanentemente la definición de transvertor seleccionada. |
| TX Follows Active Slice | Botón | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio rota en el firmware 4.2. El TGXL controla el PTT del radio a través de su cable de bloqueo de hardware; no se necesita codificación del lado del cliente. Si el campo IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |
| Select Installer... | Botón | Abre un selector de archivos que acepta instalador WiX `.msi` (FlexRadio v4.2+), instalador autoextraíble `.exe` (versiones anteriores) o archivo de firmware `.ssdr` preextraído. El gestor de firmware autodetecta el formato desde los primeros 8 bytes (número mágico OLE/MSI vs MZ PE/COFF) y extrae `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le instruye descargar el instalador SmartSDR desde flexradio.com y luego usar este botón para almacenarlo. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador externo de predistorsión adaptativa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que el radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; los radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que el radio usa para muestrear la RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en directo desde el subobjeto `apd sampler` del radio. Vuelve a INTERNAL si el radio reporta un valor no reconocido. Predeterminado: INTERNAL. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de color de slice entre la paleta integrada de AetherSDR y un conjunto personalizado completo por slice. |
| Botones de color Slice A–H | Botón | Haga clic en cualquier botón etiquetado (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter e insignias de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Se admiten hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores de slice personalizados a la paleta AetherSDR integrada. |

## Actualización de firmware (pestaña Radio)

Use los controles en la pestaña **Radio** para buscar y aplicar actualizaciones de firmware.

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualización de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica descargar el instalador SmartSDR desde flexradio.com.
2. Descargue el instalador SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` preextraído. El gestor detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. Un indicador de progreso aparece mientras se completa el almacenamiento.
4. Haga clic en **Upload Firmware** para transferir el firmware almacenado al radio.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración en la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, **Cal Frequency (MHz):**,  **Start** y **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. La etiqueta de estado en la parte superior del grupo ahora dice:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Cómo funciona la calibración en v0.9.2.1

El botón **Start** ahora valida el campo de frecuencia de calibración antes de enviar comandos, reinicia el error de frecuencia a cero (`radio set freq_error_ppb=0`), luego activa el barrido PLL. Mientras el barrido se ejecuta, **Start** se deshabilita y se etiqueta **Busy**. Una etiqueta de estado al lado del botón muestra el texto de progreso. El botón y la etiqueta vuelven a sus estados normales cuando el barrido se completa o falla.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Introduzca la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Valida el campo, reinicia `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y se etiqueta **Busy** mientras un barrido está en progreso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de calibración: Starting, texto de progreso o error. Se actualiza en directo durante el barrido. |

## Consejos

- Cada transvertor obtiene su propia pestaña anidada dentro de la pestaña XVTR. Si tiene múltiples transvortores, use esas pestañas para cambiar entre entradas.
- Si necesita volver a este diálogo más tarde para ajustar un transvertor, reabra `Settings > Radio Setup...` y vaya directamente a la pestaña **XVTR**.
- En la pestaña **RX**, siempre introduzca una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):** antes de hacer clic en **Start**. Dejar el campo vacío cancela el barrido.
- Cuando **Check for Update** reporte una nueva versión de firmware, descargue el instalador SmartSDR desde flexradio.com antes de hacer clic en **Select Installer...**. AetherSDR ya no descarga el instalador automáticamente.
- La pestaña **APD** aparece solo en radios FLEX-8x00 que ejecutan SmartSDR 4.2.18 o posterior. Si no la ve, su modelo de radio o versión de firmware no admite APD configurable.
- Los colores de slice personalizados establecidos en la pestaña **Themes** se aplican inmediatamente a widgets VFO, superposiciones panadapter e insignias de canal CAT. Seleccione **Use Aether defaults** y haga clic en **Reset All to Defaults** para volver a la paleta estándar.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Establecer potencia TX máxima por banda y modo de sintonización](set-per-band-tx-max-power-and-tune-mode.md)
