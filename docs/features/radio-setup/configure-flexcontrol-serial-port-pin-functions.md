# Configurar las Funciones de los Pines del Puerto Serie de FlexControl

Use esta página para asignar una función y polaridad a los pines de salida DTR y RTS en el puerto serie conectado a su FlexControl u otro dispositivo conectado por serie. Esto permite que AetherSDR controle hardware externo — como líneas de PTT o entradas de keyer — a través de las señales de control del puerto serie.

## Antes de comenzar

- La radio debe estar conectada. La pestaña Serial requiere una conexión de radio activa.
- La pestaña Serial solo está presente cuando AetherSDR fue compilado con soporte para puerto serie (`HAVE_SERIALPORT`). Si no ve una pestaña Serial o un elemento de menú `Settings > FlexControl...`, su compilación no incluye esta característica.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...` — esto lo lleva directamente a la pestaña Serial de Radio Setup. O bien, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo serie de la lista. Haga clic en **Refresh** para volver a escanear si su dispositivo no aparece, o escriba la ruta directamente en el campo **Path**.
3. Configure los parámetros de la línea serie usando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con los requisitos de su dispositivo.
4. Para el pin **DTR**, seleccione la función deseada del cuadro combinado de función **DTR**, luego seleccione la polaridad activa del cuadro combinado **Polarity** adyacente.
5. Para el pin **RTS**, repita las mismas dos selecciones — función y polaridad — usando los cuadros combinados de función **RTS** y **Polarity**.
6. Si sus conexiones de paleta están invertidas, marque **Paddle Swap (swap dit/dah)**.
7. Para que AetherSDR abra este puerto automáticamente cada vez que inicie, marque **Auto-open serial port on startup**.
8. Si está conectando un botón de sintonía FlexControl, haga clic en **Detect** bajo **FlexControl Tuning Knob** para identificar el dispositivo. Haga clic en **Close** para liberarlo.
9. Para que AetherSDR detecte el botón FlexControl automáticamente al iniciar, marque **Auto-detect on startup**. Para invertir la dirección de sintonía, marque **Invert tuning direction**.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango válido / valores |
|---|---|---|---|
| **Port** | Selecciona o ingresa la ruta del dispositivo serie. | — | Puertos serie del sistema |
| **Refresh** | Vuelve a escanear los puertos serie disponibles. | — | — |
| **Path** | Campo editable que muestra la ruta del puerto seleccionado. | — | Cualquier ruta de dispositivo válida |
| **Baud** | Velocidad en baudios del puerto serie. | — | Según opciones del cuadro combinado |
| **Data** | Número de bits de datos. | — | Según opciones del cuadro combinado |
| **Parity** | Configuración de paridad. | — | Según opciones del cuadro combinado |
| **Stop** | Número de bits de parada. | — | Según opciones del cuadro combinado |
| **DTR: Function** | Asigna una función de señal al pin de salida DTR. | — | Según opciones del cuadro combinado |
| **DTR: Polarity** | Define la polaridad activa-alta o activa-baja para DTR. | — | Según opciones del cuadro combinado |
| **RTS: Function** | Asigna una función de señal al pin de salida RTS. | — | Según opciones del cuadro combinado |
| **RTS: Polarity** | Define la polaridad activa-alta o activa-baja para RTS. | — | Según opciones del cuadro combinado |
| **Paddle Swap (swap dit/dah)** | Invierte las entradas de paleta dit y dah. | Desmarcado | Marcado / Desmarcado |
| **Auto-open serial port on startup** | Reabre el puerto configurado cuando se inicia AetherSDR. | Desmarcado | Marcado / Desmarcado |
| **FlexControl Tuning Knob: Detect** | Detecta un botón FlexControl conectado. | — | — |
| **FlexControl Tuning Knob: Close** | Libera la conexión del botón FlexControl. | — | — |
| **Auto-detect on startup** | Detecta automáticamente el botón FlexControl al iniciar. | Desmarcado | Marcado / Desmarcado |
| **Invert tuning direction** | Invierte la dirección de sintonía de FlexControl. | Desmarcado | Marcado / Desmarcado |

## Cambios de actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware de la pestaña **Radio** ha cambiado. El botón **Browse .ssdr...** ha sido renombrado **Select Installer...** y ahora acepta tres tipos de archivo en lugar de solo un archivo `.ssdr` pre-extraído:

- `.msi` — el instalador SmartSDR basado en WiX utilizado por FlexRadio para firmware 4.2 y posterior.
- `.exe` — el instalador SmartSDR auto-extraíble más antiguo.
- `.ssdr` — un archivo de firmware pre-extraído (aceptado como antes).

El stager de firmware detecta automáticamente el formato del archivo a partir de los primeros 8 bytes (magic OLE/MSI para `.msi`, encabezado PE/COFF MZ para `.exe`) y extrae la carga útil `.ssdr` sin requerir herramientas externas. Una barra de progreso y la etiqueta de estado se actualizan mientras se ejecuta la extracción.

Además, el botón **Check for Update** ya no se convierte en un botón **Download** cuando se encuentra una versión de firmware más nueva. En su lugar, cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com usted mismo y luego haga clic en **Select Installer...** para organizarlo.

### Controles de firmware actualizados de la pestaña Radio

| Control | Qué hace | Notas |
|---|---|---|
| **Check for Update** | Consulta las actualizaciones de firmware disponibles e informa el resultado en la etiqueta de estado. | Cuando se encuentra una actualización, la etiqueta lo dirige a descargar el instalador desde flexradio.com. La etiqueta del botón ya no cambia a **Download**. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo `.msi`, `.exe` o `.ssdr`. El stager extrae y organiza el firmware automáticamente. | Renombrado de **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Inicia la carga de firmware a la radio con una barra de progreso. | Habilitado solo después de que el stager completa la extracción exitosamente. |

## Cambios de calibración de frecuencia en v0.9.2.1

La sección de calibración de frecuencia de la pestaña **RX** ha sido revisada. Anteriormente, el campo **Cal Frequency (MHz)** y el botón **Start** solo se mostraban cuando no se detectaba un GPSDO. A partir de v0.9.2.1, estos controles siempre son visibles independientemente de si hay un GPSDO instalado.

El mensaje de estado en la parte superior del grupo de calibración cambia según el hardware:

- GPSDO instalado — mostrado en verde: *GPSDO installed. Manual frequency offset calibration available.*
- Sin GPSDO — mostrado en ámbar: *Manual frequency offset calibration available.*

El botón **Start** ahora proporciona retroalimentación de estado en línea junto al botón. Mientras una calibración está en progreso, el botón está deshabilitado y su etiqueta cambia a **Busy**. La etiqueta de estado muestra la etapa actual (por ejemplo, *Starting…*) y se actualiza a medida que avanza la calibración. El botón se vuelve a habilitar cuando la calibración se completa o falla.

Antes de iniciar la calibración, AetherSDR ahora restablece el error de frecuencia almacenado a cero (`radio set freq_error_ppb=0`) antes de enviar `radio pll_start`. Si el campo **Cal Frequency (MHz)** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra *Enter cal frequency* en ámbar y la calibración no se inicia.

### Controles de calibración actualizados de la pestaña RX

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para calibración manual. | Ahora siempre se muestra, con o sin GPSDO. |
| **Start** | Inicia el barrido de calibración de frecuencia. | Deshabilitado y etiquetado **Busy** mientras está activo. Valida que se haya ingresado una frecuencia de calibración antes de continuar. |
| **Freq Offset (ppb):** | Desviación de frecuencia manual en partes por mil millones. | Se restablece a 0 automáticamente cuando se hace clic en **Start**. |

## Temas de color de slice (pestaña Themes)

La pestaña **Themes** fue añadida en v0.9.3 bajo Radio Setup. Aloja la sección **Slice Colors**, que le permite reemplazar los colores de slice integrados de AetherSDR con una paleta completamente personalizada por slice.

### Pasos

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Themes**.
2. Seleccione **Custom colors** para habilitar la asignación de color por slice. Seleccione **Use Aether defaults** para revertir a la paleta integrada.
3. Cuando **Custom colors** está seleccionado, haga clic en cualquier botón con letra (**A** a **H**) para abrir un selector de color para ese slice. El color se aplica inmediatamente en los widgets VFO, overlays de panadapter y badges de canal CAT.
4. Para revertir todos los slices a los colores integrados, haga clic en **Reset All to Defaults**.

### Controles de la pestaña Themes

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **Use Aether defaults** | Utiliza la paleta de colores de slice integrada de AetherSDR. | Seleccionado | Los botones de color de slice están deshabilitados cuando esto está activo. |
| **Custom colors** | Habilita la asignación de color por slice. | — | Activa los botones de color A–H. |
| **Botones de color de Slice A–H** | Haga clic en un botón con letra para abrir un selector de color para ese slice. Los cambios se aplican inmediatamente. | — | Hasta 8 slices soportados. Botones deshabilitados cuando **Use Aether defaults** está seleccionado. |
| **Reset All to Defaults** | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. | — | — |

## Pestaña External APD (solo FLEX-8x00)

La pestaña **APD** configura el muestreador de Predistorsión Adaptativa Externa. Solo es visible cuando la radio conectada informa `apd configurable=1`, lo que requiere una radio serie FLEX-8x00 ejecutando firmware SmartSDR 4.2.18 o posterior. La pestaña se oculta automáticamente para radios de la serie 6000 y para cualquier radio ejecutando firmware anterior a 4.2.18.

El sistema APD muestrea la señal RF saliente y utiliza la retroalimentación para entrenar un modelo de predistorsión que lineariza el transmisor. Cuando utiliza un amplificador lineal externo, puede seleccionar una entrada de recepción externa como ruta de retroalimentación en lugar del acoplador interno de la radio.

### Pasos

1. Abra `Settings > Radio Setup...`. Si la pestaña **APD** no es visible, su radio o firmware no soporta APD configurable.
2. Para cada antena TX (**ANT1**, **ANT2**, **XVTA**, **XVTB**), seleccione el puerto de muestra de retroalimentación del cuadro combinado correspondiente. Elija **INTERNAL** cuando transmita directamente a la carga o antena propia de la radio. Elija **RX_A**, **RX_B**, **XVTA** o **XVTB** cuando un acoplador direccional en esa entrada de recepción muestrea la salida de un amplificador externo.
3. Para borrar todos los datos de entrenamiento APD acumulados e reiniciar la adaptación desde cero, haga clic en **Equalizer Reset**.

### Controles de la pestaña APD

| Control | Qué hace | Predeterminado | Valores válidos |
|---|---|---|---|
| **Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB** | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear RF saliente para el entrenamiento de APD en esa antena TX. | INTERNAL | INTERNAL, RX_A, RX_B, XVTA, XVTB |
| **Equalizer Reset** | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience nuevamente. | — | — |

## Cambios de soporte de ShackSwitch en v0.9.4

La pestaña **Peripherals** obtiene una fila dedicada a ShackSwitch y un botón **⚙ Web UI** en v0.9.4. Anteriormente, la fila Antenna Genius mostraría un estado conectado incluso cuando el dispositivo conectado era un ShackSwitch. Los dos dispositivos ahora se manejan por separado.

### Cambio de comportamiento de la fila Antenna Genius

La fila de conexión/desconexión **Antenna Genius (AG)** ahora muestra un estado conectado solo cuando el dispositivo conectado es un Antenna Genius genuino. Si un ShackSwitch es el dispositivo conectado, la fila Antenna Genius se muestra como desconectada y la fila ShackSwitch se muestra como conectada en su lugar.

### Fila ShackSwitch

Se ha añadido una nueva fila **ShackSwitch** debajo de la fila Antenna Genius. Sigue el
