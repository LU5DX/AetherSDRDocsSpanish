# Asignar un cable USB como CAT, BCD, bit o PTT

Utilice esta página para configurar los adaptadores serie USB conectados a su FLEX-8600 y asignar a cada uno un rol — control CAT, datos de banda BCD, salida de bit individual o PTT — junto con sus parámetros serie y opciones de comportamiento.

## Antes de empezar

- Conecte el/los adaptador(es serie USB al ordenador que ejecuta AetherSDR antes de abrir el diálogo.
- AetherSDR debe estar conectado a la radio. La pestaña USB Cables no está disponible sin una conexión activa a la radio.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña USB Cables. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice la lista de cables en el lado izquierdo de la pestaña. Cada cable USB detectado aparece con su nombre y un indicador de estado **Plugged** o **Unplugged**.
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Configure el tipo de cable usando el campo **Name:** y el selector de tipo asociado. Elija entre CAT, BCD, bit o PTT según el rol que deba cumplir este cable.
5. Active **Enabled** para habilitar el cable. El cable no funcionará hasta que esté habilitado.
6. Configure los parámetros serie del cable:
   - **Speed** — velocidad en baudios para la conexión serie.
   - **Data Bits** — número de bits de datos.
   - **Parity** — configuración de paridad.
   - **Stop Bits** — número de bits de parada.
   - **Flow** — método de control de flujo.
7. Configure las opciones de comportamiento relevantes para el tipo de cable:
   - **Source** — selecciona qué impulsa la salida del cable.
   - **Auto Report** — controla si los cambios de estado se informan automáticamente.
   - **BCD Type** — selecciona el formato de codificación BCD (solo cables BCD).
   - **Polarity** — establece la lógica activa en alto o activa en bajo.
   - **Bit Configuration (0–7)** — asigna funciones a bits de salida individuales (solo cables de tipo bit).
8. Repita los pasos 3–7 para cualquier cable adicional.
9. Haga clic en **Close** para cerrar el diálogo. Los ajustes surten efecto inmediatamente cuando cada cable está habilitado; no se requiere un paso de aplicación separado.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| **Cables list / Status** | Enumera todos los adaptadores serie USB detectados con estado **Plugged** o **Unplugged**. Seleccione un cable aquí para editar su configuración. | |
| **Name:** | Etiqueta visible para el usuario del cable. | |
| **Enabled** | Activa el cable. El cable está inactivo hasta que se habilita. | |
| **Speed** | Velocidad en baudios serie. | |
| **Data Bits** | Número de bits de datos serie. | |
| **Parity** | Paridad serie: None, Even, Odd, etc. | |
| **Stop Bits** | Número de bits de parada. | |
| **Flow** | Método de control de flujo (None, Hardware, Software). | |
| **Source** | Selecciona la fuente de señal de radio que impulsa la salida del cable. | |
| **Auto Report** | Cuando está activo, la radio informa los cambios de estado al cable automáticamente. | |
| **BCD Type** | Selecciona el formato de codificación de datos de banda BCD. Se aplica solo a cables de tipo BCD. | |
| **Polarity** | Establece si la lógica de salida es activa en alto o activa en bajo. | |
| **Bit Configuration (0–7)** | Asigna pines de salida individuales a funciones específicas. Se aplica solo a cables de tipo bit. | |
| **TX Follows Active Slice** | TX sigue a la slice activa. Es mutuamente excluyente con **Active Slice Follows TX**. | Se desactiva automáticamente durante la operación en Split. |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con **TX Follows Active Slice**. | |
| **Deslizadores de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. | Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. | Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. | Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio que está rota en firmware 4.2. El TGXL impulsa el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita activación desde el lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado **Connected** solo cuando el dispositivo conectado es un Antenna Genius estándar, no un ShackSwitch. | |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. | ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión AG. El descubrimiento automático a través de UDP también funciona sin esta fila. Fila oculta del estado **Connected** si Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | |
| **Select Installer...** | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (mágico OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. | Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. Cuando hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com, luego haga clic en **Select Installer...** para prepararlo. |
| **APD (pestaña)** | Configuración del muestreador externo de Predistorsión Adaptativa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. | La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y radios con firmware anterior a 4.2.18 mantienen la pestaña invisible. |
| **Combinaciones de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. | Las opciones se obtienen en vivo del subobjeto `apd sampler` de la radio. Vuelve a INTERNAL si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz de usuario — actualmente alberga la sección Slice Colors. | |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores de las slices entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. | Respaldado por `SliceColorManager::useCustomColors()`. |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en los widgets VFO, superposiciones del panadapter e insignias de canal CAT. | Los botones están deshabilitados cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de las slices a la paleta incorporada de AetherSDR. | |

## Pestaña RX — calibración de frecuencia (v0.9.2.1)

La pestaña **RX** ahora muestra los controles de calibración de frecuencia independientemente de si hay un GPSDO instalado. En versiones anteriores, los campos de calibración estaban ocultos cuando se detectaba un GPSDO.

- Si hay un GPSDO instalado, una línea de estado verde dice "GPSDO installed. Manual frequency offset calibration available."
- Si no hay un GPSDO instalado, una línea de estado amarilla dice "Manual frequency offset calibration available."

En ambos casos, los controles **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** están siempre visibles.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Introduzca una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración. Una etiqueta de estado a la derecha del botón muestra el texto de progreso.
   - "Starting…" aparece inmediatamente.
   - La radio recibe `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0`, y luego `radio pll_start` para iniciar el barrido.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no comienza.
4. Espere a que la etiqueta de estado indique la finalización. El botón **Start** se vuelve a habilitar automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

### Controles de la pestaña RX

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración, introducida en MHz con seis decimales. | Se envía a la radio como `radio set cal_freq=<value>`. |
| **Start** | Inicia el barrido de calibración. Deshabilitado y etiquetado como **Busy** mientras una calibración está en curso. | Restablece `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (ppb):** | Corrección manual de desplazamiento de frecuencia en partes por mil millones. | |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External 10 MHz. Las opciones disponibles dependen del hardware instalado y del estado actual del oscilador informado por la radio. | La etiqueta de estado junto al selector se actualiza en vivo. Cuando se selecciona Auto y la radio ha resuelto a una fuente específica, la etiqueta muestra "Auto -> \<source\>" para indicar el hardware activo. Si se selecciona una fuente External 10 MHz pero no se detecta ninguna señal externa, la etiqueta añade "(not detected)". El estado de bloqueo (Locked / Unlocked) se muestra en verde o rojo respectivamente. La etiqueta muestra "Waiting for oscillator status" hasta que la radio informe su primer estado del oscilador. |

## Actualización de firmware (v0.9.3)

En v0.9.3, el flujo de trabajo de actualización de firmware cambió. AetherSDR ya no descarga el instalador automáticamente. Cuando **Check for Update** informa que hay una versión más reciente disponible, descargue el instalador de SmartSDR desde flexradio.com usted mismo, luego use **Select Installer...** para prepararlo localmente.

### Formatos de instalador compatibles

| Formato
