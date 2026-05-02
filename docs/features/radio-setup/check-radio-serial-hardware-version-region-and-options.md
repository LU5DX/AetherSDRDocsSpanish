# Verificar número de serie, versión de hardware, región y opciones del radio

La pestaña **Radio** en Radio Setup muestra información de identificación reportada directamente por el radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de realizar diagnósticos o contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los campos de la pestaña **Radio** se llenan con datos del radio en tiempo real.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por el radio.
   - **Region** — la región regulatoria del radio (muestra `USA` por defecto si el radio no reporta ninguna).
   - **Options** — las opciones licenciadas activas en este radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis tal como lo reporta el radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si el radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones licenciadas del radio. |
| TX Follows Active Slice | Botón | El TX sigue al slice (canal de recepción) activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=menor latencia hasta 3=máxima nitidez) por modo; el control se deshabilita cuando Auto está activo. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y el radio ha detectado el TGXL, la IP detectada se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra "Connected" únicamente cuando el dispositivo conectado es un Antenna Genius que no es ShackSwitch. Si el dispositivo conectado es un ShackSwitch, el estado de esta fila queda oculto. |
| Connect / Disconnect (ShackSwitch) | Botón | Abre o cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta mediante el campo `ShackSwitch` en el beacon de difusión AG. El autodescubrimiento vía UDP también funciona sin esta fila. La fila muestra "Connected" únicamente cuando el dispositivo conectado se identifica como ShackSwitch; el estado "Connected" de la fila queda oculto si el dispositivo conectado es un Antenna Genius que no es ShackSwitch. |
| ⚙ Web UI (ShackSwitch) | Botón | Abre la interfaz de configuración web local del ShackSwitch en el navegador del sistema. Usa el `webPort` del beacon si es mayor que 1024; de lo contrario, usa `SS_WebPort` o el puerto 5000. El botón lee la IP desde `SS_ManualIp` o, si está vacío, desde la dirección del par en vivo cuando el dispositivo conectado es un ShackSwitch. |
| Select Installer... | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble más antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic frente a PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. La etiqueta cambió de **Browse .ssdr...** en la v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón para reiniciar el ecualizador. La pestaña está oculta a menos que el radio reporte `apd configurable=1`. Solo los radios de la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; los radios de la serie 6000 y los anteriores a 4.2.18 mantienen la pestaña invisible. |
| Controles combinados ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que el radio usa para muestrear la RF saliente en el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando use un amplificador lineal externo. Las opciones se llenan en tiempo real desde el subobjeto `apd sampler` del radio. Vuelve a INTERNAL si el radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color para los slices A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios se ven de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. |

Los cuatro campos de Radio Information son de solo lectura. No hay claves de configuración persistentes asociadas a ellos.

## Pestaña Firmware — seleccionar un instalador o archivo de firmware (v0.9.3)

En la v0.9.3 el botón **Browse .ssdr...** pasó a llamarse **Select Installer...**. El botón ahora acepta el paquete instalador completo de SmartSDR además de un archivo `.ssdr` ya extraído, por lo que ya no es necesario extraer el firmware manualmente antes de cargarlo.

**Para preparar el firmware para la carga:**

1. Haga clic en **Check for Update**. Si hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2 y versiones posteriores, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el archivo descargado, o elija un archivo `.ssdr` ya extraído si dispone de uno.
4. AetherSDR lee los primeros 8 bytes del archivo para detectar si es un paquete MSI, un EXE autoextraíble o un `.ssdr` sin procesar. El contenido `.ssdr` se extrae automáticamente sin herramientas externas. El progreso se muestra en la barra de progreso y en la etiqueta de estado.
5. Cuando la preparación finalice, haga clic en **Upload Firmware** para transferir el firmware al radio.

> **Nota:** En versiones anteriores a la v0.9.3, al hacer clic en **Check for Update** cuando había una actualización disponible, el botón se convertía en **Download vX.Y.Z** y descargaba y preparaba el firmware automáticamente. Ese comportamiento ha sido eliminado. Debe descargar el instalador desde flexradio.com usted mismo y luego usar **Select Installer...** para prepararlo.

## Pestaña RX — calibración de frecuencia

En la v0.9.2.1 los controles de calibración de la pestaña **RX** son siempre visibles, independientemente de si hay un GPSDO instalado. Anteriormente, los campos Cal Frequency, Start y Freq Offset estaban ocultos cuando se detectaba un GPSDO. El banner de estado en la parte superior del grupo ahora muestra:

- **GPSDO instalado** — "GPSDO installed. Manual frequency offset calibration available." (texto en verde)
- **Sin GPSDO** — "Manual frequency offset calibration available." (texto en ámbar)

Los siguientes controles están ahora disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Cuadro de número | Frecuencia utilizada para la calibración. Introduzca la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en curso. Antes de activar el barrido PLL, AetherSDR restablece el error de frecuencia del radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Cuadro de número | Desplazamiento de frecuencia manual en partes por mil millones, aplicado después de que la calibración finaliza o establecido directamente para corrección manual. |

Una etiqueta de estado aparece a la derecha del botón Start y se actualiza a lo largo de la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Inactivo | *(vacío)* | — |
| Frecuencia de calibración no ingresada | "Enter cal frequency" | Ámbar |
| Secuencia iniciada | "Starting…" | Azul grisáceo |
| En progreso | Se actualiza según el estado del PLL reportado por el radio | Azul grisáceo |

El botón Start se vuelve a habilitar y su etiqueta vuelve a **Start** cuando la secuencia de calibración finaliza o falla.

## Pestaña Peripherals — interfaz web del ShackSwitch (v0.9.4)

En la v0.9.4 la pestaña Peripherals agrega un botón dedicado **⚙ Web UI** junto a la fila de ShackSwitch. Haga clic en él para abrir la página web de configuración integrada del ShackSwitch en su navegador predeterminado.

El botón determina la URL de la siguiente manera:

1. Si el ShackSwitch está conectado actualmente y su beacon de descubrimiento anuncia un `webPort` mayor que 1024, se usa ese puerto.
2. De lo contrario, se usa la configuración almacenada en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000 como alternativa.

La dirección IP se toma de `SS_ManualIp`. Si ese campo está vacío y el dispositivo conectado es un ShackSwitch, se usa en su lugar la dirección del par en vivo. El botón no realiza ninguna acción si no se puede determinar ninguna dirección IP.

También en la v0.9.4, la fila **Connect / Disconnect (Antenna Genius)** ahora oculta su estado "Connected" cuando el dispositivo realmente conectado a través del modelo Antenna Genius es un ShackSwitch. En ese caso, la fila de ShackSwitch muestra "Connected".

**Para abrir la interfaz web del ShackSwitch:**

1. Haga clic en `Settings > Radio Setup...`.
2. Seleccione la pestaña **Peripherals**.
3. Asegúrese de que el ShackSwitch esté conectado (la fila de ShackSwitch muestra "Connected").
4. Haga clic en **⚙ Web UI**. Su navegador predeterminado abre la página de configuración del dispositivo.

## Consejos

- Si **Radio SN** está en blanco, el radio aún no ha enviado su número de serie del chasis. Desconéctese y vuelva a conectarse al radio.
- **Options** refleja lo que el radio reporta. Si ha adquirido recientemente una licencia
