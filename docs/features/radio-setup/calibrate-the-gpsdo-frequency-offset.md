# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para corregir la referencia de frecuencia de su FLEX-8600 mediante los controles de calibración incorporados. Una calibración de frecuencia precisa reduce el error de dial en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña RX en Radio Setup solo está disponible cuando hay una conexión de radio activa.
- Si hay un GPSDO instalado, los controles de calibración siguen estando disponibles. Sin un GPSDO, se muestra un mensaje de estado amarillo en lugar de la confirmación verde del GPSDO.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia de precisión conocida.
4. Haga clic en **Start** para iniciar el barrido de calibración. La etiqueta del botón cambia a **Busy** y aparece un mensaje de estado mientras se ejecuta el barrido. El botón **Start** está deshabilitado hasta que el barrido se complete o falle.
5. Cuando el barrido se complete, revise el desplazamiento medido que se muestra en **Freq Offset (ppb):**
6. Si prefiere establecer el desplazamiento manualmente en lugar de usar el resultado del barrido, edite **Freq Offset (ppb):** directamente.

## Qué hace cada control

| Control | Tipo | Descripción |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | La frecuencia de referencia utilizada durante el barrido de calibración. Establézcala en una señal de precisión conocida — por ejemplo, una estación de transmisión de frecuencia patrón. El campo no debe estar vacío antes de hacer clic en **Start**; si está vacío, se muestra una advertencia y el barrido no comienza. |
| **Start** | Botón de acción | Inicia el barrido de calibración en la frecuencia ingresada en **Cal Frequency (MHz):**. Antes de comenzar, AetherSDR reinicia el error de frecuencia actual a cero (`freq_error_ppb=0`) para que el barrido comience desde una línea de base limpia. El botón está deshabilitado y muestra **Busy** mientras el barrido está en progreso. |
| **Freq Offset (ppb):** | Spinbox | El desplazamiento de frecuencia aplicado al oscilador de referencia de la radio, en partes por mil millones. Puede establecerse mediante el barrido o ingresarse manualmente. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador. Valores válidos: `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en vivo. |
| **TX Follows Active Slice** | Botón de acción | TX sigue el slice activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante operación Split. |
| **Active Slice Follows TX** | Botón de acción | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, desde WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Controles deslizantes de agudeza de filtro Voice / CW / Digital** | Control deslizante | Establece la agudeza del filtro (0 = latencia más baja a 3 = más agudo) por modo. El control deslizante está deshabilitado cuando **Auto** está habilitado para ese modo. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternar | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de agudeza manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón de acción | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita cifrado del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Botón de acción | Abre o cierra una conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón de acción | Abre o cierra una conexión a Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |
| **Select Installer...** | Botón de acción | Abre un selector de archivos que acepta instaladores WiX `.msi` (FlexRadio v4.2+), instaladores autoextraíbles `.exe` (más antiguos) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato de los primeros 8 bytes (magia OLE/MSI frente a MZ PE/COFF) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le instruye descargar el instalador SmartSDR de flexradio.com y luego hacer clic en **Select Installer...** para prepararlo. Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y pre-4.2.18 mantienen la pestaña invisible. |
| **Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Cuadro combinado | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear el RF saliente para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Se retrocede a `INTERNAL` si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón de acción | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. |
| **Themes (tab)** | Pestaña | Pestaña de personalización de la interfaz — actualmente alberga la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. |
| **Botones de color para Slice A–H** | Botón de acción | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando se selecciona **Use Aether defaults**. Hasta 8 slices soportados. |
| **Reset All to Defaults (Themes)** | Botón de acción | Reinicia todos los colores de slice personalizados a la paleta incorporada de AetherSDR. |

## Mensajes de estado de calibración

A partir de v0.9.2.1, una etiqueta de estado aparece junto al botón **Start** y se actualiza durante todo el barrido.

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Gris azulado | La secuencia de comandos de calibración ha sido enviada a la radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Ingrese una frecuencia e intente nuevamente. |
| Busy | — | Se muestra en el botón **Start** mismo mientras un barrido está en progreso. |

## Banner de estado del GPSDO

El banner en la parte superior del grupo de calibración refleja si hay un GPSDO instalado:

- **Banner verde** — GPSDO está instalado. La calibración manual del desplazamiento de frecuencia sigue estando disponible.
- **Banner ámbar** — No hay GPSDO instalado. La calibración manual del desplazamiento de frecuencia está disponible.

En v0.9.2.1, la redacción del banner verde cambió. Anteriormente decía "GPSDO is installed. Frequency error correction is not required." Ahora dice "GPSDO installed. Manual frequency offset calibration available." Esto hace que el comportamiento sea consistente: los controles de calibración siempre se muestran independientemente de la presencia de GPSDO.

## Flujo de actualización de firmware (v0.9.3)

En v0.9.3, el flujo de actualización de firmware cambió. AetherSDR ya no descarga y prepara el firmware automáticamente cuando se detecta una actualización. En su lugar:

1. Haga clic en **Check for Update** en la pestaña **Radio**. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e le instruye descargar el instalador SmartSDR de flexradio.com.
2. Descargue el instalador de flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones más antiguas).
3. Haga clic en **Select Installer...** (previamente etiquetado como **Browse .ssdr...**) y elija el archivo descargado. AetherSDR acepta archivos `.msi`, `.exe` o `.ssdr` preextraído y prepara el firmware automáticamente, detectando el formato del encabezado del archivo.
4. Una vez que se complete la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio.

El botón **Check for Update** ya no se cambia de etiqueta a sí mismo como disparador de descarga después de detectar una actualización disponible.

## Consejos

- Si tiene la intención de usar una referencia externa de 10 MHz en lugar del GPSDO, establezca **10 MHz Reference Source:** en `External` antes de calibrar, para que el desplazamiento se aplique a la fuente correcta.
- El barrido reinicia `freq_error_ppb` a cero antes de comenzar. Si tiene un desplazamiento ingresado manualmente que desea preservar, anótelo antes de hacer clic en **Start**.

## Relacionado

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
