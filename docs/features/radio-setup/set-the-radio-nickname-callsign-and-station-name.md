# Establecer el apodo, indicativo y nombre de estación del radio

Establezca un apodo legible, su indicativo y un nombre de estación en el FLEX-8600 conectado. Estos valores identifican el radio y este cliente ante otras estaciones multiFLEX en la red.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los controles de la pestaña Radio (tab) no están disponibles sin una conexión activa.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Radio**.
3. En el grupo **Radio Identification**, localice el campo **Nickname**. Escriba el apodo que desea asignar al radio.
4. Presione Tab o haga clic fuera del campo para confirmar. AetherSDR envía el nuevo nombre al radio de inmediato.
5. En el campo **Callsign**, escriba el indicativo de su estación.
6. Presione Tab o haga clic fuera del campo para confirmar.
7. En el campo **Station Name**, escriba el nombre que identifica este cliente ante otras estaciones multiFLEX.
8. Presione Tab o haga clic fuera del campo para confirmar.
9. Haga clic en **Close** para cerrar el diálogo.

## Qué hace cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Nickname** | Etiqueta descriptiva para el radio. Se envía al radio como nombre del radio. | Nombre reportado por el radio |
| **Callsign** | Indicativo de su estación, almacenado en el radio. | _(en blanco)_ |
| **Station Name** | Identifica este cliente AetherSDR ante otras estaciones multiFLEX. | Nombre de host del sistema operativo |
| TX Follows Active Slice | TX sigue al slice (segmento de recepción) activo. Mutuamente excluyente con Active Slice Follows TX. | Se deshabilita automáticamente durante la operación Split. |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente excluyente con TX Follows Active Slice. | |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0 = menor latencia a 3 = mayor nitidez) por modo; el control se deshabilita cuando Auto está activado. | Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante manual de nitidez. | Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| Connect / Disconnect (TGXL) | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. Requerido para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de enclavamiento de hardware; no se requiere activación desde el cliente. Si el campo de IP está vacío y el radio ha detectado el TGXL, la IP detectada se completa automáticamente. | Connect |
| Connect / Disconnect (PGXL) | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| Connect / Disconnect (Antenna Genius) | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. | Connect |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia independientemente de si hay un GPSDO instalado.

- Si hay un GPSDO instalado, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." en verde.
- Si no hay un GPSDO instalado, la etiqueta de estado muestra "Manual frequency offset calibration available." en ámbar.

En ambos casos, el campo **Cal Frequency (MHz)** y el botón **Start** se muestran siempre.

### Para ejecutar una calibración de frecuencia

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia conocida en el campo **Cal Frequency (MHz)**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en progreso.
   - Una etiqueta de estado junto al botón muestra el estado actual (por ejemplo, "Starting…").
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido de calibración.
5. Espere a que la etiqueta de estado indique la finalización. El botón **Start** se vuelve a habilitar automáticamente.

### Comportamiento del campo Cal Frequency (MHz)

| Condición | Resultado |
|---|---|
| El campo está vacío al hacer clic en Start | La etiqueta de estado muestra "Enter cal frequency" en ámbar; la calibración no se inicia. |
| Se ingresa una frecuencia válida | AetherSDR envía `radio set cal_freq=<value>`, restablece el error de frecuencia a 0 ppb y luego inicia el barrido de calibración PLL. |

### Controles de la pestaña RX

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Cal Frequency (MHz)** | Frecuencia de referencia utilizada para la calibración manual. Siempre visible desde la versión v0.9.2.1 en adelante, independientemente de la presencia del GPSDO. | — |
| **Start** | Inicia el barrido de calibración de frecuencia. Se deshabilita y se etiqueta como **Busy** mientras se ejecuta una calibración. | — |
| **Freq Offset (ppb)** | Desplazamiento de frecuencia manual en partes por billón. | — |
| **10 MHz Reference Source** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de bloqueo (Locked / Unlocked) se actualiza en tiempo real junto al selector. | Auto |

## Consejos

- Si el campo **Nickname** se deja en blanco, AetherSDR lo completa automáticamente con el nombre reportado por el radio en la red.
- **Station Name** usa por defecto el nombre de host del sistema operativo cuando no se ha guardado ningún valor. Para restaurar el valor predeterminado, borre el campo y presione Tab; luego vuelva a ingresar el nombre de host manualmente si es necesario.
- Los cambios en **Nickname** y **Callsign** se envían al radio en el momento en que abandona cada campo. No se requiere un paso adicional de guardado o aplicación.
- **Station Name** se guarda localmente en la configuración de AetherSDR y también se envía al radio como identificador de estación cliente para multiFLEX.
- Antes de la versión v0.9.2.1, el campo **Cal Frequency** y el botón **Start** estaban ocultos cuando había un GPSDO instalado. Ahora están siempre disponibles.

## Relacionados

- [Verificar el número de serie, versión de hardware, región y opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Descripción general de Radio Setup](overview.md)
