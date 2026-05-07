# Crear una nueva entrada de transverter

Utilice esta página para agregar una definición de transverter a su FLEX-8600, de modo que AetherSDR conozca el desplazamiento de frecuencia FI a RF y los parámetros operativos para su banda de transverter.

## Antes de comenzar

- La radio debe estar conectada. La configuración de radio requiere una conexión activa con la radio.
- Conozca el rango de frecuencia FI que utiliza su transverter y el desplazamiento de frecuencia RF que desea visualizar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.
4. Aparece una nueva pestaña anidada. Configure los campos para la nueva entrada en esa pestaña.
5. Para restringir la entrada solo a recepción, active **RX Only:** en el estado habilitado.
6. Para eliminar una entrada que ya no necesita, haga clic en **Remove** en la pestaña de esa entrada.
7. Cierre el diálogo con **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Agrega una nueva entrada de transverter y abre su pestaña de configuración. |
| **RX Only:** | Botón de alternancia | Fuerza el transverter a solo recepción, impidiendo la transmisión a través de él. |
| **Remove** | Botón | Elimina permanentemente la definición de transverter seleccionada. |
| TX Follows Active Slice | Botón | TX sigue la slice activa. Es mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante la operación en Split. |
| Active Slice Follows TX | Botón | Cambia la slice activa cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Es mutuamente excluyente con TX Follows Active Slice. |
| Deslizadores de nitidez de filtro Voice / CW / Digital | Deslizador | Ajusta la nitidez del filtro (0=menor latencia a 3=más nítido) por modo; el deslizador está deshabilitado cuando Auto está activado. Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el deslizador manual de nitidez. Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre/cierra una conexión TCP directa con el TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que está rota en firmware 4.2. El TGXL controla PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita señalización del cliente. Si el campo IP está vacío y la radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón | Abre/cierra una conexión TCP directa con el Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre/cierra la conexión con el Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. La fila se oculta del estado Connected si un ShackSwitch (en lugar de un Antenna Genius estándar) es el dispositivo conectado. |
| Connect / Disconnect (ShackSwitch) | Botón | Abre/cierra la conexión con un conmutador de antena ShackSwitch a través del protocolo AG UDP/TCP en el puerto 9007. Guarda la IP en `SS_ManualIp` y el puerto en `SS_ControlPort`. ShackSwitch se detecta mediante el campo 'ShackSwitch' en el beacon de broadcast AG. La detección automática mediante UDP también funciona sin esta fila. La fila se oculta del estado Connected si Antenna Genius (no ShackSwitch) es el dispositivo conectado. |
| ⚙ Web UI (ShackSwitch) | Botón | Abre la interfaz de configuración web local del dispositivo ShackSwitch en el navegador del sistema. Utiliza el `webPort` del beacon si es mayor que 1024; de lo contrario, recurre a `SS_WebPort` o al puerto 5000. |
| Select Installer... | Botón | Abre un selector de archivos que acepta `.msi` (instalador WiX de FlexRadio v4.2+), `.exe` (instalador autoextraíble antiguo) o un archivo de firmware `.ssdr` preextraído. El gestor de firmware detecta automáticamente el formato a partir de los primeros 8 bytes (magia OLE/MSI vs MZ PE/COFF) y extrae el `.ssdr` sin herramientas externas. Cuando hay una actualización disponible, la etiqueta de estado le indica que descargue el instalador de SmartSDR desde flexradio.com y luego use este botón para prepararlo. La etiqueta cambió de **Browse .ssdr...** en v0.9.3. |
| APD (pestaña) | Pestaña | Configuración del muestreador de Predistorsión Adaptativa Externa — selección por antena TX del puerto de muestra de realimentación (INTERNAL / RX_A / RX_B / XVTA / XVTB) y un botón de reinicio del ecualizador. La pestaña está oculta a menos que la radio informe `apd configurable=1`. Solo las series FLEX-8x00 con firmware SmartSDR 4.2.18+ exponen esto; las series 6000 y radios anteriores a 4.2.18 mantienen la pestaña invisible. |
| Combos de muestreador ANT1 / ANT2 / XVTA / XVTB (APD) | Cuadro combinado | Selecciona la ruta de realimentación que la radio utiliza para muestrear la RF saliente para el entrenamiento APD para esa antena TX. Elija una entrada RX/XVTR externa cuando utilice un amplificador lineal externo. Las opciones se rellenan en vivo desde el subobjeto `apd sampler` de la radio. Recurre a INTERNAL si la radio informa un valor no reconocido. Predeterminado: INTERNAL. |
| Equalizer Reset (APD) | Botón | Envía `apd reset` a la radio, borrando todos los datos de entrenamiento APD por antena para que la adaptación comience de nuevo. |
| Themes (pestaña) | Pestaña | Pestaña de personalización de la interfaz de usuario — actualmente alberga la sección Slice Colors. |
| Use Aether defaults / Custom colors | Botón de opción | Cambia el esquema de color de las slices entre la paleta integrada de AetherSDR y un conjunto completamente personalizado por slice. |
| Botones de color Slice A–H | Botón | Haga clic en cualquier botón con letra (A–H) para abrir un selector de color y asignar un color personalizado para esa slice. Los cambios son visibles de inmediato en los widgets VFO, superposiciones del panadapter y distintivos de canal CAT. Los botones están deshabilitados cuando está seleccionado **Use Aether defaults**. Se admiten hasta 8 slices. |
| Reset All to Defaults (Themes) | Botón | Restablece todos los colores personalizados de las slices a la paleta integrada de AetherSDR. |

