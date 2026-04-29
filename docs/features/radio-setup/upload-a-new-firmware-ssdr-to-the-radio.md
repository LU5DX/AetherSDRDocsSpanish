# Cargar un nuevo firmware .ssdr en el radio

Esta página explica cómo cargar un archivo de imagen de firmware en su FLEX-8600 mediante el diálogo Radio Setup. Realice este procedimiento para actualizar el radio a una versión de firmware específica sin utilizar la verificación de actualizaciones automática.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Radio (tab) no se completará correctamente sin una conexión activa.
- Obtenga el archivo de firmware `.ssdr` de FlexRadio y anote la ubicación donde está guardado en su computadora.
- No transmita durante la carga.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. Haga clic en **Browse .ssdr...** para abrir un selector de archivos.
4. Navegue hasta el archivo `.ssdr` en su computadora, selecciónelo y confirme.
5. Haga clic en **Upload Firmware**.
6. Observe la barra de progreso y el texto de estado que aparecen debajo del botón. Espere hasta que el estado indique que la carga se ha completado antes de realizar cualquier otra acción.
7. Reinicie el radio según las instrucciones de las notas de versión del firmware para aplicar el nuevo firmware.

## Función de cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Check for Update** | Botón | Consulta las actualizaciones de firmware disponibles de forma automática. Use este control en lugar de **Browse .ssdr...** si desea que AetherSDR encuentre la actualización por usted. |
| **Browse .ssdr...** | Botón | Abre un diálogo de archivos para seleccionar una imagen de firmware `.ssdr` local. |
| **Upload Firmware** | Botón | Inicia la carga utilizando el archivo seleccionado con **Browse .ssdr...**. Debajo aparecen una barra de progreso y un texto de estado que se actualizan durante la transferencia. |
| TX Follows Active Slice | El transmisor sigue al slice activo. Mutuamente exclusivo con 'Active Slice Follows TX'. | Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Cambia el slice activo cuando el transmisor se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente exclusivo con 'TX Follows Active Slice'. | |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0 = menor latencia, 3 = mayor nitidez) por modo; el control deslizante se deshabilita cuando Auto está activado. | Comandos enviados como 'radio filter_sharpness <mode> level=<N>'. |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | Comandos enviados como 'radio filter_sharpness <mode> auto_level=1'. |
| Connect / Disconnect (TGXL) | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en TGXL_ManualIp y TGXL_ManualPort al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. | Necesario para recuperar TUNE en firmware 4.2 o superior. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL (TgxlConnection::requestAutotune()) en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en firmware 4.2. El TGXL controla el PTT del radio mediante su cable de enclavamiento de hardware; no se requiere activación del PTT desde el cliente. Si el campo de IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. |
| Connect / Disconnect (PGXL) | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en PGXL_ManualIp y PGXL_ManualPort. | |
| Connect / Disconnect (Antenna Genius) | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en AG_ManualIp y AG_ManualPort. | |

## Calibración de frecuencia (pestaña RX)

La pestaña RX muestra los controles de calibración independientemente de si hay un GPSDO instalado. La etiqueta de estado en la parte superior de la pestaña cambia su texto y color según el hardware presente:

- **GPSDO instalado** — la etiqueta muestra "GPSDO installed. Manual frequency offset calibration available." en verde. Si lo necesita, puede ejecutar una calibración manual de todas formas.
- **Sin GPSDO** — la etiqueta muestra "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** están siempre visibles y activos. Antes de la versión v0.9.2.1, los controles de calibración se ocultaban cuando se detectaba un GPSDO.

### Uso del botón Start

El botón **Start** ahora proporciona información de estado directamente en la pestaña RX, en lugar de depender únicamente de la respuesta del radio. Al hacer clic en **Start**:

1. AetherSDR verifica que el campo **Cal Frequency (MHz)** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no continúa.
2. El texto del botón cambia a **Busy** y el botón se deshabilita hasta que la secuencia de comandos de calibración se complete.
3. AetherSDR envía `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0` para restablecer cualquier desplazamiento previo, y luego emite `radio pll_start` para iniciar el barrido de calibración.
4. La etiqueta de estado en línea junto al botón se actualiza a medida que avanza la calibración.
5. Cuando la secuencia finaliza (o falla), el botón se vuelve a habilitar y regresa a **Start**.

La actividad de calibración se registra en el registro de protocolo a nivel de depuración, incluyendo el valor de la frecuencia de calibración, el restablecimiento de ppb y un identificador de ejecución interno que ayuda a correlacionar las entradas del registro cuando se realizan varios intentos de calibración en la misma sesión.

### Controles de frecuencia de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Campo | Ingrese la frecuencia de referencia conocida en MHz (seis decimales). Se envía como `radio set cal_freq=<value>` al salir del campo o al hacer clic en **Start**. |
| **Start** | Botón | Restablece el error de frecuencia a 0 ppb y luego inicia el barrido de calibración. Se deshabilita y muestra la etiqueta **Busy** mientras se ejecuta un barrido. |
| **Freq Offset (ppb)** | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones. Ajuste después de la calibración si se requiere un ajuste fino. |

## Consejos

- Si solo desea verificar si existe una versión más reciente, en lugar de cargar un archivo específico, use **Check for Update** en vez del flujo de trabajo manual de selección y carga.
- El área de estado del firmware está vacía hasta que comienza una carga. Si no ve la barra de progreso después de hacer clic en **Upload Firmware**, confirme que se haya seleccionado un archivo con **Browse .ssdr...** primero.
- Si **Start** muestra "Enter cal frequency" en ámbar, escriba un valor de frecuencia en el campo **Cal Frequency (MHz)** antes de volver a hacer clic en **Start**.
- Incluso con un GPSDO instalado, puede ejecutar una calibración manual si necesita verificar o anular la corrección automática.

## Solución de problemas

- **Upload Firmware no hace nada** — No se ha seleccionado ningún archivo `.ssdr`. Haga clic primero en **Browse .ssdr...**, seleccione el archivo y luego haga clic en **Upload Firmware**.
- **Los controles de la pestaña Radio no están completos o están deshabilitados** — AetherSDR no está conectado al radio. Establezca una conexión mediante `Settings > Connect to Radio...` antes de abrir Radio Setup.
- **El botón Start permanece con la etiqueta Busy** — El radio no respondió al comando `radio pll_start`. Revise el registro de protocolo para encontrar el identificador de ejecución correspondiente, verifique que el radio esté conectado y que no esté transmitiendo, y vuelva a intentarlo.

## Relacionados

- [Verificar el número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
