# Calibrar la desviación de frecuencia del GPSDO

Utilice esta página para corregir la referencia de frecuencia de su FLEX-8600 usando los controles de calibración integrados. Una calibración precisa de la frecuencia reduce el error de marcación en todas las bandas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña RX en Configuración de la radio solo está disponible cuando hay una conexión activa con la radio.
- Si hay un GPSDO instalado, los controles de calibración siguen estando disponibles. Sin un GPSDO, se muestra un mensaje de estado amarillo en lugar de la confirmación verde del GPSDO.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. En **Cal Frequency (MHz):**, ingrese la frecuencia de una señal de referencia de precisión conocida.
4. Haga clic en **Start** para comenzar el barrido de calibración. La etiqueta del botón cambia a **Busy** y aparece un mensaje de estado mientras se ejecuta el barrido. El botón **Start** está deshabilitado hasta que el barrido se complete o falle.
5. Cuando el barrido se complete, revise la desviación medida que se muestra en **Freq Offset (ppb):**.
6. Si prefiere ajustar la desviación manualmente en lugar de usar el resultado del barrido, edite **Freq Offset (ppb):** directamente.

## Qué hace cada control

| Control | Tipo | Descripción |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | La frecuencia de referencia utilizada durante el barrido de calibración. Ajústela a una señal de precisión conocida — por ejemplo, una estación de frecuencia patrón de radiodifusión. El campo no debe estar vacío antes de hacer clic en **Start**; si está vacío, se muestra una advertencia y el barrido no comienza. |
| **Start** | Botón pulsador | Inicia el barrido de calibración en la frecuencia ingresada en **Cal Frequency (MHz):**. Antes de comenzar, AetherSDR restablece el error de frecuencia actual a cero (`freq_error_ppb=0`) para que el barrido comience desde una línea base limpia. El botón se deshabilita y muestra **Busy** mientras el barrido está en curso. |
| **Freq Offset (ppb):** | Spinbox | La desviación de frecuencia aplicada al oscilador de referencia de la radio, en partes por mil millones. Puede ser ajustada por el barrido o ingresada manualmente. |
| **10 MHz Reference Source:** | Combo box | Selecciona la fuente de referencia del oscilador. Valores válidos: `Auto` \| `TCXO` \| `GPSDO` \| `External 10 MHz`. Las opciones mostradas dependen del hardware instalado y de los estados informados por la radio en el momento en que se construye la pestaña. El combo se completa dinámicamente: las entradas TCXO y External 10 MHz aparecen siempre que la radio informe su presencia o cuando coinciden con la configuración o el estado actual; GPSDO aparece cuando se detecta un GPSDO o cuando la configuración o el estado actual es `gpsdo`. Si la radio informa una fuente que aún no está en la lista, se agrega automáticamente. El estado de bloqueo se muestra junto al combo box y se actualiza en vivo (consulte [Etiqueta de estado del oscilador](#etiqueta-de-estado-del-oscilador)). |
| **TX Follows Active Slice** | Botón pulsador | TX sigue a la slice activa. Se excluye mutuamente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. |
| **Active Slice Follows TX** | Botón pulsador | Cambia la slice activa cuando TX se mueve externamente (por ejemplo, desde WSJT-X o CAT). Se excluye mutuamente con **TX Follows Active Slice**. |
| **Controles deslizantes de nitidez de filtro (Voice / CW / Digital)** | Control deslizante | Ajusta la nitidez del filtro (0 = latencia más baja a 3 = más nítido) por modo. El control deslizante está deshabilitado cuando **Auto** está activado para ese modo. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón pulsador | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar para que AetherSDR se reconecte automáticamente al inicio. Requerido para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando `autotune` nativo directamente al TGXL en lugar de la ruta del lado de la radio, que está rota en el firmware 4.2. El TGXL activa el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita ninguna señalización de PTT por parte del cliente. Si el campo IP está vacío y la radio ya ha descubierto el TGXL, la IP descubierta se precompleta. Si el campo IP se limpia y hace clic en **Connect** mientras está desconectado, la IP y el puerto manuales guardados se borran de la configuración y el botón regresa sin conectar. Si el campo IP se limpia mientras está conectado y hace clic en **Disconnect**, la IP y el puerto manuales guardados se borran antes de que se ejecute la desconexión, por lo que los visores de estado posteriores ven el estado limpiado de inmediato. Cerrar el diálogo con un campo IP vacío y sin un clic en Connect pendiente también borra cualquier IP y puerto manuales previamente guardados, y se desconecta si está actualmente conectado. |
| **Connect / Disconnect (PGXL)** | Botón pulsador | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. Se comporta de manera idéntica a la fila TGXL con respecto a la limpieza de IP vacía al desconectar o cerrar el diálogo. |
| **Connect / Disconnect (Antenna Genius)** | Botón pulsador | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Conectado si un ShackSwitch (en lugar de un Antenna Genius) es el dispositivo conectado. Se comporta de manera idéntica a la fila TGXL con respecto a la limpieza de IP vacía al desconectar o cerrar el diálogo. |
| **Connect / Disconnect (ShackSwitch)** | Botón pulsador | Abre o cierra una conexión a un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo `ShackSwitch` en la baliza de difusión AG. El descubrimiento automático a través de UDP también funciona sin esta fila. La fila se oculta del estado Conectado si un Antenna Genius (que no es ShackSwitch) es el dispositivo conectado. Se comporta de manera idéntica a la fila TGXL con respecto a la limpieza de IP vacía al desconectar o cerrar el diálogo. |
| **⚙ Web UI (ShackSwitch)** | Botón pulsador | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` de la baliza si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| **Select Installer...** | Botón pulsador | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El preparador de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (marca OLE/MSI vs PE/COFF MZ) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego haga clic en **Select Installer...** para prepararlo. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| **APD (pestaña)** | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de retroalimentación (`INTERNAL` / `RX_A` / `RX_B` / `XVTA` / `XVTB`) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las radios de la serie 6000 y anteriores a 4.2.18 mantienen la pestaña invisible. |
| **Combos de muestreador (APD) para ANT1 / ANT2 / XVTA / XVTB** | Combo box | Selecciona la ruta de retroalimentación que la radio utiliza para muestrear la RF de salida para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando controle un amplificador lineal externo. Las opciones se completan en vivo desde el subobjeto `apd sampler` de la radio. Vuelve a `INTERNAL` si la radio informa un valor no reconocido. |
| **Equalizer Reset (APD)** | Botón pulsador | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| **Themes (pestaña)** | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente aloja la sección de Colores de Slice. |
| **Use Aether defaults / Custom colors** | Botón de opción | Cambia el esquema de color de las slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. |
| **Botones de color para Slice A–H** | Botón pulsador | Haga clic en cualquier botón con letras (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles de inmediato en los widgets de VFO, superposiciones del panadapter e insignias de canal CAT. Los botones están deshabilitados cuando se selecciona **Use Aether defaults**. Se admiten hasta 8 slices. |
| **Reset All to Defaults (Themes)** | Botón pulsador | Restablece todos los colores de slice personalizados a la paleta integrada de AetherSDR. |
| **WheelRit** | Acción de FlexControl | Asigna el control RIT a la perilla de sintonía. Disponible en la asignación de acciones de los botones de FlexControl. Agregado en v26.5.1. |
| **WheelXit** | Acción de FlexControl | Asigna el control XIT a la perilla de sintonía. Disponible en la asignación de acciones de los botones de FlexControl. Agregado en v26.5.1. |

## Etiqueta de estado del oscilador

A partir de v0.9.7, la etiqueta de estado de bloqueo junto a **10 MHz Reference Source:** muestra información más rica que el texto simple anterior `<SOURCE> Locked / Unlocked`.

La etiqueta se construye de la siguiente manera:

- Si la radio aún no ha informado un estado del oscilador, la etiqueta muestra **Waiting for oscillator status** en un color gris azulado neutro.
- Si el estado activo difiere de la configuración establecida (por ejemplo, **Auto** está seleccionado pero la radio ha elegido **GPSDO**), la etiqueta muestra la transición: `Auto -> GPSDO`.
- Si tanto la configuración como el estado son conocidos y coinciden, solo se muestra el nombre de la fuente activa.
- **Locked** o **Unlocked** siempre se agrega después del nombre de la fuente.
- Si la fuente es **External 10 MHz** pero la radio informa que no hay señal externa presente, la etiqueta agrega **(not detected)**.

Codificación de colores:

| Color | Significado |
|---|---|
| Verde (`#00c040`) | El oscilador está bloqueado. |
| Rojo (`#c04040`) | El oscilador está desbloqueado. |
| Gris azulado (`#8aa8c0`) | El estado del oscilador aún no se ha recibido de la radio. |

La etiqueta se actualiza en vivo a medida que la radio informa cambios de estado. No se requiere ninguna acción para actualizarla.

La opción **External** en el combo box ahora está etiquetada como **External 10 MHz** (cambió de **External** en v0.9.7) para coincidir con la etiqueta utilizada en el texto de estado.

## Mensajes de estado de calibración

A partir de v0.9.2.1, aparece una etiqueta de estado junto al botón **Start** y se actualiza durante todo el barrido.

| Mensaje | Color | Significado |
|---|---|---|
| Starting... | Gris azulado | La secuencia de comandos de calibración se ha enviado a la radio. |
| Enter cal frequency | Ámbar | **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Ingrese una frecuencia e intente de nuevo. |
| Busy | — | Se muestra en el propio botón **Start** mientras un barrido está en curso. |

## Banner de estado del GPSDO

El banner en la parte superior del grupo de calibración refleja si hay un GPSDO instalado:

- **Banner verde** — El GPSDO está instalado. La calibración manual de la desviación de frecuencia sigue estando disponible.
- **Banner ámbar** — No hay GPSDO instalado. La calibración manual de la desviación de frecuencia está disponible.

En v0.9.2.1, el texto del banner verde cambió. Anteriormente decía "GPSDO is installed. Frequency error correction is not required." Ahora dice "GPSDO installed. Manual frequency offset calibration available." Esto hace que el comportamiento sea consistente: los controles de calibración siempre se muestran independientemente de la presencia del GPSDO.

## Flujo de actualización de firmware (v0.9.3)

En v0.9.3, el flujo de actualización de firmware cambió. AetherSDR ya no descarga y prepara el firmware automáticamente cuando se detecta una actualización. En su lugar:

1. Haga clic en **Check for Update** en la pestaña **Radio**. Si hay una actualización disponible, la etiqueta de estado muestra el número de versión y le indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador desde flexradio.com (`.msi` para SmartSDR 4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** (anteriormente etiquetado **Browse .ssdr...**) y elija el archivo descargado. AetherSDR acepta archivos `.msi`, `.exe` o un archivo `.ssdr` preextraído y prepara el firmware automáticamente, detectando el formato a partir del encabezado del archivo.
4. Una vez que la preparación se complete, haga clic en **Upload Firmware** para transferir el firmware a la radio.

El botón **Check for Update** ya no se vuelve a etiquetar como un desencadenador de descarga después de detectar una actualización disponible.

## ShackSwitch

## Modo de ventana sin marco (v26.5.1)

A partir de v26.5.1, el diálogo de Configuración de la radio utiliza una ventana sin marco con una barra de título personalizada cuando la configuración a nivel de aplicación **FramelessWindow** está habilitada (valor predeterminado: `True`). La barra de título personalizada muestra "Radio Setup" y admite operaciones estánd
