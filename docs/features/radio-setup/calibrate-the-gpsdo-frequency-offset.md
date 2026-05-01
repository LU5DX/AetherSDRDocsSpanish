# Calibre el desplazamiento de frecuencia del GPSDO

Use esta página para corregir la referencia de frecuencia de su FLEX-8600 mediante los controles de calibración integrados. Una calibración de frecuencia precisa reduce el error de marcación en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña RX en Radio Setup solo está disponible cuando hay una conexión activa a la radio.
- Si un GPSDO está instalado, los controles de calibración siguen disponibles. Sin un GPSDO, se muestra un mensaje de estado amarillo en lugar de la confirmación verde del GPSDO.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):** ingrese la frecuencia de una señal de referencia conocida y precisa.
4. Haga clic en **Start** para comenzar el barrido de calibración. La etiqueta del botón cambia a **Busy** y aparece un mensaje de estado mientras se ejecuta el barrido. El botón **Start** se desactiva hasta que el barrido se complete o falle.
5. Cuando el barrido se complete, revise el desplazamiento medido que se muestra en **Freq Offset (ppb):**
6. Si prefiere establecer el desplazamiento manualmente en lugar de usar el resultado del barrido, edite **Freq Offset (ppb):** directamente.

## Qué hace cada control

| Control | Tipo | Descripción |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | La frecuencia de referencia utilizada durante el barrido de calibración. Establézcala en una señal conocida y precisa, por ejemplo, una estación de radiodifusión de frecuencia de referencia. El campo no debe estar vacío antes de hacer clic en **Start**; si está vacío, se muestra una advertencia y el barrido no comienza. |
| **Start** | Botón de acción | Inicia el barrido de calibración en la frecuencia ingresada en **Cal Frequency (MHz):**. Antes de comenzar, AetherSDR reinicia el error de frecuencia actual a cero (`freq_error_ppb=0`) para que el barrido comience desde una línea de base limpia. El botón se desactiva y muestra **Busy** mientras el barrido está en progreso. |
| **Freq Offset (ppb):** | Spinbox | El desplazamiento de frecuencia aplicado al oscilador de referencia de la radio, en partes por mil millones. Puede establecerse mediante el barrido o ingresarse manualmente. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de oscilador de referencia. Valores válidos: `Auto` \| `TCXO` \| `GPSDO` \| `External`. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en tiempo real. |
| **TX Follows Active Slice** | Botón de acción | TX sigue la porción (slice) activa. Mutuamente excluyente con **Active Slice Follows TX**. Se desactiva automáticamente durante la operación de Split. |
| **Active Slice Follows TX** | Botón de acción | Cambia la porción activa cuando TX se mueve externamente (por ejemplo, desde WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. |
| **Deslizadores de nitidez de filtro Voice / CW / Digital** | Deslizador | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El deslizador se desactiva cuando **Auto** está habilitado para ese modo. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo y desactiva el deslizador de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón de acción | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio interrumpida en firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interlock de hardware; no se requiere activación del lado del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se completa previamente. |
| **Connect / Disconnect (PGXL)** | Botón de acción | Abre o cierra una conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón de acción | Abre o cierra una conexión a Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (en lugar de una Antenna Genius) es el dispositivo conectado. |
| **Connect / Disconnect (ShackSwitch)** | Botón de acción | Abre o cierra una conexión a un conmutador de antena ShackSwitch mediante el protocolo UDP/TCP de AG en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo `ShackSwitch` en el beacon de difusión de AG. La detección automática mediante UDP también funciona sin esta fila. La fila se oculta del estado Connected si una Antenna Genius (que no sea ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Botón de acción | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del beacon si es mayor que 1024, de lo contrario recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón de acción | Abre un selector de archivos que acepta instalador WiX de FlexRadio v4.2+ (`.msi`), instalador autoextraíble más antiguo (`.exe`) o archivo de firmware `.ssdr` preextraído. El almacenador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en **Select Installer...** para prepararlo. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (pestaña)** | Pestaña | Configuración del muestreador de predistorsión adaptativa externa (Adaptive Pre-Distortion): selección por antena TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y anteriores a la 4.2.18 mantienen la pestaña invisible. |
| **Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Cuadro combinado | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente para entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando conduzca un amplificador lineal externo. Las opciones se rellenan en directo desde el subobjeto `apd sampler` de la radio. Recurre a `INTERNAL` si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón de acción | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience desde cero. |
| **Themes (pestaña)** | Pestaña | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. |
| **Use Aether defaults / Custom colors** | Botón de opción | Alterna el esquema de color de la porción entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por porción. |
| **Botones de color Slice A–H** | Botón de acción | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa porción. Los cambios son visibles inmediatamente en widgets de VFO, superposiciones de panadapter e insignias de canal CAT. Los botones se desactivan cuando se selecciona **Use Aether defaults**. Se soportan hasta 8 porciones. |
| **Reset All to Defaults (Themes)** | Botón de acción | Reinicia todos los colores personalizados de la porción a la paleta integrada de AetherSDR. |

## Mensajes de estado de calibración

A partir de v0.9.2.1, una etiqueta de estado aparece junto al botón **Start** y se actualiza durante todo el barrido.

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Gris azulado | La secuencia de comando de calibración se ha enviado a la radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Ingrese una frecuencia e intente nuevamente. |
| Busy | — | Se muestra en el botón **Start** mismo mientras un barrido está en progreso. |

## Banner de estado del GPSDO

El banner en la parte superior del grupo de calibración refleja si un GPSDO está instalado:

- **Banner verde** — GPSDO está instalado. La calibración manual de desplazamiento de frecuencia sigue disponible.
- **Banner ámbar** — Sin GPSDO instalado. La calibración manual de desplazamiento de frecuencia está disponible.

En v0.9.2.1 el texto del banner verde cambió. Anteriormente decía "GPSDO is installed. Frequency error correction is not required." Ahora dice "GPSDO installed. Manual frequency offset calibration available." Esto hace que el comportamiento sea consistente: los controles de calibración siempre se muestran independientemente de la presencia del GPSDO.

## Flujo de actualización de firmware (v0.9.3)

En v0.9.3 el flujo de actualización de firmware cambió. AetherSDR ya no descarga y prepara el firmware automáticamente cuando se detecta una actualización. En su lugar:

1. Haga clic en **Check for Update** en la pestaña **Radio**. Si una actualización está disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones más antiguas).
3. Haga clic en **Select Installer...** (etiquetado anteriormente como **Browse .ssdr...**) y elija el archivo descargado. AetherSDR acepta archivos `.msi`, `.exe` o un archivo `.ssdr` preextraído y prepara el firmware automáticamente, detectando el formato del encabezado del archivo.
4. Una vez que se complete la preparación, haga clic en **Upload Firmware** para transferir el firmware a la radio.

El botón **Check for Update** ya no se renombra a sí mismo como activador de descarga después de detectar una actualización disponible.

## Interfaz web de ShackSwitch (v0.9.4)

En v0.9.4 se agregó un botón **⚙ Web UI** a la fila ShackSwitch en la pestaña **Peripherals**. Haga clic en él para abrir la página de configuración local del dispositivo ShackSwitch en su navegador predeterminado del sistema.

Orden de resolución de puertos:

1. Si el beacon de ShackSwitch anuncia un `webPort` mayor que 1024, se utiliza ese puerto.
2. De lo contrario, se utiliza el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, el puerto 5000 se utiliza como alternativa.

El botón lee la IP desde `SS_ManualIp`. Si esa configuración está vacía y un ShackSwitch está actualmente conectado, se utiliza la dirección de par en tiempo real. Si no se puede determinar ninguna IP, el botón no hace nada.

También en v0.9.4, la fila **Antenna Genius** en la pestaña **Peripherals** ahora oculta correctamente su estado de Connected cuando un ShackSwitch (en lugar de una verdadera Antenna Genius) es el dispositivo realmente conectado a través de la pila de protocolos de AG.

## Consejos

- Si intenta usar una referencia externa de 10 MHz en lugar del GPSDO, establezca **10 MHz Reference Source:** en `External` antes de calibrar, para que el desplazamiento se aplique a la fuente correcta.
- El barrido reinicia `freq_error_ppb` a cero antes de comenzar. Si tiene un desplazamiento ingresado manualmente que desea preservar, anótelo antes de hacer clic en **Start**.

## Relacionado

- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Descripción general de Radio Setup](overview.md)
