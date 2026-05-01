# Crear una nueva entrada de transvertor

Use esta página para agregar una definición de transvertor a su FLEX-8600 para que AetherSDR conozca el desplazamiento de frecuencia FI-a-RF y los parámetros de funcionamiento de su banda de transvertor.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión activa con la radio.
- Conozca el rango de frecuencia FI que utiliza su transvertor y el desplazamiento de frecuencia RF que desea mostrar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.
4. Aparece una nueva pestaña anidada. Configure los campos para la nueva entrada en esa pestaña.
5. Para restringir la entrada a solo recepción, establezca **RX Only:** en el estado habilitado.
6. Para eliminar una entrada que ya no necesite, haga clic en **Remove** en la pestaña de esa entrada.
7. Cierre el diálogo con **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Agrega una nueva entrada de transvertor y abre su pestaña de configuración. |
| **RX Only:** | Botón de alternancia | Fuerza el transvertor a solo recepción, impidiendo TX a través de él. |
| **Remove** | Botón | Elimina permanentemente la definición de transvertor seleccionada. |
| TX Follows Active Slice | Botón | TX sigue la slice activa. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el control deslizante se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra la conexión TCP directa con el TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse para que AetherSDR se reconecte automáticamente al iniciar. Es necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio que se rompió en firmware 4.2. El TGXL controla la PTT de la radio a través de su cable de bloqueo de hardware; no se requiere codificación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa previamente. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra la conexión TCP directa con Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra la conexión con Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo conectado. |
| Connect / Disconnect (ShackSwitch) | Botón | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en el baliza de transmisión AG. La detección automática por UDP también funciona sin esta fila. Fila oculta del estado Conectado si Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, vuelve a `SS_WebPort` o puerto 5000. |
| Select Installer... | Botón | Abre un selector de archivos que acepta `.msi` (instalador FlexRadio v4.2+ WiX), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI versus PE/COFF MZ) y extrae `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com y luego use este botón para colocarlo en fase. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para entrenamiento de APD para esa antena TX. Elija una entrada externa RX/XVTR cuando conduzca un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. Predeterminado: INTERNAL. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience desde el principio. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de colores de slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. |
| Botones de color de slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de colores y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y insignias de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Se admiten hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

Use los controles en la pestaña **Radio** para verificar e instalar actualizaciones de firmware.

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualización de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e le indica que descargue el instalador SmartSDR desde flexradio.com.
2. Descargue el instalador SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` preextraído. El gestor detecta el formato de archivo automáticamente y extrae el firmware sin herramientas externas. Un indicador de progreso aparece mientras se completa la colocación en fase.
4. Haga clic en **Upload Firmware** para transferir el firmware colocado en fase a la radio.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1 los controles de calibración en la pestaña **RX** están disponibles independientemente de si se instala un GPSDO. Anteriormente, **Cal Frequency (MHz):**,  **Start** y **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. La etiqueta de estado en la parte superior del grupo ahora lee:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Cómo funciona la calibración en v0.9.2.1

El botón **Start** ahora valida el campo de frecuencia de calibración antes de enviar cualquier comando, reinicia el error de frecuencia a cero (`radio set freq_error_ppb=0`), luego activa el barrido PLL. Mientras se ejecuta el barrido, **Start** se deshabilita y se etiqueta **Busy**. Una etiqueta de estado junto al botón muestra texto de progreso. El botón y la etiqueta vuelven a sus estados normales cuando el barrido se completa o falla.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Valida el campo, reinicia `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y se etiqueta **Busy** mientras un barrido está en progreso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado de calibración actual: Starting, texto de progreso o error. Se actualiza en vivo durante el barrido. |

## Consejos

- Cada transvertor obtiene su propia pestaña anidada dentro de la pestaña XVTR. Si tiene múltiples transvertores, use esas pestañas para cambiar entre entradas.
- Si necesita volver a este diálogo más tarde para ajustar un transvertor, reabra `Settings > Radio Setup...` y vaya directamente a la pestaña **XVTR**.
- En la pestaña **RX**, siempre ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):** antes de hacer clic en **Start**. Dejar el campo vacío cancela el barrido.
- Cuando **Check for Update** informa una nueva versión de firmware, descargue el instalador SmartSDR desde flexradio.com antes de hacer clic en **Select Installer...**. AetherSDR ya no descarga el instalador automáticamente.
- La pestaña **APD** aparece solo en radios FLEX-8x00 ejecutando SmartSDR 4.2.18 o posterior. Si no la ve, su modelo de radio o versión de firmware no admite APD configurable.
- Los colores de slice personalizados establecidos en la pestaña **Themes** se aplican inmediatamente a widgets VFO, superposiciones de panadapter e insignias de canal CAT. Seleccione **Use Aether defaults** y haga clic en **Reset All to Defaults** para volver a la paleta estándar.
- Para abrir la interfaz web de ShackSwitch, haga clic en **⚙ Web UI** en la fila ShackSwitch de la pestaña **Peripherals**. El botón utiliza el puerto web anunciado del dispositivo cuando está disponible; si la baliza no proporciona un puerto válido, vuelve a `SS_WebPort` o puerto 5000.
- La fila **Antenna Genius** oculta su estado Conectado cuando un ShackSwitch es el dispositivo activo. Use la fila **ShackSwitch** para administrar esa conexión en su lugar.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Establecer potencia TX máxima por banda y modo de sintonización](set-per-band-tx-max-power-and-tune-mode.md)
