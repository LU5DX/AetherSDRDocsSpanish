# Asignar un cable USB como CAT, BCD, bit o PTT

Use esta página para configurar los adaptadores serie USB conectados a su FLEX-8600 y asignar a cada uno una función: control CAT, datos de banda BCD, salida de bit individual o PTT, junto con sus parámetros serie y opciones de comportamiento.

## Antes de comenzar

- Conecte los adaptadores serie USB a la computadora que ejecuta AetherSDR antes de abrir el diálogo.
- AetherSDR debe estar conectado al radio. La pestaña USB Cables no está disponible sin una conexión activa al radio.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña USB Cables. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice la lista de cables en el lado izquierdo de la pestaña. Cada cable USB detectado aparece con su nombre y un indicador de estado **Plugged** o **Unplugged**.
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Establezca el tipo de cable usando el campo **Name:** y el selector de tipo asociado. Elija entre CAT, BCD, bit o PTT según la función que deba cumplir el cable.
5. Active **Enabled** para habilitar el cable. El cable no funcionará hasta que esté habilitado.
6. Configure los parámetros serie del cable:
   - **Speed** — velocidad en baudios para la conexión serie.
   - **Data Bits** — número de bits de datos.
   - **Parity** — configuración de paridad.
   - **Stop Bits** — número de bits de parada.
   - **Flow** — método de control de flujo.
7. Configure las opciones de comportamiento relevantes para el tipo de cable:
   - **Source** — selecciona qué controla la salida del cable.
   - **Auto Report** — controla si los cambios de estado se reportan automáticamente.
   - **BCD Type** — selecciona el formato de codificación BCD (solo cables BCD).
   - **Polarity** — establece lógica activa-alta o activa-baja.
   - **Bit Configuration (0–7)** — asigna funciones a los bits de salida individuales (solo cables de tipo bit).
