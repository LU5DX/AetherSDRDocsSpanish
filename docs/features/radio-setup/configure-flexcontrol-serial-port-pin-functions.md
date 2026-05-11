# Configurar las funciones de los pines del puerto serie de FlexControl

Use esta página para asignar una función y polaridad a los pines de salida DTR y RTS del puerto serie conectado a su FlexControl u otro dispositivo conectado en serie. Esto permite que AetherSDR controle hardware externo, como líneas PTT o entradas de manipulador, a través de las señales de control del puerto serie.

## Antes de comenzar

- La radio debe estar conectada. La pestaña Serial requiere una conexión activa a la radio.
- La pestaña Serial solo está presente cuando AetherSDR se compiló con soporte para puerto serie (`HAVE_SERIALPORT`). Si no ve una pestaña Serial o un elemento de menú `Settings > FlexControl...`, su compilación no incluye esta función.
- Conozca la ruta del dispositivo de su puerto serie (por ejemplo, `/dev/ttyUSB0` en Linux o `COM3` en Windows).

## Pasos

1. Abra `Settings > FlexControl...` — esto lo lleva directamente a la pestaña Serial de Radio Setup. Alternativamente, abra `Settings > Radio Setup...` y haga clic en la pestaña **Serial**.
2. En el cuadro combinado **Port**, seleccione su dispositivo serie de la lista. Haga clic en **Refresh** para volver a escanear si su dispositivo no aparece, o escriba la ruta directamente en el campo **Path**.
3. Configure los parámetros de la línea serie usando los cuadros combinados **Baud**, **Data**, **Parity** y **Stop** para que coincidan con los requisitos de su dispositivo.
4. Para el pin **DTR**, seleccione la función deseada en el cuadro combinado de función **DTR**, luego seleccione la polaridad activa en el cuadro combinado **Polarity** adyacente.
5. Para el pin **RTS**, repita las mismas dos selecciones — función y polaridad — usando los cuadros combinados de función **RTS** y **Polarity**.
6. Si sus conexiones de paddle están invertidas, marque **Paddle Swap (swap dit/dah)**.
7. Para que AetherSDR abra este puerto automáticamente cada vez que se inicie, marque **Auto-open serial port on startup**.
8. Si está conectando una perilla de sintonía FlexControl, haga clic en **Detect** debajo de **FlexControl Tuning Knob** para identificar el dispositivo. Haga clic en **Close** para liberarlo.
9. Para que AetherSDR detecte la perilla FlexControl automáticamente al inicio, marque **Auto-detect on startup**. Para invertir la dirección de sintonía, marque **Invert tuning direction**.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Valores/rango válidos |
|---|---|---|---|
| **Port** | Selecciona o ingresa la ruta del dispositivo serie. | — | Puertos serie del sistema |
| **Refresh** | Vuelve a escanear los puertos serie disponibles. | — | — |
| **Path** | Campo editable que muestra la ruta del puerto seleccionado. | — | Cualquier ruta de dispositivo válida |
| **Baud** | Velocidad en baudios del puerto serie. | — | Según opciones del cuadro combinado |
| **Data** | Número de bits de datos. | — | Según opciones del cuadro combinado |
| **Parity** | Configuración de paridad. | — | Según opciones del cuadro combinado |
| **Stop** | Número de bits de parada. | — | Según opciones del cuadro combinado |
| **DTR: Function** | Asigna una función de señal al pin de salida DTR. | — | Según opciones del cuadro combinado |
| **DTR: Polarity** | Establece polaridad activa en alto o activa en bajo para DTR. | — | Según opciones del cuadro combinado |
| **RTS: Function** | Asigna una función de señal al pin de salida RTS. | — | Según opciones del cuadro combinado |
| **RTS: Polarity** | Establece polaridad activa en alto o activa en bajo para RTS. | — | Según opciones del cuadro combinado |
| **Paddle Swap (swap dit/dah)** | Invierte las entradas de paddle dit y dah. | Sin marcar | Marcado / Sin marcar |
| **Auto-open serial port on startup** | Vuelve a abrir el puerto configurado cuando AetherSDR se inicia. | Sin marcar | Marcado / Sin marcar |
| **FlexControl Tuning Knob: Detect** | Detecta una perilla FlexControl conectada. | — | — |
| **FlexControl Tuning Knob: Close** | Libera la conexión de la perilla FlexControl. | — | — |
| **Auto-detect on startup** | Detecta automáticamente la perilla FlexControl al inicio. | Sin marcar | Marcado / Sin marcar |
| **Invert tuning direction** | Invierte la dirección de sintonía de FlexControl. | Sin marcar | Marcado / Sin marcar |

## Cambios en la actualización de firmware en v0.9.3

El flujo de trabajo de actualización de firmware de la pestaña **Radio** ha cambiado. El botón **Browse .ssdr...** ha sido renombrado a **Select Installer...** y ahora acepta tres tipos de archivo en lugar de solo un archivo `.ssdr` preextraído:

