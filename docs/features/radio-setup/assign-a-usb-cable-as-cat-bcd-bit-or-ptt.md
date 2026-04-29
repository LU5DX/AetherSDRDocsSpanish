# Asignar un cable USB como CAT, BCD, bit o PTT

Use esta página para configurar los adaptadores seriales USB conectados a su FLEX-8600 y asignar a cada uno una función: control CAT, datos de banda BCD, salida de bit individual o PTT, junto con sus parámetros seriales y opciones de comportamiento.

## Antes de comenzar

- Conecte los adaptadores seriales USB a la computadora que ejecuta AetherSDR antes de abrir el diálogo.
- AetherSDR debe estar conectado a la radio. La pestaña USB Cables no está disponible sin una conexión activa a la radio.

## Pasos

1. Abra `Settings > USB Cables...`. Esto abre el diálogo Radio Setup directamente en la pestaña USB Cables. Como alternativa, abra `Settings > Radio Setup...` y haga clic en la pestaña **USB Cables**.
2. Localice la lista de cables en el lado izquierdo de la pestaña. Cada cable USB detectado aparece con su nombre y un indicador de estado **Plugged** o **Unplugged**.
3. Seleccione el cable que desea configurar haciendo clic en él en la lista.
4. Establezca el tipo de cable usando el campo **Name:** y el selector de tipo asociado. Elija entre CAT, BCD, bit o PTT según la función que deba cumplir ese cable.
5. Active **Enabled** para habilitar el cable. El cable no funcionará hasta que esté habilitado.
6. Configure los parámetros seriales del cable:
   - **Speed** — velocidad en baudios para la conexión serial.
   - **Data Bits** — número de bits de datos.
   - **Parity** — configuración de paridad.
   - **Stop Bits** — número de bits de parada.
   - **Flow** — método de control de flujo.
7. Configure las opciones de comportamiento relevantes para el tipo de cable:
   - **Source** — selecciona qué impulsa la salida del cable.
   - **Auto Report** — controla si los cambios de estado se reportan automáticamente.
   - **BCD Type** — selecciona el formato de codificación BCD (solo para cables BCD).
   - **Polarity** — establece la lógica activa-alta o activa-baja.
   - **Bit Configuration (0–7)** — asigna funciones a los bits de salida individuales (solo para cables tipo bit).
8. Repita los pasos 3–7 para cualquier cable adicional.
9. Haga clic en **Close** para cerrar el diálogo. Los ajustes tienen efecto inmediatamente cuando se habilita cada cable; no se requiere un paso separado de Apply.

## Qué hace cada control

| Control | Descripción | Notas |
|---|---|---|
| **Cables list / Status** | Lista todos los adaptadores seriales USB detectados con estado **Plugged** o **Unplugged**. Seleccione un cable aquí para editar su configuración. | |
| **Name:** | Etiqueta visible por el usuario para el cable. | |
| **Enabled** | Activa el cable. El cable está inactivo hasta que se habilita. | |
| **Speed** | Velocidad en baudios del puerto serial. | |
| **Data Bits** | Número de bits de datos seriales. | |
| **Parity** | Paridad serial: None, Even, Odd, etc. | |
| **Stop Bits** | Número de bits de parada. | |
| **Flow** | Método de control de flujo (None, Hardware, Software). | |
| **Source** | Selecciona la fuente de señal de la radio que impulsa la salida del cable. | |
| **Auto Report** | Cuando está activo, la radio reporta los cambios de estado al cable automáticamente. | |
| **BCD Type** | Selecciona el formato de codificación de datos de banda BCD. Aplica solo a cables de tipo BCD. | |
| **Polarity** | Establece si la lógica de salida es activa-alta o activa-baja. | |
| **Bit Configuration (0–7)** | Asigna pines de salida individuales a funciones específicas. Aplica solo a cables de tipo bit. | |
| **TX Follows Active Slice** | TX sigue al slice (canal de recepción) activo. Mutuamente excluyente con **Active Slice Follows TX**. | Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=menor latencia a 3=máxima nitidez) por modo; el control deslizante se deshabilita cuando Auto está activo. | Comandos enviados como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | Comandos enviados como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. | Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que no funciona en firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y la radio ha detectado el TGXL, la IP detectada se completa automáticamente. |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. | |