8. Repita los pasos 3–7 para cualquier cable adicional.
9. Haga clic en **Close** para cerrar el diálogo. Los ajustes surten efecto de inmediato cuando se habilita cada cable; no se requiere un paso separado de aplicación.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| **Lista de cables / Estado** | Enumera todos los adaptadores serie USB detectados con estado **Plugged** o **Unplugged**. Seleccione un cable aquí para editar su configuración. | |
| **Name:** | Etiqueta visible por el usuario para el cable. | |
| **Enabled** | Activa el cable. El cable está inactivo hasta que se habilite. | |
| **Speed** | Velocidad en baudios serie. | |
| **Data Bits** | Número de bits de datos serie. | |
| **Parity** | Paridad serie: None, Even, Odd, etc. | |
| **Stop Bits** | Número de bits de parada. | |
| **Flow** | Método de control de flujo (None, Hardware, Software). | |
| **Source** | Selecciona la fuente de señal del radio que controla la salida del cable. | |
| **Auto Report** | Cuando está activo, el radio reporta los cambios de estado al cable automáticamente. | |
| **BCD Type** | Selecciona el formato de codificación de datos de banda BCD. Solo aplica a cables de tipo BCD. | |
| **Polarity** | Establece si la lógica de salida es activa-alta o activa-baja. | |
| **Bit Configuration (0–7)** | Asigna pines de salida individuales a funciones específicas. Solo aplica a cables de tipo bit. | |
| **TX Follows Active Slice** | TX sigue al slice (canal de recepción) activo. Mutuamente exclusivo con **Active Slice Follows TX**. | Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. | |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0 = menor latencia a 3 = máxima nitidez) por modo; el control deslizante se deshabilita cuando Auto está activado. | Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecta automáticamente al iniciarse. | Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila muestra el estado **Connected** solo cuando el dispositivo conectado es un Antenna Genius estándar, no un ShackSwitch. | |
| **Connect / Disconnect (ShackSwitch)** | Abre/cierra la conexión a un conmutador de antena ShackSwitch mediante el protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. | El ShackSwitch se detecta por el campo 'ShackSwitch' en la baliza de difusión AG. El autodescubrimiento vía UDP también funciona sin esta fila. La fila se oculta del estado **Connected** si el dispositivo conectado es un Antenna Genius (no ShackSwitch). |
| **⚙ Web UI (ShackSwitch)** | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Usa el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. | |
| **Select Installer...** | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador de extracción automática más antiguo) o un archivo de firmware `.ssdr` ya extraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (OLE/MSI magic vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. | Etiqueta cambiada de **Browse .ssdr...** en la v0.9.3. Cuando hay una actualización disponible, descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en **Select Installer...** para prepararlo. |
| **APD (pestaña)** | Configuración del muestreador externo de predistorsión adaptativa (APD): selección por antena TX del puerto de muestra de retroalimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. | La pestaña está oculta a menos que el radio reporte `apd configurable=1`. Solo la serie FLEX-8x00 con firmware SmartSDR 4.2.18+ expone esto; los radios de la serie 6000 y los anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Selectores de muestreador ANT1 / ANT2 / XVTA / XVTB (APD)** | Selecciona la ruta de retroalimentación que usa el radio para muestrear la RF saliente para el entrenamiento APD de esa antena TX. Elija una entrada RX/XVTR externa cuando use un amplificador lineal externo. | Las opciones se obtienen en tiempo real del subobjeto `apd sampler` del radio. Vuelve a INTERNAL si el radio reporta un valor no reconocido. |
| **Equalizer Reset (APD)** | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. | |
| **Themes (pestaña)** | Pestaña de personalización de la interfaz — actualmente aloja la sección Slice Colors. | |
| **Use Aether defaults / Custom colors** | Cambia el esquema de colores del slice entre la paleta integrada de AetherSDR y un conjunto totalmente personalizado por slice. | Respaldado por `SliceColorManager::useCustomColors()`. |
| **Botones de color Slice A–H** | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado a ese slice. Los cambios son visibles de inmediato en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT. | Los botones se deshabilitan cuando se selecciona **Use Aether defaults**. Hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Restablece todos los colores personalizados de slice a la paleta integrada de AetherSDR. | |

## Pestaña RX — calibración de frecuencia (v0.9.2.1)

La pestaña **RX** ahora muestra los controles de calibración de frecuencia independientemente de si hay un GPSDO instalado. En versiones anteriores, los campos de calibración estaban ocultos cuando se detectaba un GPSDO.

- Si hay un GPSDO instalado, una línea de estado verde indica "GPSDO installed. Manual frequency offset calibration available."
- Si no hay GPSDO instalado, una línea de estado amarilla indica "Manual frequency offset calibration available."

En ambos casos, los controles **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** son siempre visibles.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Introduzca una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración. Una etiqueta de estado a la derecha del botón muestra el texto de progreso.
   - "Starting…" aparece de inmediato.
   - El radio recibe `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0`, luego `radio pll_start` para iniciar el barrido.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en color ámbar y la calibración no se inicia.
4. Espere a que la etiqueta de estado indique la finalización. El botón **Start** se reactiva automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

### Controles de la pestaña RX

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración, introducida en MHz con seis decimales. | Se envía al radio como `radio set cal_freq=<value>`. |
| **Start** | Inicia el barrido de calibración. Se deshabilita y se etiqueta como **Busy** mientras hay una calibración en curso. | Restablece `freq_error_ppb` a 0 antes de iniciar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (ppb):** | Corrección manual de desviación de frecuencia en partes por mil millones. | |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones disponibles dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al selector y se actualiza en tiempo real. |

## Actualización de firmware (v0.9.3)

En la v0.9.3, el flujo de trabajo de actualización de firmware cambió. AetherSDR ya no descarga el instalador automáticamente. Cuando **Check for Update** informa que hay una versión más reciente disponible, descargue usted mismo el instalador de SmartSDR desde flexradio.com y luego use **Select Installer...** para prepararlo localmente.

### Formatos de instalador compatibles

| Formato | Extensión | Notas |
|---|---|---|
| Instalador WiX MSI | `.msi` | FlexRadio v4.2 y versiones posteriores. |
| Instalador EXE de extracción automática | `.exe` | Versiones anteriores de SmartSDR. |
| Archivo de firmware preextraído | `.ssdr` | Archivo de firmware directo, si ya dispone de uno. |

El preparador de firmware detecta automáticamente el formato a partir de los primeros 8
