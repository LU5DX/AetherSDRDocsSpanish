# Verificar el número de serie de la radio, versión de hardware, región y opciones

La pestaña Radio en Radio Setup muestra información identificativa reportada directamente por la radio — número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de resolver problemas o contactar soporte.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Los campos de la pestaña Radio se rellenan con datos en vivo de la radio.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por la radio.
   - **Region** — la región regulatoria de la radio (por defecto `USA` si la radio no reporta una).
   - **Options** — las opciones licenciadas activas en esta radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis tal como lo reporta la radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si la radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones de radio licenciadas. |
| TX Follows Active Slice | Botón de presión | TX sigue el slice activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante operación Split. |
| Active Slice Follows TX | Botón de presión | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. |
| Deslizadores de nitidez de filtro Voice / CW / Digital | Deslizador | Establece la nitidez del filtro (0=latencia más baja a 3=más aguda) por modo; el deslizador se deshabilita cuando Auto está habilitado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón de presión | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio rota en firmware 4.2. El TGXL controla PTT de la radio a través de su cable de bloqueo de hardware; no se necesita asignación de lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| Connect / Disconnect (PGXL) | Botón de presión | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón de presión | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra "Connected" solo cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. Si un ShackSwitch es el dispositivo conectado, el estado de esta fila está oculto. |
| Connect / Disconnect (ShackSwitch) | Botón de presión | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo UDP/TCP de AG en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de transmisión de AG. El descubrimiento automático a través de UDP también funciona sin esta fila. La fila muestra "Connected" solo cuando el dispositivo conectado se identifica como ShackSwitch; la fila está oculta del estado "Connected" si un Antenna Genius que no es ShackSwitch es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón de presión | Abre la interfaz web de configuración local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` del beacon si es mayor que 1024; de lo contrario, vuelve a `SS_WebPort` o al puerto 5000. El botón lee la IP de `SS_ManualIp` o, si está vacío, de la dirección de par activa cuando el dispositivo conectado es un ShackSwitch. |
| Select Installer... | Botón de presión | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato desde los primeros 8 bytes (números mágicos OLE/MSI frente a MZ de PE/COFF) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador externo de Adaptive Pre-Distortion — selección por antena de TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio usa para muestrear la RF saliente para entrenamiento de APD para esa antena de TX. Elija una entrada RX/XVTR externa cuando impulse un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón de presión | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color Slice A–H | Botón de presión | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asigne un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y badges de canal CAT. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón de presión | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. |

Los cuatro campos Radio Information son de solo lectura. No hay claves de configuración persistida asociadas con ellos.

## Pestaña Firmware — seleccionar un instalador o archivo de firmware (v0.9.3)

En v0.9.3 el botón **Browse .ssdr...** fue renombrado a **Select Installer...**. El botón ahora acepta el paquete de instalador SmartSDR completo además de un archivo `.ssdr` preextraído, así ya no necesita extraer el firmware manualmente antes de cargarlo.

**Para preparar firmware para carga:**

1. Haga clic en **Check for Update**. Si una actualización está disponible, la etiqueta de estado le instruye descargar el instalador SmartSDR desde flexradio.com.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2 y posteriores, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el archivo descargado, o elija un archivo `.ssdr` preextraído si tiene uno.
4. AetherSDR lee los primeros 8 bytes del archivo para detectar si es un paquete MSI, un EXE autoextraíble o un `.ssdr` sin procesar. La carga `.ssdr` se extrae automáticamente sin herramientas externas. El progreso se muestra en la barra de progreso y la etiqueta de estado.
5. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

> **Nota:** En versiones anteriores a v0.9.3, hacer clic en **Check for Update** cuando una actualización estaba disponible convertía el botón en un botón **Download vX.Y.Z** que descargaba y preparaba el firmware automáticamente. Ese comportamiento ha sido removido. Debe descargar el instalador desde flexradio.com usted mismo y luego usar **Select Installer...** para prepararlo.

## Pestaña RX — calibración de frecuencia

En v0.9.2.1 los controles de calibración en la pestaña **RX** siempre son visibles independientemente de si un GPSDO está instalado. Anteriormente, los campos Cal Frequency, Start y Freq Offset estaban ocultos cuando un GPSDO era detectado. El banner de estado en la parte superior del grupo ahora lee:

- **GPSDO installed** — "GPSDO installed. Manual frequency offset calibration available." (texto verde)
- **No GPSDO** — "Manual frequency offset calibration available." (texto ámbar)

Los siguientes controles están ahora disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Spinbox | Frecuencia usada para calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón de presión | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en progreso. Antes de activar el barrido de PLL, AetherSDR restablece el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no toma acción. |
| Freq Offset (ppb): | Spinbox | Compensación manual de frecuencia en partes por mil millones, aplicada después de que se complete la calibración o establecida directamente para corrección manual. |

Una etiqueta de estado aparece a la derecha del botón Start y se actualiza durante toda la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Inactivo | *(vacío)* | — |
| Frecuencia cal no ingresada | "Enter cal frequency" | Ámbar |
| Secuencia iniciada | "Starting…" | Gris-azul |
| En progreso | Se actualiza a medida que el estado de PLL es reportado por la radio | Gris-azul |

El botón Start se vuelve a habilitar y su etiqueta revierte a **Start** cuando la secuencia de calibración se completa o falla.

## Pestaña Peripherals — interfaz web de ShackSwitch (v0.9.4)

En v0.9.4 la pestaña Peripherals agrega un botón **⚙ Web UI** dedicado junto a la fila de ShackSwitch. Haga clic en él para abrir la página web de configuración incorporada del dispositivo ShackSwitch en su navegador del sistema.

El botón determina la URL de la siguiente manera:

1. Si el ShackSwitch está actualmente conectado y su beacon de descubrimiento anuncia un `webPort` mayor que 1024, se usa ese puerto.
2. De lo contrario se usa la configuración `SS_WebPort` almacenada.
3. Si ninguno está disponible, se usa el puerto 5000 como respaldo.

La dirección IP se toma de `SS_ManualIp`. Si ese campo está vacío y el dispositivo conectado es un ShackSwitch, se usa la dirección de par activa. El botón no toma acción si no se puede determinar ninguna dirección IP.

También en v0.9.4, la fila **Connect / Disconnect (Antenna Genius)** ahora oculta su estado "Connected" cuando un ShackSwitch es el dispositivo realmente conectado a través del modelo Antenna Genius. La fila de ShackSwitch muestra "Connected" en ese caso.

**Para abrir la interfaz web de ShackSwitch:**

1. Haga clic en `Settings > Radio Setup...`.
2. Seleccione la pestaña **Peripherals**.
3. Asegúrese de que el ShackSwitch esté conectado (la fila ShackSwitch muestra "Connected").
4. Haga clic en **⚙ Web UI**. Su navegador predeterminado abre la página de configuración del dispositivo.

## Consejos

- Si **Radio SN** está en blanco, la radio aún no ha enviado su número de serie del chasis. Desconéctese y reconéctese a la radio.
- **Options** refleja lo que la radio misma reporta. Si recientemente ha comprado una licencia
