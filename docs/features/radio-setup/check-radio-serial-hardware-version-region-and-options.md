# Verificar el número de serie, versión de hardware, región y opciones del radio

La pestaña **Radio** en Radio Setup muestra información de identificación reportada directamente por el radio: número de serie, versión de hardware, región regulatoria y opciones licenciadas. Use esta página para verificar qué hardware y opciones tiene su radio antes de realizar diagnósticos o contactar al soporte técnico.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los campos de la pestaña **Radio** se completan con datos en vivo del radio.

## Pasos

1. Haga clic en `Settings > Radio Setup...`.
2. El diálogo se abre en la pestaña **Radio** de forma predeterminada.
3. Lea los valores en el grupo **Radio Information**:
   - **Radio SN** — el número de serie del chasis.
   - **HW Version** — la cadena de versión de hardware reportada por el radio.
   - **Region** — la región regulatoria del radio (muestra `USA` de forma predeterminada si el radio no reporta ninguna).
   - **Options** — las opciones licenciadas activas en este radio (por ejemplo, `GPS`, `PGXL`).

## Qué hace cada control

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Radio SN | Indicador (solo lectura) | Número de serie del chasis según lo reporta el radio. |
| HW Version | Indicador (solo lectura) | Cadena de versión de hardware con prefijo `v`. |
| Region | Indicador (solo lectura) | Región regulatoria. Muestra `USA` si el radio no reporta ninguna. |
| Options | Indicador (solo lectura) | Opciones licenciadas del radio. |
| TX Follows Active Slice | Botón | La transmisión sigue al slice activo. Es mutuamente excluyente con Active Slice Follows TX. Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Botón | Cambia el slice activo cuando la transmisión se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente excluyente con TX Follows Active Slice. |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Control deslizante | Establece la nitidez del filtro (0 = menor latencia hasta 3 = máxima nitidez) por modo; el control se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Botón de alternancia | Activa la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Botón | Abre o cierra la conexión TCP directa con el TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Es necesario para recuperar TUNE en el firmware 4.2 o posterior. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de utilizar la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona correctamente en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y el radio ya ha detectado el TGXL, la IP detectada se completa automáticamente. |
| Connect / Disconnect (PGXL) | Botón | Abre o cierra la conexión TCP directa con el Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| Connect / Disconnect (Antenna Genius) | Botón | Abre o cierra la conexión con el Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

Los cuatro campos de Radio Information son de solo lectura. No tienen asociada ninguna clave de configuración persistente.

## Pestaña RX — calibración de frecuencia

En la versión v0.9.2.1, los controles de calibración en la pestaña **RX** siempre son visibles, independientemente de si hay un GPSDO instalado. Anteriormente, los campos Cal Frequency, Start y Freq Offset quedaban ocultos cuando se detectaba un GPSDO. El banner de estado en la parte superior del grupo ahora muestra:

- **GPSDO instalado** — "GPSDO installed. Manual frequency offset calibration available." (texto verde)
- **Sin GPSDO** — "Manual frequency offset calibration available." (texto ámbar)

Los siguientes controles están disponibles ahora en ambas configuraciones:

| Etiqueta | Tipo | Comportamiento |
|---|---|---|
| Cal Frequency (MHz): | Cuadro de giro | Frecuencia utilizada para la calibración. Ingrese la frecuencia de referencia conocida antes de hacer clic en Start. |
| Start | Botón | Inicia la secuencia de calibración de frecuencia. El botón se deshabilita y su etiqueta cambia a **Busy** mientras la calibración está en curso. Antes de activar el barrido PLL, AetherSDR restablece el error de frecuencia del radio a cero (`radio set freq_error_ppb=0`) y luego emite `radio pll_start`. Si el campo Cal Frequency está vacío, el botón muestra una advertencia y no realiza ninguna acción. |
| Freq Offset (ppb): | Cuadro de giro | Desplazamiento de frecuencia manual en partes por mil millones (ppb), aplicado después de que la calibración finaliza o configurado directamente para corrección manual. |

Una etiqueta de estado aparece a la derecha del botón Start y se actualiza durante toda la secuencia de calibración:

| Estado | Texto | Color |
|---|---|---|
| Inactivo | *(vacío)* | — |
| Frecuencia de calibración no ingresada | "Enter cal frequency" | Ámbar |
| Secuencia iniciada | "Starting…" | Azul grisáceo |
| En progreso | Se actualiza según el estado PLL reportado por el radio | Azul grisáceo |

El botón Start se vuelve a habilitar y su etiqueta regresa a **Start** cuando la secuencia de calibración finaliza o falla.

## Consejos

- Si **Radio SN** aparece en blanco, el radio aún no ha enviado su número de serie del chasis. Desconéctese y vuelva a conectarse al radio.
- **Options** refleja lo que el radio reporta directamente. Si ha adquirido recientemente una actualización de licencia, apague y encienda el radio y vuelva a conectarse para que obtenga las opciones actualizadas.
- Al ejecutar la calibración, asegúrese de que la señal de referencia esté presente en la entrada de antena y de que **Cal Frequency (MHz)** coincida exactamente con la frecuencia del transmisor de referencia antes de hacer clic en **Start**.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar el apodo, indicativo y nombre de estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Cargar un nuevo firmware .ssdr al radio](upload-a-new-firmware-ssdr-to-the-radio.md)
