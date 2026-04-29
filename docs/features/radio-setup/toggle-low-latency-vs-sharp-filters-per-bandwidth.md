# Alternar filtros de baja latencia o filtros precisos por ancho de banda

La pestaña **Filters** en Radio Setup permite elegir entre filtros DSP de baja latencia y filtros precisos para cada ancho de banda de recepción, y opcionalmente forzar el uso de filtros de baja latencia al utilizar modos digitales.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña **Filters** solo está disponible cuando hay una conexión de radio activa.
- Abra Radio Setup mediante `Settings > Radio Setup...`.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Filters**.
3. Haga clic en el botón de alternancia **Low Latency / Sharp Filters** para cambiar entre las dos familias de filtros para el ancho de banda actual. El botón refleja la selección activa.
4. Para forzar el uso de filtros de baja latencia siempre que un modo digital (DIGU o DIGL) esté activo, active la casilla **Use Low Latency Filters for Digital Modes**.
5. Cierre el cuadro de diálogo. Los ajustes tienen efecto de inmediato.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Low Latency / Sharp Filters** | Botón de alternancia | Cambia la preferencia de familia de filtros entre baja latencia y filtros precisos para el ancho de banda seleccionado. |
| **Use Low Latency Filters for Digital Modes** | Casilla de verificación | Cuando está activada, anula la elección de filtro por ancho de banda y utiliza filtros de baja latencia siempre que un slice DIGU o DIGL esté activo. |
| Controles deslizantes de precisión de filtro de voz / CW / digital | Control deslizante | Establece la precisión del filtro (0=latencia mínima hasta 3=máxima precisión) por modo. El control se desactiva cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (voz / CW / digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo y desactiva el control deslizante de precisión manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| TX Follows Active Slice | Botón de acción | TX sigue el slice activo. Mutuamente excluyente con Active Slice Follows TX. Se desactiva automáticamente durante la operación en Split. |
| Active Slice Follows TX | Botón de acción | Cambia el slice activo cuando TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. |
| Connect / Disconnect (TGXL) | Botón de acción | Abre o cierra una conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo de hardware; no se requiere manipulación desde el cliente. Si el campo de IP está vacío y el radio ha detectado el TGXL, la IP detectada se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Botón de acción | Abre o cierra una conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón de acción | Abre o cierra una conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

## Calibración de frecuencia (pestaña RX)

En la versión 0.9.2.1, los controles de calibración de frecuencia en la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles Cal Frequency y Start estaban ocultos cuando se detectaba un GPSDO.

- Cuando hay un GPSDO instalado, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." en verde.
- Cuando no hay un GPSDO instalado, la etiqueta de estado muestra "Manual frequency offset calibration available." en ámbar.

### Procedimiento de calibración

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia de precisión conocida en **Cal Frequency (MHz)**.
4. Haga clic en **Start**. AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`), establece la frecuencia de calibración e inicia el barrido de calibración PLL. El campo de estado junto al botón Start se actualiza a medida que avanza la calibración.
5. Mientras la calibración está en curso, el botón **Start** se deshabilita y muestra "Busy". Se vuelve a habilitar cuando la calibración finaliza o falla.
6. Ajuste **Freq Offset (ppb)** manualmente si es necesario una vez que la calibración haya concluido.

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz)** | Spinbox | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Botón de acción | Restablece el error de frecuencia a 0 ppb, aplica la frecuencia de calibración e inicia el barrido de calibración PLL. Se deshabilita y muestra "Busy" mientras hay una calibración en curso. |
| **Freq Offset (ppb)** | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source** | Cuadro combinado | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se muestra junto al cuadro combinado y se actualiza en tiempo real. |

## Consejos

- Los filtros de baja latencia reducen el retardo de procesamiento, lo que beneficia la decodificación de modos digitales en tiempo real y el CW. Los filtros precisos proporcionan una mayor selectividad de falda, lo que resulta más útil en condiciones de banda congestionada en SSB.
- La casilla **Use Low Latency Filters for Digital Modes** se aplica a todos los anchos de banda, por lo que no es necesario cambiar el ajuste por ancho de banda cada vez que se cambia a un modo digital.
- Si **Start** no se activa después de ingresar una frecuencia de calibración, verifique que el campo Cal Frequency no esté vacío.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Seleccionar el modo iámbico A o B para el manipulador del radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)
