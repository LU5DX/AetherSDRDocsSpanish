# Cambiar la radio entre DHCP e IP estática

Use esta página para cambiar cómo el FLEX-8600 obtiene su dirección de red: automáticamente mediante DHCP o con una IP estática fija, máscara de subred y puerta de enlace que usted especifique.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Network solo está disponible cuando hay una conexión de radio activa.
- Si va a cambiar a IP estática, tenga listos la dirección IP, la máscara de subred y los valores de la puerta de enlace antes de comenzar.
- Cambiar la configuración de red hará que la radio se mueva a una nueva dirección. Deberá volver a conectarse después de aplicar los cambios.

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Network**.
3. Anote la **IP Address**, la **Mask** y la **MAC Address** actuales que se muestran como indicadores de solo lectura.
4. Haga clic en el botón de alternancia **DHCP / Static** para cambiar de modo. El botón refleja el modo actual; al hacer clic en él se cambia al otro.
5. Si seleccionó el modo estático, complete los campos de texto **IP Address:**, **Mask:** y **Gateway:** con los valores de su red.
6. Haga clic en **Apply** para enviar la configuración de red a la radio.
7. Vuelva a conectarse a la radio en su nueva dirección usando `Settings > Connect to Radio...`.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **IP Address / Mask / MAC Address** | Indicadores (solo lectura) | Muestra las direcciones de red actuales de la radio. |
| **DHCP / Static** | Botón de alternancia | Cambia la radio entre los modos DHCP e IP estática. |
| **IP Address:** | Campo de texto | Dirección IP estática que se asignará a la radio. Activo solo en modo estático. |
| **Mask:** | Campo de texto | Máscara de subred para la configuración estática. Activo solo en modo estático. |
| **Gateway:** | Campo de texto | Puerta de enlace predeterminada para la configuración estática. Activo solo en modo estático. |
| **Apply** | Botón de acción | Envía la configuración de red a la radio. |
| **TX Follows Active Slice** | Botón de acción | La transmisión sigue al slice (segmento de recepción) activo. Mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación Split. |
| **Active Slice Follows TX** | Botón de acción | Cambia el slice activo cuando la transmisión se mueve externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con **TX Follows Active Slice**. |
| **Voice / CW / Digital filter sharpness sliders** | Controles deslizantes (0–3) | Establece la nitidez del filtro (0 = menor latencia, 3 = máxima nitidez) por modo. El control se deshabilita cuando Auto está activado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. |
| **Auto (Voice / CW / Digital)** | Botón de alternancia | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. |
| **Connect / Disconnect (TGXL)** | Botón de acción | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Al conectar, guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` para que AetherSDR se reconecte automáticamente al iniciar. Necesario para recuperar TUNE en el firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que falló en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de interbloqueo de hardware; no se requiere keying desde el cliente. Si el campo de IP está vacío y la radio ha detectado el TGXL, la IP detectada se completa automáticamente. |
| **Connect / Disconnect (PGXL)** | Botón de acción | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. |
| **Connect / Disconnect (Antenna Genius)** | Botón de acción | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia y selección de la fuente de referencia de 10 MHz. En la versión v0.9.2.1, los controles de calibración se muestran siempre, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo indica el estado del GPSDO:

- **GPSDO instalado** — etiqueta en verde: *GPSDO installed. Manual frequency offset calibration available.*
- **Sin GPSDO** — etiqueta en ámbar: *Manual frequency offset calibration available.*

### Controles de calibración

| Control | Tipo | Comportamiento |
|---|---|---|
| **Cal Frequency (MHz):** | Spinbox / campo de texto | Frecuencia utilizada para la calibración. No debe estar vacío antes de iniciar. |
| **Start** | Botón de acción | Inicia la secuencia de calibración de frecuencia. Establece `cal_freq`, restablece `freq_error_ppb` a 0 y luego activa la calibración PLL de la radio. El botón se deshabilita y muestra **Busy** mientras la calibración está en curso. Una etiqueta de estado junto al botón informa el progreso (Starting… / running / result). |
| **Freq Offset (ppb):** | Spinbox | Desplazamiento de frecuencia manual en partes por mil millones. Se establece en 0 automáticamente al inicio de una ejecución de calibración. |
| **10 MHz Reference Source:** | Cuadro combinado | Selecciona la fuente de referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. El estado de enganche en tiempo real (Locked / Unlocked) se muestra junto al cuadro. |

### Cómo funciona la calibración en v0.9.2.1

1. Ingrese la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
2. Haga clic en **Start**. AetherSDR envía `radio set cal_freq=<value>` y `radio set freq_error_ppb=0` a la radio, luego emite `radio pll_start` para iniciar el barrido.
3. El botón **Start** se deshabilita y se etiqueta como **Busy** hasta que la secuencia se complete o falle.
4. La etiqueta de estado junto al botón se actualiza en tiempo real. Cuando la calibración finaliza, el botón se vuelve a habilitar y la etiqueta muestra el resultado.

Si el campo **Cal Frequency (MHz):** está vacío al hacer clic en **Start**, la etiqueta de estado muestra *Enter cal frequency* en ámbar y la calibración no se inicia.

> **Nota:** Antes de la versión v0.9.2.1, los controles de calibración se ocultaban cuando se detectaba un GPSDO. Ahora siempre están disponibles.

## Consejos

- Los indicadores **IP Address / Mask / MAC Address** muestran lo que la radio está usando actualmente. Registre estos valores antes de realizar cambios para poder revertirlos si es necesario.
- El interruptor **Enforce Private IP Connections:** en la misma pestaña rechaza conexiones desde direcciones que no sean RFC1918. Si asigna una IP estática, confirme que esté dentro de un rango privado (p. ej., 192.168.x.x, 10.x.x.x) si ese interruptor está habilitado.

## Solución de problemas

- **No se puede encontrar la radio después de hacer clic en Apply** — La radio se ha movido a su nueva dirección. Use `Settings > Connect to Radio...` para descubrirla y volver a conectarse a ella en la dirección actualizada.
- **Los campos IP Address:, Mask: y Gateway: no son editables** — El interruptor está configurado en DHCP. Haga clic en **DHCP / Static** para cambiar primero al modo estático.
- **El botón Start permanece deshabilitado después de la calibración** — Si el diálogo se cierra o la radio se desconecta mientras la calibración está en curso, el estado del botón se descarta. Vuelva a abrir Radio Setup e inténtelo de nuevo.
- **La etiqueta de estado muestra "Enter cal frequency"** — Escriba una frecuencia válida en MHz en el campo **Cal Frequency (MHz):** antes de hacer clic en **Start**.

## Relacionados

- [Cambiar la MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Verificar número de serie, versión de hardware, región y opciones de la radio](check-radio-serial-hardware-version-region-and-options.md)
