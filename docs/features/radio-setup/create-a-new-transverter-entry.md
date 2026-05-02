# Crear una nueva entrada de transverter

Use esta página para añadir una definición de transverter a su FLEX-8600, de modo que AetherSDR conozca el desplazamiento de frecuencia IF-a-RF y los parámetros de operación para la banda de su transverter.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Tenga a mano el rango de frecuencia IF que utiliza su transverter y el desplazamiento de frecuencia RF que desea mostrar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.
4. Aparece una nueva pestaña anidada. Configure los campos de la nueva entrada en esa pestaña.
5. Para restringir la entrada solo a recepción, establezca **RX Only:** en el estado habilitado.
6. Para eliminar una entrada que ya no necesita, haga clic en **Remove** en la pestaña de esa entrada.
7. Cierre el diálogo con **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Añade una nueva entrada de transverter y abre su pestaña de configuración. |
| **RX Only:** | Botón de alternancia | Fuerza el transverter a solo recepción, impidiendo la transmisión a través de él. |
| **Remove** | Botón | Elimina permanentemente la definición de transverter seleccionada. |
| TX Follows Active Slice | Botón | La transmisión sigue al slice (canal de recepción) activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. |
| Active Slice Follows TX | Botón | Cambia el slice activo cuando la transmisión se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=menor latencia a 3=mayor nitidez) por modo; el control queda deshabilitado cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE con el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que está rota en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y la radio ha detectado el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si el dispositivo conectado es un ShackSwitch (en lugar de un Antenna Genius estándar). |
| Connect / Disconnect (ShackSwitch) | Botón | Abre/cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo 'ShackSwitch' en el beacon de difusión AG. El descubrimiento automático vía UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (que no sea ShackSwitch). |
| ⚙ Web UI (ShackSwitch) | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| Select Installer... | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego use este botón para prepararlo. La etiqueta cambió de **Browse .ssdr...** en la versión v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. |
| Cuadros combinados ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que utiliza la radio para muestrear la RF de salida durante el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando use un amplificador lineal externo. Las opciones se obtienen en tiempo real del sub-objeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. Valor predeterminado: INTERNAL. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz — actualmente alberga la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. |
| Botones de color de Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Se admiten hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

Use los controles de la pestaña **Radio** para verificar y aplicar actualizaciones de firmware.

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` ya extraído. El preparador detecta el formato del archivo automáticamente y extrae el firmware sin herramientas externas. Aparece un indicador de progreso mientras se completa la preparación.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio.

## Calibración de frecuencia (pestaña RX)

En la versión v0.9.2.1, los controles de calibración de la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** se ocultaban cuando se detectaba un GPSDO. La etiqueta de estado en la parte superior del grupo ahora muestra:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Cómo funciona la calibración en v0.9.2.1

El botón **Start** ahora valida el campo de frecuencia de calibración antes de enviar cualquier comando, restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego inicia el barrido PLL. Mientras el barrido está en curso, **Start** se deshabilita y muestra la etiqueta **Busy**. Una etiqueta de estado junto al botón muestra el texto de progreso. El botón y la etiqueta vuelven a su estado normal cuando el barrido se completa o falla.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Introduzca la frecuencia de referencia en MHz usada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y muestra la etiqueta **Busy** mientras el barrido está en curso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de calibración: iniciando, texto de progreso o error. Se actualiza en tiempo real durante el barrido. |

## Consejos

- Cada transverter obtiene su propia pestaña anidada dentro de la pestaña XVTR. Si tiene varios transverters, use esas pestañas para cambiar entre entradas.
- Si necesita volver a este diálogo más adelante para ajustar un transverter, abra nuevamente `Settings > Radio Setup...` y vaya directamente a la pestaña **XVTR**.
- En la pestaña **RX**, introduzca siempre una frecuencia de referencia precisa y conocida en **Cal Frequency (MHz):** antes de hacer clic en **Start**. Dejar el campo vacío cancela el barrido.
- Cuando **Check for Update** informa una nueva versión de firmware, descargue el instalador de SmartSDR desde flexradio.com antes de hacer clic en **Select Installer...**. AetherSDR ya no descarga el instalador automáticamente.
- La pestaña **APD** aparece únicamente en radios FLEX-8x00 que ejecutan SmartSDR 4.2.18 o posterior. Si no la ve, el modelo de radio o la versión de firmware no admite APD configurable.
- Los colores de slice personalizados establecidos en la pestaña **Themes** se aplican de inmediato a los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Seleccione **Use Aether defaults** y haga clic en **Reset All to Defaults** para volver a la paleta estándar.
- Para abrir la interfaz web del ShackSwitch, haga clic en **⚙ Web UI** en la fila ShackSwitch de la pestaña **Peripherals**. El botón usa el puerto web anunciado por el dispositivo cuando está disponible; si el beacon no proporciona un puerto válido, recurre a `SS_WebPort` o al puerto 5000.
- La fila **Antenna Genius** oculta su estado Connected cuando el dispositivo activo es un ShackSwitch. Use la fila **ShackSwitch** para gestionar esa conexión.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Establecer potencia TX máxima por banda y modo de sintonía](set-per-band-tx-max-power-and-tune-mode.md)
