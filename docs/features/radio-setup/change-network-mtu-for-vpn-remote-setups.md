# Cambiar el MTU de red para configuraciones VPN/remotas

El ajuste de MTU de red controla el tamaño máximo de paquete que la radio envía por la red. Reducirlo evita la fragmentación cuando se conecta a través de una VPN u otro túnel que disminuye el MTU de ruta disponible.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network no es accesible cuando está desconectado.
- Conozca el MTU de su túnel VPN o ruta de red. Los MTU de VPN habituales son 1400–1450 bytes; una ruta Ethernet estándar es de 1500 bytes.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Network**.
3. Localice el control giratorio **Network MTU:**.
4. Establezca el valor para que coincida con el MTU de su ruta de red.
5. Haga clic en **Apply** para enviar el nuevo MTU a la radio.

## Qué hace cada control

| Control | Descripción | Valor predeterminado |
|---|---|---|
| **Network MTU:** | Tamaño de paquete de salida en bytes. Redúzcalo cuando opere a través de una VPN o cualquier enlace con MTU reducido. | — |
| **Apply** | Envía la configuración actual de la pestaña Network, incluido el valor de MTU, a la radio. | — |
| TX Follows Active Slice | TX sigue el slice (receptor parcial) activo. Mutuamente exclusivo con Active Slice Follows TX. Se desactiva automáticamente durante la operación Split. | — |
| Active Slice Follows TX | Cambia el slice activo cuando TX se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con TX Follows Active Slice. | — |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0=menor latencia a 3=máxima nitidez) por modo; el control deslizante se desactiva cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; desactiva el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| Connect / Disconnect (TGXL) | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio, que no funciona en el firmware 4.2. El TGXL controla el PTT de la radio a través de su cable de interbloqueo de hardware; no se necesita manipulación desde el cliente. Si el campo de IP está vacío y la radio ha detectado el TGXL, la IP detectada se completa automáticamente. | — |
| Connect / Disconnect (PGXL) | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| Connect / Disconnect (Antenna Genius) | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. | — |

## Calibración de frecuencia (pestaña RX)

En la versión v0.9.2.1, los controles de calibración de frecuencia de la pestaña RX están disponibles independientemente de si hay un GPSDO instalado. Anteriormente, los controles **Cal Frequency (MHz):**, **Start** y **Freq Offset (ppb):** se ocultaban cuando se detectaba un GPSDO. Ahora todos los campos de calibración se muestran siempre; una etiqueta de estado en la parte superior del grupo indica si hay un GPSDO presente (texto verde) o no (texto ámbar).

### Procedimiento de calibración

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **RX**.
3. Introduzca una frecuencia de referencia conocida y precisa en el campo **Cal Frequency (MHz):**.
4. Haga clic en **Start**.
   - La etiqueta del botón cambia a **Busy** y se desactiva mientras se ejecuta el barrido de calibración.
   - Una etiqueta de estado junto al botón se actualiza a medida que avanza el barrido.
   - La radio primero restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) y luego inicia la secuencia de calibración PLL.
5. Cuando la calibración finaliza, el botón se reactiva y la etiqueta de estado muestra el resultado.
6. Si prefiere establecer el desplazamiento manualmente, introduzca un valor directamente en **Freq Offset (ppb):** sin hacer clic en **Start**.

### Mensajes de estado de calibración

| Mensaje | Significado |
|---|---|
| Starting… | El comando de barrido ha sido enviado a la radio. |
| Busy | La calibración PLL está en progreso. |
| Enter cal frequency | El campo **Cal Frequency (MHz):** estaba vacío cuando se hizo clic en **Start**. Introduzca un valor e intente de nuevo. |

### Notas

- Hacer clic en **Start** con el campo **Cal Frequency (MHz):** vacío muestra una advertencia ámbar "Enter cal frequency" y no envía ningún comando.
- La secuencia de calibración registra la frecuencia de calibración y el ID de ejecución en el registro de protocolo de depuración (`lcProtocol`). Puede consultarlo en el visor de registros de AetherSDR si el registro de diagnóstico está habilitado.
- Si el diálogo Radio Setup se cierra mientras hay una calibración en curso, la llamada de retorno en vuelo se descarta de forma segura; no se aplica ningún estado parcial.

## Consejos

- Si no está seguro de qué MTU usar, comience en 1400 bytes y auméntelo hasta que observe pérdida de paquetes o cortes de audio; luego redúzcalo entre 10–20 bytes.
- El ajuste **Audio Buffer:** (que se encuentra en la pestaña **Audio**) puede ayudar a absorber la variación de retardo (jitter) en enlaces VPN de forma independiente al ajuste de MTU. Consulte [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md).

## Solución de problemas

- **Apply no tiene efecto visible** — Confirme que la radio sigue conectada. Si la conexión se interrumpió, reconéctese mediante `Settings > Connect to Radio...` y repita los pasos.
- **El audio se corta después de cambiar el MTU** — Es posible que el nuevo valor siga siendo demasiado grande para la ruta. Reduzca **Network MTU:** otros 20–50 bytes y haga clic en **Apply** de nuevo.
- **El botón Start permanece desactivado después de la calibración** — Si el diálogo se cerró y se volvió a abrir durante un barrido, haga clic en **Start** de nuevo con la frecuencia de calibración deseada. La ejecución anterior se descartó de forma limpia.

## Relacionados

- [Cambiar la radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Seleccionar Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