## Pestaña RX — calibración de frecuencia (v0.9.2.1)

La pestaña **RX** ahora muestra los controles de calibración de frecuencia independientemente de si hay un GPSDO instalado. En versiones anteriores, los campos de calibración se ocultaban cuando se detectaba un GPSDO.

- Si hay un GPSDO instalado, una línea de estado verde indica "GPSDO installed. Manual frequency offset calibration available."
- Si no hay GPSDO instalado, una línea de estado amarilla indica "Manual frequency offset calibration available."

En ambos casos, los controles **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** son siempre visibles.

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...` y haga clic en la pestaña **RX**.
2. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón cambia a **Busy** y se deshabilita mientras la calibración está en curso. Una etiqueta de estado a la derecha del botón muestra el texto de progreso.
   - "Starting…" aparece de inmediato.
   - La radio recibe `radio set cal_freq=<value>` seguido de `radio set freq_error_ppb=0`, luego `radio pll_start` para iniciar el barrido.
   - Si deja el campo **Cal Frequency (MHz):** vacío y hace clic en **Start**, la etiqueta de estado muestra "Enter cal frequency" en ámbar y la calibración no comienza.
4. Espere a que la etiqueta de estado indique la finalización. El botón **Start** se vuelve a habilitar automáticamente.
5. Confirme o ajuste el resultado usando **Freq Offset (ppb):**.

### Controles de la pestaña RX

| Control | Descripción | Notas |
|---|---|---|
| **Cal Frequency (MHz):** | Frecuencia utilizada para la calibración, ingresada en MHz con seis decimales. | Se envía a la radio como `radio set cal_freq=<value>`. |
| **Start** | Inicia el barrido de calibración. Se deshabilita y se etiqueta como **Busy** mientras hay una calibración en curso. | Restablece `freq_error_ppb` a 0 antes de comenzar. Requiere una frecuencia de calibración no vacía. |
| **Freq Offset (ppb):** | Corrección manual del desplazamiento de frecuencia en partes por mil millones. | |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones disponibles dependen del hardware instalado. | El estado de bloqueo (Locked / Unlocked) se muestra junto al selector y se actualiza en tiempo real. |

## Consejos

- Si un cable muestra **Unplugged**, verifique la conexión USB física y vuelva a abrir el diálogo. La lista refleja el estado en el momento en que se cargó la pestaña.
- Asigne solo un cable PTT a la vez si desea un comportamiento de activación de transmisión predecible.
- Los cables BCD y bit comparten muchos de los mismos parámetros seriales; configure **Speed**, **Data Bits**, **Parity**, **Stop Bits** y **Flow** para que coincidan con los requisitos del dispositivo externo que recibe los datos.
- Al realizar la calibración de frecuencia, asegúrese de que la señal de referencia sea estable y esté exactamente en la frecuencia ingresada antes de hacer clic en **Start**. Hacer clic en **Start** con una referencia inestable o ausente producirá una corrección de desplazamiento inexacta.

## Solución de problemas

- **El cable muestra Unplugged aunque está conectado** — Es posible que el adaptador USB no estuviera presente cuando se cargó la pestaña. Cierre Radio Setup, asegúrese de que el adaptador sea reconocido por el sistema operativo y vuelva a abrir `Settings > USB Cables...`.
- **El interruptor Enabled no tiene efecto** — Confirme que la radio esté conectada. La pestaña USB Cables requiere una conexión activa a la radio; los controles no envían comandos sin ella.
- **Las salidas BCD o bit están invertidas** — Verifique la configuración de **Polarity** del cable y cámbiela para que coincida con los niveles lógicos de su dispositivo externo.
- **El botón Start permanece deshabilitado después de la calibración** — Si la conexión con la radio se interrumpe durante un barrido de calibración, el botón puede permanecer en estado Busy. Cierre y vuelva a abrir Radio Setup para restablecer el diálogo.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serial de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
