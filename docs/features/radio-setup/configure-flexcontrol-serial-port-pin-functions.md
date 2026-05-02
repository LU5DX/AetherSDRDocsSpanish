# Configurar las funciones de los pines del puerto serie de FlexControl

Use esta página para asignar una función y polaridad a los pines de salida DTR y RTS del puerto serie conectado a su FlexControl u otro dispositivo serie. Esto permite que AetherSDR controle hardware externo — como líneas PTT o entradas de manipulador — a través de las señales de control del puerto serie.

## Antes de comenzar

- El radio debe estar conectado. La pestaña Serial requiere una conexión activa con el radio.
- La pestaña Serial solo está presente cuando AetherSDR fue compilado con soporte para puerto serie (`HAVE_SERIALPORT`). Si no ve una pestaña Serial ni el elemento de menú `Settings > FlexControl...`, su versión no incluye esta función.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...` — esto lleva directamente a la pestaña Serial de Radio Setup. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo serie de la lista. Haga clic en **Refresh** para volver a buscar si su dispositivo no aparece, o escriba la ruta directamente en el campo **Path**.
3. Configure los parámetros de la línea serie usando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con los requisitos de su dispositivo.
4. Para el pin **DTR**, seleccione la función deseada en el cuadro combinado de función **DTR**, luego seleccione la polaridad activa en el cuadro combinado **Polarity** adyacente.
5. Para el pin **RTS**, repita las mismas dos selecciones — función y polaridad — usando los cuadros combinados de función **RTS** y **Polarity**.
6. Si las conexiones de su paleta están invertidas, marque **Paddle Swap (swap dit/dah)**.
7. Para que AetherSDR abra este puerto automáticamente cada vez que inicie, marque **Auto-open serial port on startup**.
8. Si está conectando un mando de sintonía FlexControl, haga clic en **Detect** bajo **FlexControl Tuning Knob** para identificar el dispositivo. Haga clic en **Close** para liberarlo.
9. Para que AetherSDR detecte el mando FlexControl automáticamente al inicio, marque **Auto-detect on startup**. Para invertir la dirección de sintonía, marque **Invert tuning direction**.

## Qué hace cada control

| Control | Qué hace | Predeterminado | Rango / valores válidos |
|---|---|---|---|
| **Port** | Selecciona o introduce la ruta del dispositivo serie. | — | Puertos serie del sistema |
| **Refresh** | Vuelve a buscar puertos serie disponibles. | — | — |
| **Path** | Campo editable que muestra la ruta del puerto seleccionado. | — | Cualquier ruta de dispositivo válida |
| **Baud** | Velocidad en baudios del puerto serie. | — | Según las opciones del cuadro combinado |
| **Data** | Número de bits de datos. | — | Según las opciones del cuadro combinado |
| **Parity** | Configuración de paridad. | — | Según las opciones del cuadro combinado |
| **Stop** | Número de bits de parada. | — | Según las opciones del cuadro combinado |
| **DTR: Function** | Asigna una función de señal al pin de salida DTR. | — | Según las opciones del cuadro combinado |
| **DTR: Polarity** | Establece la polaridad activa-alta o activa-baja para DTR. | — | Según las opciones del cuadro combinado |
| **RTS: Function** | Asigna una función de señal al pin de salida RTS. | — | Según las opciones del cuadro combinado |
| **RTS: Polarity** | Establece la polaridad activa-alta o activa-baja para RTS. | — | Según las opciones del cuadro combinado |
| **Paddle Swap (swap dit/dah)** | Invierte las entradas dit y dah de la paleta. | Sin marcar | Marcado / Sin marcar |
| **Auto-open serial port on startup** | Reabre el puerto configurado cuando AetherSDR inicia. | Sin marcar | Marcado / Sin marcar |
| **FlexControl Tuning Knob: Detect** | Detecta un mando FlexControl conectado. | — | — |
| **FlexControl Tuning Knob: Close** | Libera la conexión con el mando FlexControl. | — | — |
| **Auto-detect on startup** | Detecta automáticamente el mando FlexControl al inicio. | Sin marcar | Marcado / Sin marcar |
| **Invert tuning direction** | Invierte la dirección de sintonía del FlexControl. | Sin marcar | Marcado / Sin marcar |

## Cambios en el flujo de actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware en la pestaña **Radio** ha cambiado. El botón **Browse .ssdr...** ha sido renombrado a **Select Installer...** y ahora acepta tres tipos de archivo en lugar de solo un archivo `.ssdr` previamente extraído:

- `.msi` — el instalador SmartSDR basado en WiX que utiliza FlexRadio para el firmware 4.2 y posteriores.
- `.exe` — el instalador SmartSDR autoextraíble más antiguo.
- `.ssdr` — un archivo de firmware previamente extraído (aceptado como antes).

El preparador de firmware detecta el formato del archivo automáticamente a partir de los primeros 8 bytes (OLE/MSI magic para `.msi`, encabezado PE/COFF MZ para `.exe`) y extrae el contenido `.ssdr` sin requerir herramientas externas. Una barra de progreso y una etiqueta de estado se actualizan mientras se ejecuta la extracción.

Además, el botón **Check for Update** ya no cambia a un botón **Download** cuando se encuentra una versión de firmware más reciente. En su lugar, cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com usted mismo y luego haga clic en **Select Installer...** para prepararlo.

### Controles de firmware actualizados en la pestaña Radio

| Control | Qué hace | Notas |
|---|---|---|
| **Check for Update** | Consulta las actualizaciones de firmware disponibles e informa el resultado en la etiqueta de estado. | Cuando se encuentra una actualización, la etiqueta le indica que descargue el instalador desde flexradio.com. La etiqueta del botón ya no cambia a **Download**. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo `.msi`, `.exe` o `.ssdr`. El preparador extrae y prepara el firmware automáticamente. | Renombrado desde **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Inicia la carga del firmware al radio con una barra de progreso. | Se habilita solo después de que el preparador complete la extracción con éxito. |

## Cambios en la calibración de frecuencia en v0.9.2.1

La sección de calibración de frecuencia en la pestaña **RX** ha sido revisada. Anteriormente, el campo **Cal Frequency (MHz)** y el botón **Start** solo se mostraban cuando no se detectaba un GPSDO. A partir de v0.9.2.1, esos controles son siempre visibles independientemente de si hay un GPSDO instalado.

El mensaje de estado en la parte superior del grupo de calibración cambia según el hardware:

- GPSDO instalado — se muestra en verde: *GPSDO installed. Manual frequency offset calibration available.*
- Sin GPSDO — se muestra en ámbar: *Manual frequency offset calibration available.*

El botón **Start** ahora proporciona retroalimentación de estado en línea junto al botón. Mientras una calibración está en curso, el botón se deshabilita y su etiqueta cambia a **Busy**. La etiqueta de estado muestra la etapa actual (por ejemplo, *Starting…*) y se actualiza conforme avanza la calibración. El botón se vuelve a habilitar cuando la calibración se completa o falla.

Antes de iniciar la calibración, AetherSDR ahora restablece el error de frecuencia almacenado a cero (`radio set freq_error_ppb=0`) antes de enviar `radio pll_start`. Si el campo **Cal Frequency (MHz)** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra *Enter cal frequency* en ámbar y la calibración no inicia.

### Controles de calibración actualizados en la pestaña RX

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | Ahora siempre visible, con o sin GPSDO. |
| **Start** | Inicia el barrido de calibración de frecuencia. | Se deshabilita y se etiqueta **Busy** mientras está activo. Valida que se haya ingresado una frecuencia de calibración antes de continuar. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por billón. | Se restablece a 0 automáticamente cuando se hace clic en **Start**. |

## Temas de color para slices (pestaña Themes)

La pestaña **Themes** fue agregada en v0.9.3 bajo Radio Setup. Contiene la sección **Slice Colors**, que permite reemplazar los colores de slice predeterminados de AetherSDR con una paleta personalizada por slice.

### Pasos

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Themes**.
2. Seleccione **Custom colors** para habilitar la asignación de color por slice. Seleccione **Use Aether defaults** para volver a la paleta predeterminada.
3. Cuando **Custom colors** está seleccionado, haga clic en cualquier botón con letra (**A** a **H**) para abrir un selector de color para ese slice. El color se aplica inmediatamente en los widgets de VFO, las superposiciones del panadapter y las insignias de canal CAT.
4. Para revertir todos los slices a los colores predeterminados, haga clic en **Reset All to Defaults**.

### Controles de la pestaña Themes

| Control | Qué hace | Predeterminado | Notas |
|---|---|---|---|
| **Use Aether defaults** | Usa la paleta de colores de slice predeterminada de AetherSDR. | Seleccionado | Los botones de color de slice se deshabilitan cuando está activo. |
| **Custom colors** | Habilita la asignación de color por slice. | — | Activa los botones de color A–H. |
| **Botones de color de slice A–H** | Haga clic en un botón con letra para abrir un selector de color para ese slice. Los cambios se aplican inmediatamente. | — | Se admiten hasta 8 slices. Los botones se deshabilitan cuando **Use Aether defaults** está seleccionado. |
| **Reset All to Defaults** | Restablece todos los colores de slice personalizados a la paleta predeterminada de AetherSDR. | — | — |

## Pestaña APD externa (solo FLEX-8x00)

La pestaña **APD** configura el muestreador de Predistorsión Adaptativa Externa. Solo es visible cuando el radio conectado reporta `apd configurable=1`, lo que requiere un radio de la serie FLEX-8x00 con firmware SmartSDR 4.2.18 o posterior. La pestaña se oculta automáticamente para los radios de la serie 6000 y para cualquier radio con firmware anterior a 4.2.18.

El sistema APD muestrea la señal de RF saliente y utiliza la retroalimentación para entrenar un modelo de predistorsión que linealiza el transmisor. Al operar un amplificador lineal externo, puede seleccionar una entrada de recepción externa como ruta de retroalimentación en lugar del acoplador interno del radio.

### Pasos

1. Abra `Settings > Radio Setup...`. Si la pestaña **APD** no es visible, su radio o firmware no admite APD configurable.
2. Para cada antena de TX (**ANT1**, **ANT2**, **XVTA**, **XVTB**), seleccione el puerto de muestra de retroalimentación en el cuadro combinado correspondiente. Elija **INTERNAL** cuando transmita directamente hacia la carga o antena propia del radio. Elija **RX_A**, **RX_B**, **XVTA** o **XVTB** cuando un acoplador direccional en esa entrada de recepción muestree la salida de un amplificador externo.
3. Para borrar todos los datos de entrenamiento APD acumulados y reiniciar la adaptación desde cero, haga clic en **Equalizer Reset**.

### Controles de la pestaña APD

| Control | Qué hace | Predeterminado | Valores válidos |
|---|---|---|---|
| **Cuadros combinados de muestreador ANT1 / ANT2 / XVTA / XVTB** | Selecciona la ruta de retroalimentación que el radio utiliza para muestrear la RF saliente en el entrenamiento APD para esa antena TX. | INTERNAL | INTERNAL, RX_A, RX_B, XVTA, XVTB |
| **Equalizer Reset** | Envía `apd reset` al radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience desde cero. | — | — |

## Cambios en el soporte de ShackSwitch en v0.9.4

La pestaña **Peripherals** incorpora una fila dedicada a ShackSwitch y un botón **⚙ Web UI** en v0.9.4. Anteriormente, la fila de Antenna Genius mostraba un estado conectado incluso cuando el dispositivo conectado era un ShackSwitch. Los dos dispositivos ahora se manejan por separado.

### Cambio de comportamiento en la fila de Antenna Genius

La fila Connect/Disconnect de **Antenna Genius (AG)** ahora muestra un estado conectado solo cuando el dispositivo conectado es un Antenna Genius genuino. Si el dispositivo conectado es un ShackSwitch, la fila de Antenna Genius se muestra como desconectada y la fila de ShackSwitch se muestra como conectada en su lugar.

### Fila de ShackSwitch

Se ha agregado una nueva fila **ShackSwitch** debajo de la fila de Antenna Genius. Sigue el