- `.msi` — el instalador SmartSDR basado en WiX utilizado por FlexRadio para firmware 4.2 y posteriores.
- `.exe` — el instalador SmartSDR autoextraíble más antiguo.
- `.ssdr` — un archivo de firmware preextraído (aceptado como antes).

El preparador de firmware detecta el formato del archivo automáticamente a partir de los primeros 8 bytes (OLE/MSI magic para `.msi`, cabecera PE/COFF MZ para `.exe`) y extrae la carga útil `.ssdr` sin necesidad de herramientas externas. Una barra de progreso y una etiqueta de estado se actualizan mientras se ejecuta la extracción.

Además, el botón **Check for Update** ya no se convierte en un botón **Download** cuando se encuentra una versión de firmware más reciente. En su lugar, cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador SmartSDR desde flexradio.com y luego haga clic en **Select Installer...** para prepararlo.

### Controles de firmware actualizados de la pestaña Radio

| Control | Qué hace | Notas |
|---|---|---|
| **Check for Update** | Consulta actualizaciones de firmware disponibles e informa el resultado en la etiqueta de estado. | Cuando se encuentra una actualización, la etiqueta le indica que descargue el instalador desde flexradio.com. La etiqueta del botón ya no cambia a **Download**. |
| **Select Installer...** | Abre un selector de archivos. Seleccione un archivo `.msi`, `.exe` o `.ssdr`. El preparador extrae y prepara el firmware automáticamente. | Renombrado de **Browse .ssdr...** en v0.9.3. |
| **Upload Firmware** | Inicia la carga del firmware a la radio con una barra de progreso. | Habilitado solo después de que el preparador complete la extracción exitosamente. |

## Cambios en la calibración de frecuencia en v0.9.2.1

La sección de calibración de frecuencia de la pestaña **RX** ha sido revisada. Anteriormente, el campo **Cal Frequency (MHz)** y el botón **Start** solo se mostraban cuando no se detectaba un GPSDO. A partir de v0.9.2.1, esos controles siempre están visibles independientemente de si hay un GPSDO instalado.

El mensaje de estado en la parte superior del grupo de calibración cambia según el hardware:

- GPSDO instalado — se muestra en verde: *GPSDO installed. Manual frequency offset calibration available.*
- Sin GPSDO — se muestra en ámbar: *Manual frequency offset calibration available.*

El botón **Start** ahora proporciona retroalimentación de estado en línea junto al botón. Mientras una calibración está en progreso, el botón está deshabilitado y su etiqueta cambia a **Busy**. La etiqueta de estado muestra la etapa actual (por ejemplo, *Starting…*) y se actualiza a medida que la calibración avanza. El botón se vuelve a habilitar cuando la calibración se completa o falla.

Antes de iniciar la calibración, AetherSDR ahora restablece el error de frecuencia almacenado a cero (`radio set freq_error_ppb=0`) antes de enviar `radio pll_start`. Si el campo **Cal Frequency (MHz)** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra *Enter cal frequency* en ámbar y la calibración no se inicia.

### Controles de calibración actualizados de la pestaña RX

| Control | Qué hace | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración manual. | Ahora siempre se muestra, con o sin GPSDO. |
| **Start** | Inicia el barrido de calibración de frecuencia. | Deshabilitado y etiquetado como **Busy** mientras está activo. Valida que se haya ingresado una frecuencia de calibración antes de continuar. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. | Se restablece a 0 automáticamente cuando se hace clic en **Start**. |

## Cambios en la fuente de referencia de 10 MHz en v0.9.7

El cuadro combinado **10 MHz Reference Source:** en la pestaña **RX** se ha actualizado para poblarse y mostrarse con mayor precisión según el hardware detectado y el estado del oscilador en vivo.

Anteriormente, el cuadro combinado solo listaba las opciones correspondientes al hardware detectado en el momento en que se abría el diálogo (TCXO, GPSDO, External), y la etiqueta de estado de bloqueo mostraba solo la cadena de estado del oscilador sin procesar seguida de "Locked" o "Unlocked". A partir de v0.9.7, el cuadro combinado y la etiqueta de estado se comportan de la siguiente manera.

### Población del cuadro combinado

El cuadro combinado se reconstruye dinámicamente. **Auto** siempre está presente. Las entradas adicionales aparecen cuando alguna de las siguientes condiciones es verdadera para esa fuente:

- La radio ha informado algún estado del oscilador (el campo de estado no está vacío) — en este caso **TCXO** y **External 10 MHz** siempre se incluyen.
- El hardware correspondiente se detecta (`tcxoPresent`, `gpsdoPresent`, `extPresent`).
- La fuente coincide con la configuración actual o el estado actual del oscilador.

La entrada para una referencia externa ahora está etiquetada como **External 10 MHz** en lugar de **External**.

El cuadro combinado selecciona la entrada que coincide con la configuración actual del oscilador de la radio. Si esa configuración no está en la lista, recurre a la selección actual del cuadro combinado y luego a **Auto**.

### Etiqueta de estado de bloqueo

