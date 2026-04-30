# Activar refuerzo de audio o aumentar el búfer de audio para operación remota

Use estas configuraciones para compensar bajo volumen de recepción o interrupciones de audio cuando opera AetherSDR a través de una conexión VPN o SmartLink. Audio Boost añade ganancia extra en la ruta de audio del cliente; un búfer de audio más grande absorbe la fluctuación de la red a costa de mayor latencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Estos controles no están disponibles cuando no hay radio conectada.
- Abra `Settings > Radio Setup...` y seleccione la pestaña **Audio** antes de seguir los pasos que se indican a continuación.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el volumen de recepción, haga clic en **Audio Boost:** para activarlo. El botón muestra su estado activo cuando está habilitado.
4. Para reducir interrupciones o pérdidas de audio, haga clic en la casilla giratoria **Audio Buffer:** e ingrese un valor entre 50 y 1000 ms. Los valores más altos añaden más búfer a costa de latencia.
5. Cierre el diálogo. Los cambios surten efecto inmediatamente.

## Qué hace cada control

| Control | Qué hace | Rango válido |
|---|---|---|
| **Audio Boost:** | Habilita ganancia extra en la ruta de audio del cliente. | Activado / Desactivado |
| **Audio Buffer:** | Establece el búfer de audio del lado del cliente para absorber la fluctuación de la red. Aumente este valor al usar conexiones VPN o SmartLink con latencia inestable. | 50–1000 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio usado sobre SmartLink o LAN. | Auto / Uncompressed / Opus |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante operación Split. | Activado / Desactivado |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | Activado / Desactivado |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está habilitado. | 0–3 |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática de nivel de filtro para ese modo; desactiva el deslizador de nitidez manual. | Activado / Desactivado |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` en conexión para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio rota en firmware 4.2. El TGXL controla PTT de radio mediante su cable de bloqueo de hardware; no se necesita codificación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa previamente. | — |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa a Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. | — |
| **Select Installer...** | Abre un selector de archivos que acepta .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador autoextraíble más antiguo), o archivo de firmware .ssdr preextraído. El organizador de firmware detecta automáticamente el formato desde los primeros 8 bytes (magic OLE/MSI vs PE/COFF MZ) y extrae el .ssdr sin herramientas externas. Este botón se denominaba **Browse .ssdr...** antes de v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador externo de Predistorsión Adaptativa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que usa la radio para muestrear el RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa al accionar un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL / RX_A / RX_B / XVTA / XVTB |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente alberga la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults / Custom colors |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para ese slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones de panadapter y insignias de canal CAT. Los botones están deshabilitados cuando se selecciona **Use Aether defaults**. Se admiten hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | — |

## Actualización de firmware — seleccionar un instalador (cambio de v0.9.3)

En v0.9.3 el flujo de trabajo de organización de firmware cambió. El botón previamente etiquetado **Browse .ssdr...** ahora está etiquetado **Select Installer...**. El selector de archivos ahora acepta el paquete de instalador SmartSDR completo además de un archivo .ssdr preextraído.

Cuando **Check for Update** detecta una versión de firmware más nueva, AetherSDR ya no la descarga automáticamente. En su lugar, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com usted mismo, luego use **Select Installer...** para organizarlo.

### Cómo organizar y cargar firmware

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador SmartSDR desde flexradio.com a su computadora (.msi para v4.2+, .exe para versiones más antiguas).
5. Haga clic en **Select Installer...**. En el selector de archivos, seleccione el archivo .msi, .exe, o .ssdr descargado y haga clic en **Open**. La etiqueta de estado muestra **Preparing firmware from \<filename\>...** y una barra de progreso aparece mientras el organizador extrae el firmware.
6. Cuando la organización se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y etiqueta de estado rastrean la carga.

> **Nota:** Si ya tiene un archivo .ssdr preextraído, puede seleccionarlo directamente en el paso 5. El organizador detecta el formato automáticamente.

## Pestaña RX — calibración de frecuencia

En v0.9.2.1 la sección de calibración de la pestaña RX fue revisada. El campo **Cal Frequency (MHz):** y el botón **Start** ahora siempre son visibles independientemente de si se instala un GPSDO. Cuando está presente un GPSDO, la etiqueta de estado lo confirma en verde; cuando no se instala GPSDO, la etiqueta aparece en ámbar. Ambos casos permiten calibración manual de offset de frecuencia.

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz a usar para calibración. El campo no debe estar vacío antes de hacer clic en Start. |
| **Start** | Comienza la secuencia de calibración de frecuencia. AetherSDR reinicia el error de frecuencia a 0 ppb, luego envía `radio pll_start` a la radio. El botón está deshabilitado y etiquetado **Busy** mientras se ejecuta la calibración. Una etiqueta de estado junto al botón informa el progreso (Starting…, y estados posteriores). |
| **Freq Offset (ppb):** | Muestra u establece manualmente el offset de frecuencia actual en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO, o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en vivo junto al control. |

### Cómo ejecutar una calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**. El botón cambia a **Busy** y la etiqueta de estado muestra **Starting…**.
5. Espere a que la etiqueta de estado indique finalización. El botón se reactiva automáticamente.
6. Si es necesario, revise el valor resultante en **Freq Offset (ppb):**.

> **Nota:** Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la secuencia no se ejecuta.

## Consejos

- Comience con un aumento modesto del búfer (200–300 ms) antes de aumentar más. Valores muy grandes hacen que el audio sea notoriamente lento durante QSOs.
- Si la calidad de audio es pobre sobre SmartLink, también revise la configuración de códec (**Audio Compression (SmartLink):**). Cambiar de Auto a Opus puede reducir el ancho de banda y mejorar la estabilidad en conexiones lentas.

## Solución de problemas

- **Los controles Audio Boost y Audio Buffer están deshabilitados u ocultos** — Estos controles están en la pestaña **Audio**. Confirme que ha seleccionado esa pestaña, no otra pestaña como **RX** o **Phone/CW**.
- **Aumentar Audio Buffer no tiene efecto en las pérdidas** — El búfer absorbe la fluctuación pero no puede compensar pérdida de paquetes sostenida. Verifique su ruta de red; también vea [Change network MTU for VPN/remote setups](change-network-mtu-for-vpn-remote-setups.md).
- **El botón Start permanece deshabilitado después de la calibración** — Si la radio no responde a `radio pll_start`, verifique que la radio esté conectada y no esté transmitiendo, luego intente de nuevo.
- **Select Installer... muestra una barra de progreso pero nunca habilita Upload Firmware** — El organizador fue incapaz de extraer un .ssdr válido del archivo seleccionado. Confirme que descargó el instalador SmartSDR correcto para su familia de radio e intente de nuevo.

## Relacionado

- [Pick Opus vs uncompressed audio for SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Choose PC input/output audio devices](choose-pc-input-output-audio-devices.md)
- [Change network MTU for VPN/remote setups](change-network-mtu-for-vpn-remote-setups.md)