## Actualización de firmware (pestaña Radio)

Utilice los controles en la pestaña **Radio** para verificar y aplicar actualizaciones de firmware.

1. Haga clic en **Check for Update**. AetherSDR consulta el servidor de actualizaciones de FlexRadio.
   - Si el firmware está actualizado, la etiqueta de estado muestra la versión actual en verde.
   - Si hay una actualización disponible, la etiqueta de estado muestra el número de versión e indica que descargue el instalador de SmartSDR desde flexradio.com.
2. Descargue el instalador de SmartSDR desde flexradio.com (`.msi` para v4.2+, `.exe` para versiones anteriores).
3. Haga clic en **Select Installer...** y elija el instalador descargado o un archivo `.ssdr` preextraído. El gestor detecta automáticamente el formato del archivo y extrae el firmware sin herramientas externas. Aparece un indicador de progreso mientras se completa la preparación.
4. Haga clic en **Upload Firmware** para transferir el firmware preparado a la radio.

## Calibración de frecuencia (pestaña RX)

En v0.9.2.1, los controles de calibración en la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. La etiqueta de estado en la parte superior del grupo ahora dice:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Cómo funciona la calibración en v0.9.2.1

El botón **Start** ahora valida el campo de frecuencia de calibración antes de enviar cualquier comando, restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego activa el barrido PLL. Mientras el barrido se ejecuta, **Start** está deshabilitado y etiquetado como **Busy**. Una etiqueta de estado junto al botón muestra el texto de progreso. El botón y la etiqueta vuelven a su estado normal cuando el barrido se completa o falla.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Introduzca la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacía antes de hacer clic en Start. |
| **Start** | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Deshabilitado y etiquetado como **Busy** mientras un barrido está en progreso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de la calibración: Starting, texto de progreso o error. Se actualiza en vivo durante el barrido. |

## Fuente de referencia de 10 MHz (pestaña RX)

El cuadro combinado **10 MHz Reference Source:** en la pestaña **RX** selecciona qué oscilador utiliza la radio como referencia de frecuencia. A partir de v0.9.7, el cuadro combinado y la etiqueta de estado de bloqueo a su lado se comportan de manera diferente a versiones anteriores.

### Población del cuadro combinado

El cuadro combinado se rellena dinámicamente según lo que la radio informa en el momento en que se construye la pestaña. Los elementos aparecen de acuerdo con las siguientes reglas:

| Etiqueta del elemento | Cuándo se muestra |
|---|---|
| Auto | Siempre presente. |
| TCXO | Presente cuando la radio ha informado algún estado de oscilador, cuando la radio informa `tcxoPresent`, o cuando la configuración actual o activa es `tcxo`. |
| GPSDO | Presente cuando la radio informa `gpsdoPresent`, o cuando la configuración actual o activa es `gpsdo`. |
| External 10 MHz | Presente cuando la radio ha informado algún estado de oscilador, cuando la radio informa `extPresent`, o cuando la configuración actual o activa es `external`. |

El cuadro combinado selecciona el elemento que coincide con el `oscSetting` actual de la radio. Si ese valor no está en la lista, el cuadro combinado recurre a la selección actual y luego a **Auto**.

> En versiones anteriores a v0.9.7, el cuadro combinado mostraba solo los elementos correspondientes a las banderas de hardware presentes al abrir el diálogo, y el elemento **External** estaba etiquetado como **External** en lugar de **External 10 MHz**.

### Etiqueta de estado de bloqueo

La etiqueta a la derecha del cuadro combinado muestra el estado actual del oscilador y la condición de bloqueo. Se actualiza cuando la radio envía nuevo estado.

| Condición | Texto de la etiqueta | Color |
|---|---|---|
| Aún no se ha recibido estado | Waiting for oscillator status | Gris |
| La configuración es Auto, la radio ha seleccionado una fuente | Auto -> \<source\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración difiere del estado activo | \<setting\> -> \<active\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| La configuración coincide con el estado activo | \<source\> Locked / Unlocked | Verde (bloqueado) / Rojo (desbloqueado) |
| External seleccionado pero no se detecta señal externa | \<text\> (not detected) añadido | Verde (bloqueado) / Rojo (desbloqueado) |

La radio envía `ext` para la fuente externa en algunas respuestas de firmware. AetherSDR normaliza esto a `external` antes de mostrarlo, por lo que la etiqueta siempre muestra **External 10 MHz** en lugar de **Ext**.

## Consejos

- Cada transverter obtiene su propia pestaña anidada dentro de la pestaña XVTR. Si tiene múltiples transverters, use esas pestañas para cambiar entre entradas.
- Si necesita volver a este diálogo más tarde para ajustar un transverter, vuelva a abrir `Settings > Radio Setup...` y vaya directamente a la pestaña **XVTR**.
- En la pestaña **RX**, introduzca siempre una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):** antes de hacer clic en **Start**. Dejar el campo vacío cancela el barrido.
- Cuando **Check for Update** informe una nueva versión de firmware, descargue el instalador de SmartSDR desde flexradio.com antes de continuar.
