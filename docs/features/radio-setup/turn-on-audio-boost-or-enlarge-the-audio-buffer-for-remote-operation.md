# Activar audio boost o aumentar el búfer de audio para operación remota

Utilice estos parámetros para compensar el volumen de recepción bajo o cortes de audio al operar AetherSDR a través de una conexión VPN o SmartLink. Audio Boost añade ganancia adicional en la ruta de audio del cliente; un búfer de audio más grande absorbe la fluctuación de latencia de la red al costo de una latencia aumentada.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Estos controles no están disponibles cuando no hay radio conectada.
- Abra `Settings > Radio Setup...` y seleccione la pestaña **Audio** antes de seguir los pasos que se describen a continuación.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el volumen de recepción, haga clic en **Audio Boost:** para activarlo. El botón muestra su estado activo cuando está habilitado.
4. Para reducir cortes o interrupciones de audio, haga clic en el cuadro de rotación **Audio Buffer:** e ingrese un valor entre 50 y 1000 ms. Los valores más altos añaden más buffering al costo de latencia.
5. Cierre el diálogo. Los parámetros surten efecto inmediatamente.

## Qué hace cada control

| Control | Qué hace | Rango válido |
|---|---|---|
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | On / Off |
| **Audio Buffer:** | Establece el búfer de audio del lado del cliente para absorber la fluctuación de latencia de la red. Aumente este valor cuando utilice conexiones VPN o SmartLink con latencia inestable. | 50–1000 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado sobre conexiones SmartLink o LAN. | Auto / Uncompressed / Opus |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante operación Split. | On / Off |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | On / Off |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador se deshabilita cuando Auto está habilitado. | 0–3 |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador de nitidez manual. | On / Off |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Se requiere para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que se dañó en firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de bloqueo de hardware; no se necesita control de lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellenará previamente. | — |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda la IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión a Antenna Genius (puerto predeterminado 9007). Guarda la IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (en lugar de un Antenna Genius) es el dispositivo actualmente conectado. | — |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo UDP/TCP AG en el puerto 9007. Guarda la IP en `SS_ManualIp` y puerto en `SS_ControlPort`. ShackSwitch se detecta por el campo 'ShackSwitch' en el faro de descubrimiento AG. El descubrimiento automático vía UDP también funciona sin esta fila. Fila oculta del estado Conectado si Antenna Genius (non-ShackSwitch) es el dispositivo conectado. | — |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el webPort del faro si es > 1024; si no, recae en `SS_WebPort` o puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta instaladores .msi (FlexRadio v4.2+ WiX), .exe (instaladores autoextraíbles más antiguos) o un archivo de firmware .ssdr preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magic OLE/MSI versus MZ PE/COFF) y extrae el .ssdr sin herramientas externas. Este botón se etiquetaba **Browse .ssdr...** antes de v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador externo de Pre-Distorsión Adaptativa — selección por antena de TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento de APD para esa antena de TX. Elija una entrada RX/XVTR externa cuando maneje un amplificador lineal externo. Las opciones se rellenan en tiempo real desde el subobjeto `apd sampler` de la radio. Recae a INTERNAL si la radio informa un valor no reconocido. | INTERNAL / RX_A / RX_B / XVTA / XVTB |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults / Custom colors |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter e insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Se soportan hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | — |

## Pestaña Peripherals — interfaz web ShackSwitch (cambio en v0.9.4)

En v0.9.4 la pestaña Peripherals gana un botón **⚙ Web UI** en la fila ShackSwitch. Al hacer clic en él se abre la interfaz de configuración web incorporada del dispositivo ShackSwitch en su navegador del sistema.

El botón determina la URL de la siguiente manera:

1. Si el ShackSwitch está actualmente conectado y su faro de descubrimiento anuncia un `webPort` mayor que 1024, se usa ese puerto.
2. Si no, se utiliza el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000 como respaldo.

