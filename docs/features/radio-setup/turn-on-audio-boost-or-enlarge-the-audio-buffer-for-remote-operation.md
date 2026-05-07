# Activar la amplificación de audio o aumentar el búfer de audio para operación remota

Use estas configuraciones para compensar el volumen de recepción bajo o la pérdida de audio al operar AetherSDR a través de una conexión VPN o SmartLink. La amplificación de audio agrega ganancia adicional en la ruta de audio del cliente; un búfer de audio más grande absorbe la fluctuación de la red a costa de una mayor latencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Estos controles no están disponibles cuando no hay una radio conectada.
- Abra `Settings > Radio Setup...` y seleccione la pestaña **Audio** antes de seguir los pasos a continuación.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el volumen de recepción, haga clic en **Audio Boost:** para activarlo. El botón muestra su estado activo cuando está habilitado.
4. Para reducir la pérdida o interrupción de audio, haga clic en el control de número **Audio Buffer:** e introduzca un valor entre 50 y 1000 ms. Los valores más altos agregan más almacenamiento en búfer a costa de la latencia.
5. Cierre el cuadro de diálogo. Los cambios surten efecto de inmediato.

## Qué hace cada control

| Control | Qué hace | Rango válido |
|---|---|---|
| **Audio Boost:** | Activa una ganancia adicional en la ruta de audio del cliente. | Activo / Inactivo |
| **Audio Buffer:** | Establece el búfer de audio del lado del cliente para absorber la fluctuación de la red. Auméntelo cuando use conexiones VPN o SmartLink con latencia inestable. | 50–1000 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto / Uncompressed / Opus |
| **TX Follows Active Slice** | El TX sigue al slice activo. Es mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante la operación en Split. | Activo / Inactivo |
| **Active Slice Follows TX** | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con TX Follows Active Slice. | Activo / Inactivo |
| **Controles deslizantes de nitidez del filtro Voice / CW / Digital** | Establece la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo; el control deslizante está deshabilitado cuando Auto está activado. | 0–3 |
| **Auto (Voice / CW / Digital)** | Activa la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | Activo / Inactivo |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa con el TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que está rota en el firmware 4.2. El TGXL activa el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita activación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. | — |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa con el Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión con el Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (en lugar de un Antenna Genius) es el dispositivo actualmente conectado. | — |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión con un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo 'ShackSwitch' en el beacon de difusión de AG. El descubrimiento automático a través de UDP también funciona sin esta fila. La fila se oculta del estado Connected si Antenna Genius (no ShackSwitch) es el dispositivo conectado. | — |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el webPort del beacon si es > 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble antiguo) o un archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI vs MZ PE/COFF) y extrae el .ssdr sin herramientas externas. Este botón se denominaba **Browse .ssdr...** antes de v0.9.3. | — |
| **APD (pestaña)** | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento de APD para esa antena TX. Elija una entrada RX/XVTR externa cuando se acciona un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. | INTERNAL / RX_A / RX_B / XVTA / XVTB |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento de APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz de usuario — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color del slice entre la paleta integrada de AetherSDR y un conjunto completamente personalizable por slice. | Use Aether defaults / Custom colors |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles de inmediato en los widgets de VFO, superposiciones del panadapter e insignias de canal CAT. Los botones están deshabilitados cuando está seleccionado **Use Aether defaults**. Se admiten hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — |

## Pestaña Peripherals — Interfaz web de ShackSwitch (cambio en v0.9.4)

En v0.9.4, la pestaña Peripherals agrega un botón **⚙ Web UI** en la fila de ShackSwitch. Al hacer clic, se abre la interfaz de configuración web integrada del dispositivo ShackSwitch en su navegador del sistema.

El botón determina la URL de la siguiente manera:

1. Si el ShackSwitch está actualmente conectado y su beacon de descubrimiento anuncia un `webPort` mayor de 1024, se utiliza ese puerto.
2. De lo contrario, se utiliza el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se utiliza el puerto 5000 como recurso.

La dirección IP se toma de `SS_ManualIp` si está configurada. Si ese campo está vacío y el dispositivo actualmente conectado es un ShackSwitch, se utiliza la dirección del par en vivo. El botón no hace nada si no se puede resolver una dirección IP.

