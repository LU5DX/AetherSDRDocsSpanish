# Asignar un cable USB como CAT, BCD, bit o PTT

Use esta página para configurar los adaptadores USB seriales conectados a su FLEX-8600 y asignar a cada uno un rol — control CAT, datos de banda BCD, salida de bit individual o PTT — junto con sus parámetros seriales y opciones de comportamiento.

## Antes de comenzar

- Conecte el o los adaptadores USB seriales a la computadora que ejecuta AetherSDR antes de abrir el diálogo.
- AetherSDR debe estar conectado a la radio. La pestaña USB Cables no está disponible sin una conexión de radio activa.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña USB Cables. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice la lista de cables en el lado izquierdo de la pestaña. Cada cable USB detectado aparece con su nombre y un indicador de estado **Plugged** (Conectado) o **Unplugged** (Desconectado).
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Establezca el tipo de cable usando el campo **Name:** y el selector de tipo asociado. Elija entre CAT, BCD, bit o PTT según el rol que este cable deba cumplir.
5. Establezca **Enabled** para habilitar el cable. El cable no funcionará hasta que esté habilitado.
6. Configure los parámetros seriales para el cable:
   - **Speed** — velocidad en baudios para la conexión serial.
   - **Data Bits** — número de bits de datos.
   - **Parity** — configuración de paridad.
   - **Stop Bits** — número de bits de parada.
   - **Flow** — método de control de flujo.
7. Configure las opciones de comportamiento relevantes para el tipo de cable:
   - **Source** — selecciona qué impulsa la salida del cable.
   - **Auto Report** — controla si los cambios de estado se reportan automáticamente.
   - **BCD Type** — selecciona el formato de codificación BCD (solo cables BCD).
   - **Polarity** — establece lógica activo-alto o activo-bajo.
   - **Bit Configuration (0–7)** — asigna funciones a bits de salida individuales (solo cables de bit).
