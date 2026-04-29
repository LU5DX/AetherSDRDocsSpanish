# Crear una nueva entrada de transverter

Use esta página para agregar una definición de transverter a su FLEX-8600 de modo que AetherSDR conozca el desplazamiento de frecuencia IF-a-RF y los parámetros de operación para la banda de su transverter.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Conozca el rango de frecuencia IF que usa su transverter y el desplazamiento de frecuencia RF que desea mostrar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **XVTR**.
3. Haga clic en **Create New Transverter**.
4. Aparece una nueva pestaña anidada. Configure los campos de la nueva entrada en esa pestaña.
5. Para restringir la entrada solo a recepción, establezca **RX Only:** en el estado habilitado.
6. Para eliminar una entrada que ya no necesita, haga clic en **Remove** en la pestaña de esa entrada.
7. Cierre el cuadro de diálogo con **Close**.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Create New Transverter** | Botón | Agrega una nueva entrada de transverter y abre su pestaña de configuración. |
| **RX Only:** | Botón de alternancia | Fuerza el transverter solo a recepción, impidiendo la transmisión a través de él. |
| **Remove** | Botón | Elimina permanentemente la definición de transverter seleccionada. |
| TX Follows Active Slice | Botón | La TX sigue al slice (canal de recepción) activo. Mutuamente exclusivo con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia el slice activo cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0=menor latencia hasta 3=máxima nitidez) por modo; el control se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2 o superior. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado de la radio, que no funciona en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se requiere ninguna activación desde el cliente. Si el campo IP está vacío y la radio ha detectado el TGXL, la IP detectada se completa automáticamente. |
| Connect / Disconnect (PGXL) | Botón | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

## Calibración de frecuencia (pestaña RX)

En la versión v0.9.2.1, los controles de calibración de la pestaña **RX** están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** se ocultaban cuando se detectaba un GPSDO. La etiqueta de estado en la parte superior del grupo ahora muestra:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Cómo funciona la calibración en v0.9.2.1

El botón **Start** ahora valida el campo de frecuencia de calibración antes de enviar cualquier comando, restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) y luego inicia el barrido del PLL. Mientras el barrido está en curso, **Start** se deshabilita y se etiqueta como **Busy**. Una etiqueta de estado junto al botón muestra el texto de progreso. El botón y la etiqueta regresan a su estado normal cuando el barrido se completa o falla.

| Control | Comportamiento |
|---|---|
| **Cal Frequency (MHz):** | Ingrese la frecuencia de referencia en MHz utilizada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Valida el campo, restablece `freq_error_ppb` a 0 e inicia el barrido de calibración. Se deshabilita y se etiqueta como **Busy** mientras hay un barrido en curso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |
| Etiqueta de estado | Muestra el estado actual de calibración: inicio, texto de progreso o error. Se actualiza en tiempo real durante el barrido. |

## Sugerencias

- Cada transverter tiene su propia pestaña anidada dentro de la pestaña XVTR. Si tiene varios transverters, use esas pestañas para alternar entre entradas.
- Si necesita volver a este cuadro de diálogo más adelante para ajustar un transverter, vuelva a abrir `Settings > Radio Setup...` y vaya directamente a la pestaña **XVTR**.
- En la pestaña **RX**, ingrese siempre una frecuencia de referencia precisa y conocida en **Cal Frequency (MHz):** antes de hacer clic en **Start**. Dejar el campo vacío cancela el barrido.

## Relacionado

- [Descripción general de Radio Setup](overview.md)
- [Configurar la potencia TX máxima por banda y el modo de sintonización](set-per-band-tx-max-power-and-tune-mode.md)
