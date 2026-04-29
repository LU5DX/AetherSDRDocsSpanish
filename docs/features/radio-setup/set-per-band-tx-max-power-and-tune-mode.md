# Configurar la potencia TX máxima por banda y el modo de sintonía

Use esta página para limitar la potencia de transmisión por banda y elegir el comportamiento de la función Tune. Estos ajustes se almacenan en el radio y se aplican independientemente del cliente que se conecte.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña TX no es accesible sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **TX**.
3. Haga clic en **TX Band Settings** para abrir el diálogo dedicado de potencia y sintonía por banda.
4. En la tabla por banda, localice la banda que desea configurar.
5. Ajuste el límite de potencia para esa banda según sea necesario. El rango válido para **Max Power:** es 0–100 %.
6. Para cambiar el comportamiento de sintonía, seleccione la opción deseada en el cuadro combinado **Tune Mode:**.
7. Cierre el diálogo cuando termine. Los ajustes se aplican inmediatamente al radio.

## Qué hace cada control

| Control                                               | Tipo              | Rango válido / opciones                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TX Band Settings**                                  | Botón             | —                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **Max Power:**                                        | Cuadro numérico   | 0–100 %                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **Tune Mode:**                                        | Cuadro combinado  | Ver opciones del firmware del radio                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **Show TX in Waterfall:**                             | Botón de activación | Habilitado / Deshabilitado                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| **TX Follows Active Slice / Active Slice Follows TX** | Par de botones    | Mutuamente excluyentes                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| TX Follows Active Slice                               | Botón             | TX sigue al slice (receptor) activo. Mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split.                                                                                                                                                                                                                                                                                                              |
| Active Slice Follows TX                               | Botón             | Cambia el slice activo cuando TX se desplaza externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice.                                                                                                                                                                                                                                                                                                                       |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | 0–3. Establece la nitidez del filtro (0 = menor latencia, 3 = máxima nitidez) por modo. El control se deshabilita cuando Auto está activo. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`.                                                                                                                                                                                                                                               |
| Auto (Voice / CW / Digital)                           | Botón de activación | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`.                                                                                                                                                                                                                                                              |
| Connect / Disconnect (TGXL)                           | Botón             | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del radio interrumpida en el firmware 4.2. Si el campo IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se rellena automáticamente. |
| Connect / Disconnect (PGXL)                           | Botón             | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`.                                                                                                                                                                                                                                                                                                          |
| Connect / Disconnect (Antenna Genius)                 | Botón             | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`.                                                                                                                                                                                                                                                                                                                            |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** contiene controles para la calibración manual del desplazamiento de frecuencia y la selección de la fuente de referencia de 10 MHz. En la versión v0.9.2.1, los controles de calibración se muestran siempre, independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado indica "GPSDO installed. Manual frequency offset calibration available." (verde). Cuando no hay GPSDO, la etiqueta indica "Manual frequency offset calibration available." (ámbar).

### Cómo ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras se ejecuta la calibración.
   - El campo de estado a la derecha del botón muestra el texto de progreso ("Starting…" y luego el estado en tiempo real).
   - Antes de iniciar, AetherSDR restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`.
   - Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, el campo de estado muestra "Enter cal frequency" y la calibración no continúa.
5. Cuando la calibración finaliza, el botón se vuelve a habilitar y el campo de estado muestra el resultado.
6. Si necesita establecer un desplazamiento manualmente, introduzca un valor en **Freq Offset (ppb):**.

### Controles de calibración

| Control                      | Tipo              | Notas                                                                                                              |
|------------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------|
| **Cal Frequency (MHz):**     | Cuadro numérico   | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en **Start**.                    |
| **Start**                    | Botón             | Inicia la calibración. Restablece `freq_error_ppb` a 0 y luego emite `radio pll_start`. Deshabilitado mientras está ocupado. |
| **Freq Offset (ppb):**       | Cuadro numérico   | Desplazamiento de frecuencia manual en partes por mil millones.                                                    |
| **10 MHz Reference Source:** | Cuadro combinado  | Auto / TCXO / GPSDO / External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo se actualiza en tiempo real. |

## Consejos

- **TX Band Settings** también es accesible directamente desde `Settings > TX Band Settings...` sin necesidad de abrir Radio Setup primero.
- El cuadro numérico **Max Power:** en la pestaña TX establece un límite a nivel de radio. Los límites por banda configurados dentro de **TX Band Settings** operan sobre este límite.
- Al ejecutar la calibración de frecuencia, asegúrese de que ninguna otra estación esté transmitiendo en la frecuencia de referencia antes de hacer clic en **Start**.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
