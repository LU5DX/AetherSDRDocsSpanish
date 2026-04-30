# Verificar número de serie de la radio, versión de hardware, región y opciones

La pestaña Radio en Radio Setup muestra información de identificación reportada directamente por la radio — número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de solucionar problemas o contactar al soporte.

## Antes de comenzar

- AetherSDR debe estar conectada a la radio. Los campos de la pestaña Radio se rellenan desde datos de radio en vivo.

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
| TX Follows Active Slice | Botón de acción | TX sigue el slice activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante operación Split. |
| Active Slice Follows TX | Botón de acción | Cambia el slice activo cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. |
| Deslizadores de nitidez de filtro Voice / CW / Digital | Deslizador | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador se deshabilita cuando se habilita Auto. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón de acción | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio rota en firmware 4.2. El TGXL controla PTT de radio a través de su cable de interlock de hardware; no se necesita keying del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| Connect / Disconnect (PGXL) | Botón de acción | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón de acción | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. |
| Select Installer... | Botón de acción | Abre un selector de archivos que acepta instalador WiX `.msi` (FlexRadio v4.2+), instalador auto-extraíble `.exe` (versiones antiguas) o archivo de firmware `.ssdr` pre-extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador de Pre-Distorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio de ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios de serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. |
| Equalizer Reset (APD) | Botón de acción | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de radio | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. Respaldado por `SliceColorManager::useCustomColors()`. |
| Botones de color del slice A–H | Botón de acción | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, overlays de panadapter y insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón de acción | Reinicia todos los colores de slice personalizados a la paleta incorporada de AetherSDR. |

Los cuatro campos Radio Information son de solo lectura. No hay claves de configuración persistentes asociadas con ellos.

## Pestaña Firmware — seleccionar un instalador o archivo de firmware (v0.9.3)

En v0.9.3 el botón **Browse .ssdr...** fue renombrado a **Select Installer...**. El botón ahora acepta el paquete instalador SmartSDR completo además de un archivo `.ssdr` pre-extraído, de modo que ya no necesita extraer el firmware manualmente antes de cargarlo.

**Para preparar firmware para carga:**

1. Haga clic en **Check for Update**. Si hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2 y posterior, `.exe` para versiones antiguas).
3. Haga clic en **Select Installer...** y elija el archivo descargado, o elija un archivo `.ssdr` pre-extraído si tiene uno.
4. AetherSDR lee los primeros 8 bytes del archivo para detectar si es un paquete MSI, un EXE auto-extraíble o un `.ssdr` sin procesar. La carga `.ssdr` se extrae automáticamente sin herramientas externas. El progreso se muestra en la barra de progreso y la etiqueta de estado.
5. Cuando se completa la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio.

> **Nota:** En versiones anteriores a v0.9.3, hacer clic en **Check for Update** cuando había una actualización disponible convertía el botón en un botón **Download vX.Y.Z** que descargaba y preparaba el firmware automáticamente. Ese comportamiento ha sido eliminado. Debe descargar el instalador desde flexradio.com usted mismo y luego usar **Select Installer...** para prepararlo.

## Pestaña RX — calibración de frecuencia

En v0.9.2.1 los controles de calibración en la pestaña **RX** siempre están visibles independientemente de si está instalado un GPSDO. Anteriormente, los campos Cal Frequency, Start y Freq Offset estaban ocultos cuando se detectaba un GPSDO. El banner de estado en la parte superior del grupo ahora lee:

- **GPSDO installed** — "GPSDO installed. Manual frequency offset calibration available." (texto verde)
- **No GPSDO** — "Manual frequency offset calibration available." (texto ámbar)

Los siguientes controles ahora están disponibles en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Cuadro giratorio | Frecuencia utilizada para calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón de acción | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en progreso. Antes de activar el barrido PLL, AetherSDR reinicia el error de frecuencia de la radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no toma acción. |
| Freq Offset (ppb): | Cuadro giratorio | Desplazamiento de frecuencia manual en partes por billón, aplicado después de que se completa la calibración o establecido directamente para corrección manual. |

Una etiqueta de estado aparece a la derecha del botón Start y se actualiza durante la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Idle | *(vacío)* | — |
| Frequency de calibración no ingresada | "Enter cal frequency" | Ámbar |
| Secuencia iniciada | "Starting…" | Gris-azul |
| En progreso | Actualizado a medida que el radio reporta el estado PLL | Gris-azul |

El botón Start se re-habilita y su etiqueta revierte a **Start** cuando la secuencia de calibración se completa o falla.

## Consejos

- Si **Radio SN** está en blanco, la radio aún no ha enviado su número de serie de chasis. Desconecte y reconecte a la radio.
- **Options** refleja lo que reporta la radio misma. Si ha comprado recientemente una actualización de licencia, apague la radio y reconecte para que obtenga las opciones actualizadas.
- Al ejecutar calibración, asegúrese de que la señal de referencia esté presente en la entrada de antena y que **Cal Frequency (MHz)** coincida exactamente con la frecuencia del transmisor de referencia antes de hacer clic en **Start**.
- La pestaña **APD** aparece solo en radios FLEX-8x00 ejecutando SmartSDR 4.2.18 o posterior. Si no ve la pestaña, su modelo de radio o versión de firmware no admite APD configurable.
- Para personalizar colores de slice, abra la pestaña **Themes**, seleccione **Custom colors** y luego haga clic en el botón con letra para cada slice que desee cambiar.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Establecer el apodo, indicativo y nombre de la estación de la radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr a la radio](upload-a-new-firmware-ssdr-to-the-radio.md)
