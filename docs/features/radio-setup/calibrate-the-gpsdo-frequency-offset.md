# Calibrar el desplazamiento de frecuencia del GPSDO

Use esta página para corregir la referencia de frecuencia de su FLEX-8600 mediante los controles de calibración integrados. Una calibración de frecuencia precisa reduce el error de dial en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña RX en Radio Setup solo está disponible cuando hay una conexión de radio activa.
- Si hay un GPSDO instalado, los controles de calibración siguen disponibles. Sin un GPSDO, se muestra un mensaje de estado en amarillo en lugar de la confirmación verde del GPSDO.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia de precisión conocida.
4. Haga clic en **Start** para iniciar el barrido de calibración. La etiqueta del botón cambia a **Busy** y aparece un mensaje de estado mientras se ejecuta el barrido. El botón **Start** permanece deshabilitado hasta que el barrido se complete o falle.
5. Cuando el barrido se complete, revise el desplazamiento medido que se muestra en **Freq Offset (ppb):**.
6. Si prefiere establecer el desplazamiento manualmente en lugar de usar el resultado del barrido, edite **Freq Offset (ppb):** directamente.

## Qué hace cada control

| Control | Tipo | Descripción |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | La frecuencia de referencia utilizada durante el barrido de calibración. Establézcala en una señal de precisión conocida — por ejemplo, una emisora de frecuencia estándar de radiodifusión. El campo no debe estar vacío antes de hacer clic en **Start**; si está vacío, se muestra una advertencia y el barrido no se inicia. |
| **Start** | Botón | Inicia el barrido de calibración en la frecuencia ingresada en **Cal Frequency (MHz):**. Antes de iniciar, AetherSDR restablece el error de frecuencia actual a cero (`freq_error_ppb=0`) para que el barrido comience desde una línea base limpia. El botón se deshabilita y muestra **Busy** mientras el barrido está en curso. |
| **Freq Offset (ppb):** | Spinbox | El desplazamiento de frecuencia aplicado al oscilador de referencia del radio, en partes por mil millones. Puede ser establecido por el barrido o ingresado manualmente. |
| **10 MHz Reference Source:** | Combo box | Selecciona la fuente de referencia del oscilador. Valores válidos: `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al combo box y se actualiza en tiempo real. |
| **TX Follows Active Slice** | Botón | TX sigue al slice (canal de recepción) activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, desde WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Slider | Establece la nitidez del filtro (0 = menor latencia a 3 = máxima nitidez) por modo. El control deslizante se deshabilita cuando **Auto** está habilitado para ese modo. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que se interrumpió en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y el radio ya descubrió el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si el dispositivo conectado es un ShackSwitch (en lugar de un Antenna Genius). |
| **Connect / Disconnect (ShackSwitch)** | Botón | Abre o cierra una conexión a un conmutador de antenas ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo `ShackSwitch` en la baliza de difusión AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (no ShackSwitch). |
| **⚙ Web UI (ShackSwitch)** | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de autoextracción más antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en **Select Installer...** para prepararlo. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (tab)** | Pestaña | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y un botón de restablecimiento del ecualizador. La pestaña se oculta a menos que el radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; los radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Combo box | Selecciona la ruta de retroalimentación que el radio usa para muestrear la RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se cargan en tiempo real desde el sub-objeto `apd sampler` del radio. Regresa a `INTERNAL` si el radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. |
| **Themes (tab)** | Pestaña | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de colores de los slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. |
| **Botones de color Slice A–H** | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles inmediatamente en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Se admiten hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón | Restablece todos los colores personalizados de los slices a la paleta integrada de AetherSDR. |

## Mensajes de estado de la calibración

A partir de v0.9.2.1, aparece una etiqueta de estado junto al botón **Start** que se actualiza durante el barrido.

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Azul grisáceo | La secuencia de comandos de calibración ha sido enviada al radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Ingrese una frecuencia e intente nuevamente. |
| Busy | — | Se muestra en el propio botón **Start** mientras hay un barrido en curso. |

## Banner de estado del GPSDO

El banner en la parte superior del grupo de calibración refleja si hay un GPSDO instalado:

- **Banner verde** — El GPSDO está instalado. La calibración manual del desplazamiento de frecuencia sigue disponible.
- **Banner ámbar** — No hay GPSDO instalado. La calibración manual del desplazamiento de frecuencia está disponible.

En v0.9.2.1 cambió el texto del banner verde. Antes decía "GPSDO is installed. Frequency error correction is not required." Ahora dice "GPSDO installed. Manual frequency offset calibration available." Esto hace que el comportamiento sea consistente: los controles de calibración siempre se muestran independientemente de la presencia del GPSDO.

## Flujo de trabajo de actualización de firmware (v0.9.3)

En v0.9.3 cambió el flujo de actualización de firmware. AetherSDR ya no descarga ni prepara el firmware automáticamente cuando se detecta una actualización. En su lugar:

1. Haga clic en **Check for Update** en la pestaña **Radio**. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** (anteriormente etiquetado como **Browse .ssdr...**) y seleccione el archivo descargado. AetherSDR acepta `.msi`, `.exe` o un archivo `.ssdr` preextraído y prepara el firmware automáticamente, detectando el formato a partir del encabezado del archivo.
4. Una vez que la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware al radio.

El botón **Check for Update** ya no cambia su etiqueta para convertirse en un disparador de descarga después de detectar una actualización disponible.

## Interfaz web del ShackSwitch (v0.9.4)

En v0.9.4, se agregó un botón **⚙ Web UI** a la fila del ShackSwitch en la pestaña **Peripherals**. Haga clic en él para abrir la página de configuración local del dispositivo ShackSwitch en su navegador predeterminado del sistema.

Orden de resolución del puerto:

1. Si la baliza del ShackSwitch anuncia un `webPort` mayor que 1024, se usa ese puerto.
2. De lo contrario, se usa el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000 como alternativa.

El botón lee la IP desde `SS_ManualIp`. Si ese ajuste está vacío y hay un ShackSwitch actualmente conectado, se usa en su lugar la dirección del par activo. Si no se puede determinar ninguna IP, el botón no hace nada.

También en v0.9.4, la fila de **Antenna Genius** en la pestaña **Peripherals** ahora oculta correctamente su estado Connected cuando el dispositivo conectado a través del protocolo AG es un ShackSwitch (en lugar de un Antenna Genius real).

## Consejos

- Si tiene intención de usar una referencia externa de 10 MHz en lugar del GPSDO, establezca **10 MHz Reference Source:** en `External` antes de calibrar, para que el desplazamiento se aplique a la fuente correcta.
- El barrido restablece `freq_error_ppb` a cero antes de iniciar. Si tiene un desplazamiento ingresado manualmente que desea conservar, anótelo antes de hacer clic en **Start**.

## Relacionado

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
