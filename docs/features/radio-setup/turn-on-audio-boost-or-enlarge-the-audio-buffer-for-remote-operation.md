# Activar el refuerzo de audio o ampliar el búfer de audio para operación remota

Use estos ajustes para compensar el bajo volumen de recepción o los cortes de audio al operar AetherSDR a través de una conexión VPN o SmartLink. Audio Boost agrega ganancia adicional en la ruta de audio del cliente; un Audio Buffer más grande absorbe el jitter de red a costa de mayor latencia.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. Estos controles no están disponibles cuando no hay ninguna radio conectada.
- Abra `Settings > Radio Setup...` y seleccione la pestaña **Audio** antes de seguir los pasos a continuación.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Para aumentar el volumen de recepción, haga clic en **Audio Boost:** para activarlo. El botón muestra su estado activo cuando está habilitado.
4. Para reducir los cortes o interrupciones de audio, haga clic en el spinbox **Audio Buffer:** e ingrese un valor entre 50 y 1000 ms. Los valores más altos agregan más almacenamiento en búfer a costa de mayor latencia.
5. Cierre el diálogo. Los ajustes surten efecto de inmediato.

## Qué hace cada control

| Control | Qué hace | Rango válido |
|---|---|---|
| **Audio Boost:** | Habilita ganancia adicional en la ruta de audio del cliente. | On / Off |
| **Audio Buffer:** | Establece el búfer de audio del lado del cliente para absorber el jitter de red. Auméntelo cuando use conexiones VPN o SmartLink con latencia inestable. | 50–1000 ms |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto / Uncompressed / Opus |
| **TX Follows Active Slice** | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación en Split. | On / Off |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | On / Off |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=menor latencia a 3=mayor nitidez) por modo; el control deslizante se deshabilita cuando Auto está habilitado. | 0–3 |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | On / Off |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectarse, para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio, que está rota en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se necesita ningún cierre de clave del lado del cliente. Si el campo de IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. | — |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (en lugar de un Antenna Genius) es el dispositivo conectado actualmente. | — |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antenas ShackSwitch mediante el protocolo UDP/TCP del AG en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. El ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión del AG. El autodescubrimiento por UDP también funciona sin esta fila. La fila se oculta del estado Connected si el dispositivo conectado es un Antenna Genius (que no sea ShackSwitch). | — |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el webPort de la baliza si es > 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | — |
| **Select Installer...** | Abre un selector de archivos que acepta archivos .msi (instalador WiX de FlexRadio v4.2+), .exe (instalador de extracción automática anterior) o un archivo de firmware .ssdr preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el archivo .ssdr sin herramientas externas. Este botón estaba etiquetado como **Browse .ssdr...** antes de la versión v0.9.3. | — |
| **APD (tab)** | Configuración del muestreador externo de Predistorsión Adaptativa (APD) — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña se oculta a menos que la radio informe `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; las radios de la serie 6000 y las anteriores a 4.2.18 mantienen la pestaña invisible. | — |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que usa la radio para muestrear la RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando use un amplificador lineal externo. Las opciones se obtienen en tiempo real del subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio reporta un valor no reconocido. | INTERNAL / RX_A / RX_B / XVTA / XVTB |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. | — |
| **Themes (tab)** | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. | — |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores del slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. | Use Aether defaults / Custom colors |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Se admiten hasta 8 slices. | — |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | — |

## Pestaña Peripherals — interfaz web del ShackSwitch (cambio en v0.9.4)

En la versión v0.9.4, la pestaña Peripherals incorpora un botón **⚙ Web UI** en la fila del ShackSwitch. Al hacer clic en él, se abre la interfaz de configuración web integrada del dispositivo ShackSwitch en el navegador del sistema.

El botón determina la URL de la siguiente manera:

1. Si el ShackSwitch está conectado actualmente y su baliza de descubrimiento anuncia un `webPort` mayor que 1024, se usa ese puerto.
2. De lo contrario, se usa el valor almacenado en `SS_WebPort`.
3. Si ninguno está disponible, se usa el puerto 5000 como alternativa.

La dirección IP se toma de `SS_ManualIp` si está configurada. Si ese campo está vacío y el dispositivo conectado actualmente es un ShackSwitch, se usa en su lugar la dirección del par activo. El botón no hace nada si no se puede resolver ninguna dirección IP.

La fila de Antenna Genius también incorpora un pequeño cambio de comportamiento en la versión v0.9.4: cuando un ShackSwitch es el dispositivo conectado, la fila de Antenna Genius ya no muestra el estado Connected, manteniendo las dos filas visualmente distintas.

### Cómo abrir la interfaz web del ShackSwitch

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Peripherals**.
3. Confirme que la fila del ShackSwitch muestre **Connected**. Si no es así, ingrese la IP del dispositivo y haga clic en **Connect**.
4. Haga clic en **⚙ Web UI**. Su navegador predeterminado abre la página de configuración del ShackSwitch.

> **Nota:** Si su ShackSwitch usa un puerto web no estándar, configúrelo manualmente en `SS_WebPort` antes de hacer clic en **⚙ Web UI**.

## Actualización de firmware — selección de un instalador (cambio en v0.9.3)

En la versión v0.9.3 cambió el flujo de trabajo de preparación de firmware. El botón que anteriormente estaba etiquetado como **Browse .ssdr...** ahora se llama **Select Installer...**. El selector de archivos ahora acepta el paquete completo del instalador de SmartSDR además de un archivo .ssdr preextraído.

Cuando **Check for Update** detecta una versión de firmware más reciente, AetherSDR ya no la descarga automáticamente. En su lugar, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com usted mismo y, a continuación, use **Select Installer...** para prepararlo.

### Cómo preparar y cargar el firmware

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Check for Update**. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador desde flexradio.com.
4. Descargue el instalador de SmartSDR desde flexradio.com a su computadora (.msi para v4.2+, .exe para versiones anteriores).
5. Haga clic en **Select Installer...**. En el selector de archivos, seleccione el archivo .msi, .exe o .ssdr descargado y haga clic en **Open**. La etiqueta de estado muestra **Preparing firmware from \<filename\>...** y aparece una barra de progreso mientras el preparador extrae el firmware.
6. Cuando la preparación finalice, haga clic en **Upload Firmware** para transferir el firmware a la radio. Una barra de progreso y una etiqueta de estado hacen seguimiento de la carga.

> **Nota:** Si ya tiene un archivo .ssdr preextraído, puede seleccionarlo directamente en el paso 5. El preparador detecta el formato automáticamente.

## Pestaña RX — calibración de frecuencia

En la versión v0.9.2.1 se revisó la sección de calibración de la pestaña RX. El campo **Cal Frequency (MHz):** y el botón **Start** ahora son siempre visibles, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado lo confirma en verde; cuando no hay ningún GPSDO instalado, la etiqueta aparece en ámbar. En ambos casos se permite la calibración manual del desplazamiento de frecuencia.

### Controles de calibración

| Control | Qué hace |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia conocida y precisa en MHz que se usará para la calibración. El campo no debe estar vacío antes de hacer clic en Start. |
| **Start** | Inicia la secuencia de calibración de frecuencia. AetherSDR restablece el error de frecuencia a 0 ppb y luego envía `radio pll_start` a la radio. El botón se deshabilita y se etiqueta como **Busy** mientras la calibración está en curso. Una etiqueta de estado junto al botón reporta el progreso (Starting… y estados subsiguientes). |
| **Freq Offset (ppb):** | Muestra o establece manualmente el desplazamiento de frecuencia actual en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en tiempo real junto al control. |

### Cómo ejecutar una calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**. El botón cambia a **Busy** y la etiqueta de estado muestra **Starting…**.
5. Espere a que la etiqueta de estado indique la finalización. El botón se reactiva automáticamente.
6. Si es necesario, revise el valor resultante en **Freq Offset (ppb):**.

> **Nota:** Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la secuencia no se ejecuta.

## Consejos

- Comience con un aumento moderado del búfer (200–300 ms) antes de subir más. Los valores muy grandes hacen que el audio sea notablemente lento durante los QSOs.