La dirección IP se toma de `SS_ManualIp` si está establecida. Si ese campo está vacío y el dispositivo actualmente conectado es un ShackSwitch, se usa la dirección de par en vivo. El botón no hace nada si no se puede resolver ninguna dirección IP.

La fila Antenna Genius también gana un pequeño cambio de comportamiento en v0.9.4: cuando un ShackSwitch es el dispositivo conectado, la fila Antenna Genius ya no muestra un estado Conectado, manteniendo las dos filas visualmente distintas.

### Cómo abrir la interfaz web de ShackSwitch

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Confirme que la fila ShackSwitch muestra **Connected**. Si no, ingrese la IP del dispositivo y haga clic en **Connect**.
4. Haga clic en **⚙ Web UI**. Su navegador predeterminado abre la página de configuración de ShackSwitch.

> **Nota:** Si su ShackSwitch utiliza un puerto web no estándar, establézcalo manualmente en `SS_WebPort` antes de hacer clic en **⚙ Web UI**.

## Actualización de firmware — seleccionar un instalador (cambio en v0.9.3)

En v0.9.3 el flujo de trabajo de gestión de firmware cambió. El botón previamente etiquetado **Browse .ssdr...** ahora se etiqueta **Select Installer...**. El selector de archivos ahora acepta el paquete instalador SmartSDR completo además de un archivo .ssdr preextraído.

Cuando **Check for Update** detecta una versión de firmware más nueva, AetherSDR ya no lo descarga automáticamente. En su lugar, la etiqueta de estado le instruye a descargar el instalador SmartSDR de flexradio.com usted mismo, y luego usar **Select Installer...** para gestionar la carga.

### Cómo gestionar y cargar firmware

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e instrucciones para descargar el instalador de flexradio.com.
4. Descargue el instalador SmartSDR de flexradio.com a su computadora (.msi para v4.2+, .exe para versiones anteriores).
5. Haga clic en **Select Installer...**. En el selector de archivos, seleccione el archivo .msi, .exe o .ssdr descargado y haga clic en **Open**. La etiqueta de estado muestra **Preparing firmware from \<filename\>...** y aparece una barra de progreso mientras el gestor extrae el firmware.
6. Cuando se completa la gestión, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y etiqueta de estado rastrean la carga.

> **Nota:** Si ya tiene un archivo .ssdr preextraído, puede seleccionarlo directamente en el paso 5. El gestor detecta el formato automáticamente.

## Pestaña RX — calibración de frecuencia

En v0.9.2.1 la sección de calibración de la pestaña RX fue revisada. El campo **Cal Frequency (MHz):** y el botón **Start** ahora siempre son visibles independientemente de si hay un GPSDO instalado. Cuando un GPSDO está presente, la etiqueta de estado lo confirma en verde; cuando no hay GPSDO instalado, la etiqueta aparece en ámbar. Ambos casos permiten calibración manual del desplazamiento de frecuencia.

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz a usar para la calibración. El campo no debe estar vacío antes de hacer clic en Start. |
| **Start** | Comienza la secuencia de calibración de frecuencia. AetherSDR reinicia el error de frecuencia a 0 ppb, luego envía `radio pll_start` a la radio. El botón se deshabilita y se etiqueta **Busy** mientras se ejecuta la calibración. Una etiqueta de estado junto al botón informa el progreso (Starting…, y estados posteriores). |
| **Freq Offset (ppb):** | Muestra o establece manualmente el desplazamiento de frecuencia actual en partes por billón. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO, o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en tiempo real junto al control. |

### Cómo ejecutar una calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**. El botón cambia a **Busy** y la etiqueta de estado muestra **Starting…**.
5. Espere a que la etiqueta de estado indique finalización. El botón se habilita automáticamente.
6. Si es necesario, revise el valor resultante en **Freq Offset (ppb):**.

> **Nota:** Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la secuencia no se ejecuta.

## Consejos

- Comience con un aumento modesto del búfer (200–300 ms) antes de aumentar más. Los valores muy grandes hacen que el audio sea notoriamente lento durante QSOs.