La fila de Antenna Genius también recibe un pequeño cambio de comportamiento en v0.9.4: cuando un ShackSwitch es el dispositivo conectado, la fila de Antenna Genius ya no muestra un estado Connected, manteniendo las dos filas visualmente distintas.

### Cómo abrir la interfaz web de ShackSwitch

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Confirme que la fila de ShackSwitch muestra **Connected**. Si no es así, introduzca la IP del dispositivo y haga clic en **Connect**.
4. Haga clic en **⚙ Web UI**. Su navegador predeterminado abre la página de configuración de ShackSwitch.

> **Nota:** Si su ShackSwitch utiliza un puerto web no estándar, configúrelo manualmente en `SS_WebPort` antes de hacer clic en **⚙ Web UI**.

## Actualización de firmware — selección de un instalador (cambio en v0.9.3)

En v0.9.3, el flujo de trabajo de preparación de firmware cambió. El botón anteriormente etiquetado como **Browse .ssdr...** ahora se llama **Select Installer...**. El selector de archivos ahora acepta el paquete completo del instalador de SmartSDR además de un archivo .ssdr preextraído.

Cuando **Check for Update** detecta una versión de firmware más reciente, AetherSDR ya no la descarga automáticamente. En su lugar, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego use **Select Installer...** para prepararlo.

### Cómo preparar y cargar firmware

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com en su computadora (.msi para v4.2+, .exe para versiones anteriores).
5. Haga clic en **Select Installer...**. En el selector de archivos, seleccione el archivo .msi, .exe o .ssdr descargado y haga clic en **Open**. La etiqueta de estado muestra **Preparing firmware from \<nombre de archivo\>...** y aparece una barra de progreso mientras el preparador extrae el firmware.
6. Cuando la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y una etiqueta de estado siguen la carga.

> **Nota:** Si ya tiene un archivo .ssdr preextraído, puede seleccionarlo directamente en el paso 5. El preparador detecta el formato automáticamente.

## Pestaña RX — calibración de frecuencia

En v0.9.2.1, la sección de calibración de la pestaña RX fue revisada. El campo **Cal Frequency (MHz):** y el botón **Start** ahora son siempre visibles, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado lo confirma en verde; cuando no hay ningún GPSDO instalado, la etiqueta aparece en ámbar. Ambos casos permiten el ajuste manual del desfase de frecuencia.

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Introduzca la frecuencia de referencia conocida y precisa en MHz para usar en la calibración. El campo no debe estar vacío antes de hacer clic en Start. |
| **Start** | Comienza la secuencia de calibración de frecuencia. AetherSDR restablece el error de frecuencia a 0 ppb y luego envía `radio pll_start` a la radio. El botón se deshabilita y se etiqueta como **Busy** mientras la calibración se está ejecutando. Una etiqueta de estado junto al botón informa el progreso (Starting… y estados posteriores). |
| **Freq Offset (ppb):** | Muestra o establece manualmente el desfase de frecuencia actual en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador. Las opciones disponibles dependen del hardware instalado. La etiqueta de estado junto al control se actualiza en vivo y muestra la fuente activa, el estado de bloqueo y cualquier resolución en curso (ver más abajo). |

### 10 MHz Reference Source — comportamiento de la etiqueta de estado (cambio en v0.9.7)

En v0.9.7, la etiqueta de estado de bloqueo junto a **10 MHz Reference Source:** fue revisada para mostrar información de estado más rica.

El texto de la etiqueta se determina de la siguiente manera:

- Si la radio aún no ha informado el estado del oscilador, la etiqueta muestra **Waiting for oscillator status**.
- Si **Auto** está seleccionado y la radio se ha resuelto a una fuente específica, la etiqueta muestra **Auto -> \<fuente resuelta\>** seguido de **Locked** o **Unlocked**.
- Si una fuente específica está seleccionada pero la radio está usando activamente una fuente diferente, la etiqueta muestra **\<fuente seleccionada\> -> \<fuente activa\>** seguido de **Locked** o **Unlocked**.
- De lo contrario, la etiqueta muestra el nombre de la fuente activa seguido de **Locked** o **Unlocked**.