8. Repita los pasos 3–7 para cualquier cable adicional.
9. Haga clic en **Close** para descartar el diálogo. Los ajustes tienen efecto inmediatamente cuando cada cable está habilitado; no se requiere un paso Apply separado.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| **Cables list / Status** | Lista todos los adaptadores USB seriales detectados con estado **Plugged** (Conectado) o **Unplugged** (Desconectado). Seleccione un cable aquí para editar su configuración. | |
| **Name:** | Etiqueta visible para el usuario del cable. | |
| **Enabled** | Activa el cable. El cable está inactivo hasta que se habilite. | |
| **Speed** | Velocidad en baudios serial. | |
| **Data Bits** | Número de bits de datos seriales. | |
| **Parity** | Paridad serial: None, Even, Odd, etc. | |
| **Stop Bits** | Número de bits de parada. | |
| **Flow** | Método de control de flujo (None, Hardware, Software). | |
| **Source** | Selecciona la fuente de señal de radio que impulsa la salida del cable. | |
| **Auto Report** | Cuando está activo, la radio reporta cambios de estado al cable automáticamente. | |
| **BCD Type** | Selecciona el formato de codificación de datos de banda BCD. Se aplica solo a cables de tipo BCD. | |
| **Polarity** | Establece si la lógica de salida es activo-alto o activo-bajo. | |
| **Bit Configuration (0–7)** | Asigna pines de salida individuales a funciones específicas. Se aplica solo a cables de tipo bit. | |
| **TX Follows Active Slice** | TX sigue la slice activa. Mutuamente excluyente con **Active Slice Follows TX**. | Se deshabilita automáticamente durante operación Split. |
| **Active Slice Follows TX** | Cambia la slice activa cuando TX se mueve externamente (p. ej. WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=latencia más baja a 3=más nítido) por modo; el regulador se deshabilita cuando Auto está habilitado. | Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática de nivel de filtro para ese modo; deshabilita el regulador de nitidez manual. | Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Abre/cierra conexión TCP directa al TGXL en puerto 9010. Guarda IP y puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente en el inicio. | Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` rota en firmware 4.2 del lado de la radio. El TGXL impulsa PTT de radio a través de su cable de bloqueo de hardware; no se requiere codificación del lado del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena previamente. |
| **Connect / Disconnect (PGXL)** | Abre/cierra conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda IP y puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra conexión a Antenna Genius (puerto predeterminado 9007). Guarda IP y puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra estado **Connected** solo cuando el dispositivo conectado es una Antenna Genius estándar, no un ShackSwitch. | |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en puerto 9007. Guarda IP en `SS_ManualIp` y puerto en `SS_ControlPort`. | ShackSwitch se detecta por el campo 'ShackSwitch' en el beacon de difusión AG. La detección automática vía UDP también funciona sin esta fila. Fila oculta del estado **Connected** si Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa `webPort` del beacon si es mayor a 1024; de lo contrario, regresa a `SS_WebPort` o puerto 5000. | |
| **Select Installer...** | Abre un selector de archivos que acepta instalador `.msi` (FlexRadio v4.2+ WiX), instalador `.exe` (antiguo de auto-extracción) o archivo de firmware `.ssdr` pre-extraído. El preparador de firmware detecta automáticamente el formato de los primeros 8 bytes (magia OLE/MSI vs PE/COFF MZ) y extrae `.ssdr` sin herramientas externas. | Etiqueta cambiada de **Browse .ssdr...** en v0.9.3. Cuando una actualización está disponible, descargue el instalador SmartSDR de flexradio.com, luego haga clic en **Select Installer...** para prepararlo. |
| **APD (tab)** | Configuración de muestreador de Pre-Distorsión Adaptativa externa — selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y botón de reseteo de ecualizador. | La pestaña está oculta a menos que la radio reporte `apd configurable=1`. Solo serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; radios 6000-series y pre-4.2.18 mantienen la pestaña invisible. |
| **ANT1 / ANT2 / XVTA / XVTB sampler combos (APD)** | Selecciona la ruta de retroalimentación que la radio usa para muestrear el RF saliente para entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando impulse un amplificador lineal externo. | Las opciones se rellenan en tiempo real desde el sub-objeto `apd sampler` de la radio. Regresa a INTERNAL si la radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | |
| **Themes (tab)** | Pestaña de personalización de UI — actualmente aloja la sección Slice Colors. | |
| **Use Aether defaults / Custom colors** | Cambia el esquema de color de slice entre la paleta incorporada de AetherSDR y un conjunto completamente personalizado por slice. | Respaldado por `SliceColorManager::useCustomColors()`. |
| **Slice A–H color buttons** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles inmediatamente en widgets VFO, superposiciones panadapter y badges de canal CAT. | Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Restablece todos los colores de slice personalizados a la paleta incorporada de AetherSDR. | |

## Pestaña RX — calibración de frecuencia (v0.9.2.1)

La pestaña **RX** ahora muestra los controles de calibración de frecuencia independientemente de si un GPSDO está instalado. En versiones anteriores, los campos de calibración estaban ocultos cuando se detectaba un GPSDO.

- Si un GPSDO está instalado, una línea de estado verde lee "GPSDO installed. Manual frequency offset calibration available."
- Si no hay GPSDO instalado, una línea de estado amarilla lee "Manual frequency offset calibration available."

En ambos casos, los controles **Cal Frequency (MHz):**,  **Start** y **Freq Offset (ppb):** siempre son visibles.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración. Una etiqueta de estado a la derecha del botón muestra texto de progreso.
   - "Starting…" aparece inmediatamente.
   - La radio recibe `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0`, luego `radio pll_start` para comenzar el barrido.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no comienza.
4. Espere a que la etiqueta de estado indique finalización. El botón **Start** se habilita automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

### Controles de la pestaña RX

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia usada para calibración, ingresada en MHz hasta seis decimales. | Se envía a la radio como `radio set cal_freq=<value>`. |
| **Start** | Comienza el barrido de calibración. Se deshabilita y se etiqueta **Busy** mientras una calibración está en progreso. | Restablece `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia cal no vacía. |
| **Freq Offset (ppb):** | Corrección manual de desviación de frecuencia en partes por billón. | |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones disponibles dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al selector y se actualiza en tiempo real. |

## Actualización de firmware (v0.9.3)

En v0.9.3, el flujo de trabajo de actualización de firmware cambió. AetherSDR ya no descarga el instalador automáticamente. Cuando **Check for Update** reporta que hay una versión más nueva disponible, descargue usted mismo el instalador SmartSDR de flexradio.com, luego use **Select Installer...** para prepararlo localmente.

### Formatos de instalador soportados

| Formato | Extensión | Notas |
|---|---|---|
| Instalador WiX MSI | `.msi` | FlexRadio v4.2 y posterior. |
| Instalador EXE auto-extraíble | `.exe` | Versiones anteriores de SmartSDR. |
| Archivo de firmware pre-extraído | `.ssdr` | Archivo de firmware directo, si ya tiene uno. |

El preparador de firmware detecta automáticamente el formato de los primeros 8