La etiqueta de estado de bloqueo junto al cuadro combinado ahora muestra una descripción más rica:

- Cuando el estado del oscilador aún no se ha recibido: *Waiting for oscillator status* (mostrado en gris/azul).
- Cuando se selecciona **Auto** y la radio se ha resuelto a una fuente específica: *Auto -> <fuente resuelta>* (por ejemplo, *Auto -> GPSDO*).
- Cuando la configuración y el estado activo difieren: *<configuración> -> <estado activo>* (por ejemplo, *TCXO -> External 10 MHz*).
- De lo contrario: solo el nombre de la fuente activa.

En todos los casos, el estado de bloqueo se agrega: *Locked* (mostrado en verde) o *Unlocked* (mostrado en rojo). Si la fuente activa es **External 10 MHz** pero no se detecta ninguna referencia externa, se agrega *(not detected)* después del estado de bloqueo.

El color de la etiqueta es verde (`#00c040`) cuando está bloqueada, rojo (`#c04040`) cuando está desbloqueada y gris-azul (`#8aa8c0`) mientras espera el estado.

### Controles de fuente de referencia actualizados de la pestaña RX

| Control | Qué hace | Notas |
|---|---|---|
| **10 MHz Reference Source:** | Selecciona la fuente de referencia del oscilador. Envía `radio oscillator <valor>` a la radio cuando se cambia. | Entradas **Auto**, **TCXO**, **GPSDO** y **External 10 MHz**. Las opciones mostradas dependen del hardware detectado y del estado del oscilador en vivo. El valor `ext` informado por la radio se trata como equivalente a `external`. |
| Etiqueta de estado de bloqueo | Muestra la fuente activa, la resolución de Auto y el estado de bloqueo. Se actualiza en vivo a medida que la radio informa cambios en el estado del oscilador. | Verde = Bloqueado; Rojo = Desbloqueado; Gris-azul = esperando estado. Agrega *(not detected)* cuando External 10 MHz está activo pero no hay señal de referencia externa presente. |

## Temas de color de los slices (pestaña Themes)

La pestaña **Themes** se agregó en v0.9.3 bajo Radio Setup. Alberga la sección **Slice Colors**, que le permite reemplazar los colores de slice integrados de AetherSDR con una paleta completamente personalizada por slice.

### Pasos

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **Themes**.
2. Seleccione **Custom colors** para habilitar la asignación de color por slice. Seleccione **Use Aether defaults** para volver a la paleta integrada.
3. Cuando **Custom colors** esté seleccionado, haga clic en cualquier botón con letra (**A** a **H**) para abrir un selector de color para ese slice. El color surte efecto inmediatamente en los widgets VFO, las superposiciones del panadapter y las insignias de canal CAT.
4. Para revertir todos los slices a los colores integrados, haga clic en **Reset All to Defaults**.

### Controles de la pestaña Themes

| Control | Qué hace | Valor predeterminado | Notas |
|---|---|---|---|
| **Use Aether defaults** | Utiliza la paleta de colores de slice integrada de AetherSDR. | Seleccionado | Los botones de color de slice están deshabilitados cuando esto está activo. |
| **Custom colors** | Habilita la asignación de color por slice. | — | Activa los botones de color A–H. |
| **Slice A–H color buttons** | Abren un selector de color para cada letra de slice. | — | Los cambios se aplican inmediatamente. |

## Cambios en el diálogo Radio Setup en v26.5.1

El diálogo Radio Setup ahora utiliza una ventana sin marco con una barra de título personalizada. Esto proporciona una apariencia moderna coherente con otros diálogos de AetherSDR.

### Comportamiento de ventana sin marco

- El diálogo usa `Qt::FramelessWindowHint` cuando la aplicación está en modo sin marco.
- Se muestra una barra de título personalizada en la parte superior del diálogo con el título "Radio Setup".
- La barra de título se oculta cuando el modo sin marco está deshabilitado.
- El diálogo sigue siendo redimensionable; se instala un controlador de redimensionamiento sin marco.

### Borrado de IP en la pestaña Peripherals

La pestaña **Peripherals** ahora maneja correctamente el borrado de una dirección IP manual guardada para dispositivos TGXL, PGXL y Antenna Genius. Cuando se hace clic en el botón **Connect** / **Disconnect**, se aplica la siguiente lógica:

- Si está conectado y el campo IP se ha borrado, la IP manual guardada y el puerto se eliminan de la configuración antes de desconectar. Esto asegura que los manejadores posteriores (por ejemplo, la visibilidad del botón SmartSDR) vean la configuración borrada inmediatamente.
- Si está desconectado y el campo IP está vacío con una IP manual guardada previamente presente, al hacer clic en el botón se borra la IP manual y el puerto guardados de la configuración para que el dispositivo deje de conectarse automáticamente.
- Si está desconectado y el campo IP está vacío sin IP manual guardada, el botón no hace nada.

### Guardar al cerrar para campos IP de periféricos

Cuando cierra el diálogo Radio Setup, cualquier fila de la pestaña **
