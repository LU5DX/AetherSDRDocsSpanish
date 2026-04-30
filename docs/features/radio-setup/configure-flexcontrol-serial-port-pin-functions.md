# Configurar las funciones de los pines del puerto serie de FlexControl

Utilice esta página para asignar una función y polaridad a los pines de salida DTR y RTS del puerto serie conectado a su FlexControl u otro dispositivo conectado por serie. Esto permite que AetherSDR controle hardware externo, como líneas PTT o entradas de manipulador, a través de las señales de control del puerto serie.

## Antes de comenzar

- La radio debe estar conectada. La pestaña Serial requiere una conexión de radio activa.
- La pestaña Serial solo está presente cuando AetherSDR se compiló con soporte de puerto serie (`HAVE_SERIALPORT`). Si no ve una pestaña Serial o un elemento de menú `Settings > FlexControl...`, su compilación no incluye esta función.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...` — esto le lleva directamente a la pestaña Serial de Radio Setup. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo serie de la lista. Haga clic en **Refresh** para volver a explorar si su dispositivo no aparece, o escriba la ruta directamente en el campo **Path**.
3. Establezca los parámetros de la línea serie utilizando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con los requisitos de su dispositivo.
4. Para el pin **DTR**, seleccione la función deseada del cuadro combinado de función **DTR**, luego seleccione la polaridad activa del cuadro combinado **Polarity** adyacente.
5. Para el pin **RTS**, repita las mismas dos selecciones — función y polaridad — utilizando los cuadros combinados de función **RTS** y **Polarity**.
6. Si las conexiones de su manipulador están invertidas, marque **Paddle Swap (swap dit/dah)**.
7. Para que AetherSDR abra este puerto automáticamente cada vez que se inicie, marque **Auto-open serial port on startup**.
8. Si está conectando una perilla de sintonía FlexControl, haga clic en **Detect** bajo **FlexControl Tuning Knob** para identificar el dispositivo. Haga clic en **Close** para liberarlo.
9. Para que AetherSDR detecte la perilla FlexControl automáticamente al inicio, marque **Auto-detect on startup**. Para invertir la dirección de sintonía, marque **Invert tuning direction**.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango/valores válidos |
|---|---|---|---|
| **Port** | Selecciona o ingresa la ruta del dispositivo serie. | — | Puertos serie del sistema |
| **Refresh** | Vuelve a explorar los puertos serie disponibles. | — | — |
| **Path** | Campo editable que muestra la ruta del puerto seleccionado. | — | Cualquier ruta de dispositivo válida |
| **Baud** | Velocidad en baudios del puerto serie. | — | Según las opciones del cuadro combinado |
| **Data** | Número de bits de datos. | — | Según las opciones del cuadro combinado |
| **Parity** | Configuración de paridad. | — | Según las opciones del cuadro combinado |
| **Stop** | Número de bits de parada. | — | Según las opciones del cuadro combinado |
| **DTR: Function** | Asigna una función de señal al pin de salida DTR. | — | Según las opciones del cuadro combinado |
| **DTR: Polarity** | Establece la polaridad activa alta o activa baja para DTR. | — | Según las opciones del cuadro combinado |
| **RTS: Function** | Asigna una función de señal al pin de salida RTS. | — | Según las opciones del cuadro combinado |
| **RTS: Polarity** | Establece la polaridad activa alta o activa baja para RTS. | — | Según las opciones del cuadro combinado |
| **Paddle Swap (swap dit/dah)** | Invierte las entradas de manipulador dit y dah. | Sin marcar | Marcado / Sin marcar |
| **Auto-open serial port on startup** | Reabre el puerto configurado cuando se inicia AetherSDR. | Sin marcar | Marcado / Sin marcar |
| **FlexControl Tuning Knob: Detect** | Detecta una perilla FlexControl conectada. | — | — |
| **FlexControl Tuning Knob: Close** | Libera la conexión de la perilla FlexControl. | — | — |
| **Auto-detect on startup** | Detecta automáticamente la perilla FlexControl al iniciar. | Sin marcar | Marcado / Sin marcar |
| **Invert tuning direction** | Invierte la dirección de la sintonía de FlexControl. | Sin marcar | Marcado / Sin marcar |

## Cambios de actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware de la pestaña **Radio** ha cambiado. El botón **Browse .ssdr...** ha sido renombrado a **Select Installer...** y ahora acepta tres tipos de archivo en lugar de solo un archivo `.ssdr` preextraído:

- `.msi` — el instalador SmartSDR basado en WiX utilizado por FlexRadio para firmware 4.2 y posterior.
- `.exe` — el instalador SmartSDR autoextraíble más antiguo.
- `.ssdr` — un archivo de firmware preextraído (aceptado como antes).

El organizador de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magic OLE/MSI para `.msi`, encabezado PE/COFF MZ para `.exe`) y extrae la carga útil `.ssdr` sin requerir herramientas externas. Una barra de progreso y una etiqueta de estado se actualizan mientras se ejecuta la extracción.

Además, el botón **Check for Update** ya no cambia a un botón **Download** cuando se encuentra una versión de firmware más nueva. En su lugar, cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com usted mismo y luego haga clic en **Select Installer...** para organizarlo.

### Controles de firmware de la pestaña Radio actualizados

| Control | Qué hace | Notas |
|---|---|---|
| **Check for Update** | Consulta las actualizaciones de firmware disponibles e informa el resultado en la etiqueta de estado. | Cuando se encuentra una actualización, la etiqueta le dirige a descargar el instalador desde flexradio.com. La etiqueta del botón ya no cambia a **Download**. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo `.msi`, `.exe` o `.ssdr`. El organizador extrae y organiza el firmware automáticamente. | Renombrado de **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Inicia la carga de firmware a la radio con una barra de progreso. | Habilitado solo después de que el organizador complete la extracción correctamente. |

## Cambios de calibración de frecuencia en v0.9.2.1

La sección de calibración de frecuencia de la pestaña **RX** ha sido revisada. Anteriormente, el campo **Cal Frequency (MHz)** y el botón **Start** solo se mostraban cuando no se detectaba un GPSDO. A partir de v0.9.2.1, esos controles siempre son visibles independientemente de si hay un GPSDO instalado.

El mensaje de estado en la parte superior del grupo de calibración cambia según el hardware:

- GPSDO instalado — mostrado en verde: *GPSDO installed. Manual frequency offset calibration available.*
- Sin GPSDO — mostrado en ámbar: *Manual frequency offset calibration available.*

El botón **Start** ahora proporciona retroalimentación de estado en línea junto al botón. Mientras se ejecuta una calibración, el botón está deshabilitado y su etiqueta cambia a **Busy**. La etiqueta de estado muestra la etapa actual (por ejemplo, *Starting…*) y se actualiza mientras la calibración procede. El botón se vuelve a habilitar cuando la calibración se completa o falla.

Antes de iniciar la calibración, AetherSDR ahora restablece el error de frecuencia almacenado a cero (`radio set freq_error_ppb=0`) antes de enviar `radio pll_start`. Si el campo **Cal Frequency (MHz)** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra *Enter cal frequency* en ámbar y la calibración no se inicia.

### Controles de calibración de la pestaña RX actualizados

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | Ahora siempre se muestra, con o sin GPSDO. |
| **Start** | Inicia el barrido de calibración de frecuencia. | Deshabilitado y etiquetado **Busy** mientras está activo. Valida que se haya ingresado una frecuencia de calibración antes de proceder. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. | Se restablece a 0 automáticamente cuando se hace clic en **Start**. |

## Temas de colores de slice (pestaña Themes)

La pestaña **Themes** se agregó en v0.9.3 en Radio Setup. Aloja la sección **Slice Colors**, que le permite reemplazar los colores de slice integrados de AetherSDR con una paleta completamente personalizada por slice.

### Pasos

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Themes**.
2. Seleccione **Custom colors** para habilitar la asignación de color por slice. Seleccione **Use Aether defaults** para revertir a la paleta integrada.
3. Cuando **Custom colors** está seleccionado, haga clic en cualquier botón con letra (**A** a **H**) para abrir un selector de color para ese slice. El color toma efecto inmediatamente en los widgets VFO, superposiciones de panadapter e insignias de canal CAT.
4. Para revertir todos los slices a los colores integrados, haga clic en **Reset All to Defaults**.

### Controles de la pestaña Themes

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **Use Aether defaults** | Utiliza la paleta de colores de slice integrada de AetherSDR. | Seleccionado | Los botones de color de slice están deshabilitados cuando esto está activo. |
| **Custom colors** | Habilita la asignación de color por slice. | — | Activa los botones de color A–H. |
| **Botones de color Slice A–H** | Haga clic en un botón con letra para abrir un selector de color para ese slice. Los cambios se aplican inmediatamente. | — | Se admiten hasta 8 slices. Los botones están deshabilitados cuando **Use Aether defaults** está seleccionado. |
| **Reset All to Defaults** | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — | — |

## Pestaña APD externo (solo FLEX-8x00)

La pestaña **APD** configura el muestreador de Predistorsión Adaptativa Externa. Solo es visible cuando la radio conectada informa `apd configurable=1`, lo que requiere una radio serie FLEX-8x00 que ejecute firmware SmartSDR 4.2.18 o posterior. La pestaña se oculta automáticamente para radios serie 6000 y para cualquier radio que ejecute firmware anterior a 4.2.18.

El sistema APD muestrea la señal RF saliente y utiliza la retroalimentación para entrenar un modelo de predistorsión que linealiza el transmisor. Cuando controla un amplificador lineal externo, puede seleccionar una entrada de recepción externa como la ruta de retroalimentación en lugar del acoplador interno de la radio.

### Pasos

1. Abra `Settings > Radio Setup...`. Si la pestaña **APD** no es visible, su radio o firmware no admite APD configurable.
2. Para cada antena TX (**ANT1**, **ANT2**, **XVTA**, **XVTB**), seleccione el puerto de muestra de retroalimentación del cuadro combinado correspondiente. Elija **INTERNAL** cuando transmita directamente a la carga o antena propia de la radio. Elija **RX_A**, **RX_B**, **XVTA** o **XVTB** cuando un acoplador direccional en esa entrada de recepción muestree la salida de un amplificador externo.
3. Para borrar todos los datos de entrenamiento APD acumulados e reiniciar la adaptación desde cero, haga clic en **Equalizer Reset**.

### Controles de la pestaña APD

| Control | Qué hace | Predeterminado | Valores válidos |
|---|---|---|---|
| **Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB** | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear RF saliente para el entrenamiento APD en esa antena TX. | INTERNAL | INTERNAL, RX_A, RX_B, XVTA, XVTB |
| **Equalizer Reset** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. | — | — |

## Consejos

- Si abre Radio Setup a través de `Settings > Radio Setup...` en lugar de `Settings > FlexControl...`, la pestaña Serial aparece en el extremo derecho de la barra de pestañas. Desplácese o amplíe el diálogo si la pestaña no es visible.
- La pestaña Serial se construye perezosamente — no se construye hasta que hace clic en ella por primera vez, por lo que hay una breve pausa la primera vez que la selecciona.
- En la pestaña RX, si tiene un GPSDO instalado aún puede ejecutar una calibración manual. Ingrese la frecuencia de referencia en **Cal Frequency (MHz)** y haga clic en **Start**.
- La pestaña **APD** aparece y desaparece dinámicamente cuando la radio informa sus capacidades. Si conecta una radio diferente que no admite APD configurable, la pestaña se oculta sin requerir reinicio.
- Los cambios de color de la pestaña **Themes** toman efecto inmediatamente.
