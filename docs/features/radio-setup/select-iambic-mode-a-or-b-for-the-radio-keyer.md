# Seleccionar el modo iámbico A o B para el manipulador del radio

Elija entre el modo iámbico Curtis A y el modo Curtis B para el manipulador integrado del FLEX-8600. La configuración se aplica tanto al manipulador de hardware del radio como al manipulador de software local de AetherSDR, que refleja el estado del radio para proporcionar sidetone de baja latencia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Phone/CW no está disponible cuando no hay ningún radio conectado.
- Debe haber una paleta (paddle) conectada al jack de llave del radio para que el manipulador iámbico funcione.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el cuadro de diálogo Radio Setup.
2. Haga clic en la pestaña **Phone/CW**.
3. Confirme que **Iambic:** esté configurado en **Enabled**. Si aparece **Disabled**, haga clic una vez para activar el manipulador iámbico.
4. Haga clic en **A** o **B** para seleccionar el modo iámbico Curtis deseado.

## Función de cada control

| Control | Tipo | Valor predeterminado |
|---|---|---|
| **Iambic:** | Botón de alternancia | — |
| **Iambic Mode: A / B** | Botón de acción (par mutuamente exclusivo) | A |
| **Swap:** | Botón de alternancia | — |
| TX Follows Active Slice | TX sigue el slice activo. Mutuamente exclusivo con 'Active Slice Follows TX'. | Se desactiva automáticamente durante la operación en Split. |
| Active Slice Follows TX | Cambia el slice activo cuando el TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con 'TX Follows Active Slice'. | |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0 = menor latencia a 3 = máxima nitidez) por modo; el control se desactiva cuando Auto está habilitado. | Comandos enviados como 'radio filter_sharpness \<mode> level=\<N>'. |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; desactiva el control deslizante manual de nitidez. | Comandos enviados como 'radio filter_sharpness \<mode> auto_level=1'. |
| Connect / Disconnect (TGXL) | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en TGXL_ManualIp y TGXL_ManualPort al conectar, de modo que AetherSDR se reconecte automáticamente al iniciar. | Necesario para recuperar TUNE en el firmware 4.2 o posterior. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL (TgxlConnection::requestAutotune()) en lugar de utilizar la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en el firmware 4.2. El TGXL controla el PTT del radio mediante su cable de interbloqueo de hardware; no se requiere manipulación desde el cliente. Si el campo IP está vacío y el radio ha detectado el TGXL, la IP detectada se rellena automáticamente. |
| Connect / Disconnect (PGXL) | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en PGXL_ManualIp y PGXL_ManualPort. | |
| Connect / Disconnect (Antenna Genius) | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en AG_ManualIp y AG_ManualPort. | |

## Calibración de frecuencia (pestaña RX)

En la versión v0.9.2.1, los controles de calibración de frecuencia de la pestaña RX están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** se ocultaban cuando se detectaba un GPSDO. La etiqueta de estado en la parte superior del grupo ahora muestra:

- **GPSDO installed. Manual frequency offset calibration available.** (verde) — GPSDO presente.
- **Manual frequency offset calibration available.** (ámbar) — sin GPSDO.

### Uso de la calibración de frecuencia

1. Haga clic en `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Ingrese una frecuencia de referencia de precisión conocida en **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en curso.
   - Una etiqueta de estado junto al botón informa el progreso (Starting… y los estados siguientes).
   - AetherSDR restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) antes de iniciar el barrido.
5. Cuando la calibración finaliza, el botón se vuelve a habilitar y la etiqueta de estado se actualiza con el resultado.
6. Si el campo **Cal Frequency (MHz):** está vacío cuando hace clic en **Start**, la etiqueta de estado muestra **Enter cal frequency** y la calibración no comienza.

### Controles de calibración

| Control | Tipo | Valor predeterminado | Comportamiento |
|---|---|---|---|
| **Cal Frequency (MHz):** | Spinbox | — | Frecuencia utilizada para la calibración. No debe estar vacío antes de hacer clic en Start. |
| **Start** | Botón | — | Restablece el error de frecuencia a 0 ppb y luego inicia el barrido de calibración. Se deshabilita y muestra la etiqueta Busy durante una calibración activa. |
| **Freq Offset (ppb):** | Spinbox | — | Desplazamiento de frecuencia manual en partes por mil millones. Se aplica directamente sin ejecutar un barrido. |

## Consejos

- El modo A (Curtis A) libera el último elemento cuando ambas paletas se sueltan en medio de una pulsación continua. El modo B (Curtis B) completa el último elemento antes de detenerse. Elija según su estilo de transmisión.
- El manipulador de software local refleja el modo que seleccione aquí, proporcionando una respuesta de sidetone inferior a 5 ms independiente de la latencia de red.
- Cuando hay un GPSDO instalado, la corrección de error de frecuencia que proporciona el GPSDO es independiente de los controles de calibración manual. Aun así, puede utilizar la calibración manual para verificar o ajustar el desplazamiento.

## Relacionados

- [Descripción general de Radio Setup](overview.md)
- [Configurar las funciones de los pines del puerto serie de FlexControl](configure-flexcontrol-serial-port-pin-functions.md)
