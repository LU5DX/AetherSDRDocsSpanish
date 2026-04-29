# Descripción general de la configuración del radio

El diálogo Radio Setup es la ventana central de configuración de su FLEX-8600. Reúne en un solo lugar la identificación del radio, la red, el GPS, la transmisión, el audio, los filtros, los transvertidores, los cables USB, los periféricos y los ajustes del puerto serie para FlexControl. Ábralo cada vez que necesite cambiar la forma en que AetherSDR interactúa con el hardware de su radio.

## Antes de comenzar

- El radio debe estar conectado. Radio Setup requiere una conexión de radio activa.

## Cómo funciona

Abra Radio Setup desde `Settings > Radio Setup...`. El diálogo contiene una fila de pestañas en la parte superior; cada pestaña cubre un área de configuración específica. Las pestañas distintas a Radio cargan su contenido la primera vez que hace clic en ellas.

También puede ir directamente a pestañas específicas:

- `Settings > USB Cables...` abre Radio Setup con la pestaña **USB Cables** activa.
- `Settings > FlexControl...` abre Radio Setup con la pestaña **Serial** activa (disponible únicamente cuando el soporte de puerto serie está integrado).

El diálogo recuerda su tamaño y posición entre sesiones.

### Resumen de pestañas

| Pestaña | Qué se configura aquí |
|---|---|
| **Radio** | Número de serie, versión de hardware, región, opciones con licencia, apodo, indicativo, nombre de la estación, información de licencia y actualización de firmware. |
| **Network** | Dirección IP (DHCP o estática), MTU de red y aplicación de IP privada. |
| **GPS** | Estado GPS en tiempo real: latitud, longitud, altitud, hora y cantidad de satélites. |
| **TX** | Tiempos de retención/retardo de TX, enclavamientos, límite de potencia global, modo de sintonía, visualización de TX en el waterfall, comportamiento de seguimiento TX/slice, y acceso directo a los ajustes por banda. |
| **Phone/CW** | Medidor de nivel de micrófono, keyer iambic (modo A/B, inversión, banda lateral), CWX, decodificador CW y marca predeterminada de RTTY. |
| **RX** | Calibración de desplazamiento de frecuencia y selección de fuente de referencia de 10 MHz. Los controles de calibración están siempre visibles; cuando hay un GPSDO instalado, la etiqueta de estado confirma su presencia. |
| **Audio** | Niveles de salida de línea, auriculares y altavoz; códec de compresión de audio; selección de dispositivo de audio del PC; aumento de audio; tamaño del búfer de audio; modo de grabación, carpeta, grabación automática al transmitir y tiempo de espera por inactividad; control del contenedor NVIDIA BNR. |
| **Filters** | Selección de filtro de baja latencia o de corte pronunciado por ancho de banda, y una opción separada para modos digitales. |
| **XVTR** | Configuración por transvertidor; crear o eliminar entradas de transvertidor. |
| **USB Cables** | Asignación de adaptadores serie USB a tipos de cable CAT, BCD, bit y PTT, y configuración de sus parámetros serie. |
| **Peripherals** | Conexión IP manual a dispositivos externos: TGXL, PGXL y Antenna Genius. |
| **Serial** | Selección de puerto serie para FlexControl, parámetros de línea, asignación de funciones de pines (DTR/RTS), inversión de paleta, apertura automática y detección del mando de sintonía. (Visible únicamente cuando el soporte de puerto serie está integrado.) |

## Qué hace cada control

Los siguientes controles tienen claves de configuración persistentes.

| Control | Pestaña | Comportamiento |
|---|---|---|
| **Audio Compression (SmartLink):** Auto / Uncompressed / Opus | Audio | Selecciona el códec de audio utilizado a través de SmartLink o LAN. |
| **Audio Boost:** | Audio | Habilita ganancia adicional en la ruta de audio del lado del cliente. |
| **Audio Buffer:** | Audio | Aumenta el búfer de audio para absorber la fluctuación de latencia (jitter) de VPN o SmartLink. |
| **Recording:** Radio Side / Client Side | Audio | Selecciona si las grabaciones se capturan en el radio o en esta computadora. |
| **Save to:** | Audio | Ruta de la carpeta donde se guardan las grabaciones. |
| **Auto-record on TX** | Audio | Inicia automáticamente la grabación cada vez que el radio transmite. |
| **Idle timeout:** | Audio | Segundos de silencio tras los cuales una grabación activa se detiene automáticamente. |
| TX Follows Active Slice | TX sigue al slice activo. Mutuamente exclusivo con 'Active Slice Follows TX'. | Se deshabilita automáticamente durante la operación en Split. |
| Active Slice Follows TX | Cambia el slice activo cuando TX se desplaza externamente (p. ej., WSJT-X o CAT). Mutuamente exclusivo con 'TX Follows Active Slice'. | |
| Controles deslizantes de nitidez de filtro Voice / CW / Digital | Establece la nitidez del filtro (0 = menor latencia, 3 = máxima nitidez) por modo; el control deslizante se deshabilita cuando Auto está activo. | Comandos enviados como 'radio filter_sharpness \<mode\> level=\<N\>'. |
| Auto (Voice / CW / Digital) | Habilita la selección automática del nivel de filtro para ese modo; deshabilita el control deslizante de nitidez manual. | Comandos enviados como 'radio filter_sharpness \<mode\> auto_level=1'. |
| Connect / Disconnect (TGXL) | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en TGXL_ManualIp y TGXL_ManualPort al conectarse, de modo que AetherSDR se vuelva a conectar automáticamente al iniciar. | Necesario para recuperar TUNE en firmware 4.2 o posterior. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL (TgxlConnection::requestAutotune()) en lugar de la ruta `tgxl autotune handle=<H>` del lado del radio, que no funciona en firmware 4.2. El TGXL controla el PTT del radio mediante su cable de enclavamiento de hardware; no se requiere activación desde el cliente. Si el campo IP está vacío y el radio ha descubierto el TGXL, la IP descubierta se completa automáticamente. |
| Connect / Disconnect (PGXL) | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en PGXL_ManualIp y PGXL_ManualPort. | |
| Connect / Disconnect (Antenna Genius) | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en AG_ManualIp y AG_ManualPort. | |

## Pestaña RX — calibración de frecuencia

En la versión v0.9.2.1 se revisó el diseño de la pestaña RX. Los controles de calibración ahora están siempre visibles, independientemente de si hay un GPSDO instalado. Una etiqueta de estado en la parte superior del grupo cambia de color y texto para reflejar el hardware presente:

- **GPSDO instalado** — etiqueta en verde: "GPSDO installed. Manual frequency offset calibration available."
- **Sin GPSDO** — etiqueta en ámbar: "Manual frequency offset calibration available."

El campo **Cal Frequency (MHz):** y el botón **Start** están siempre presentes. Al hacer clic en **Start**:

1. AetherSDR valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, una etiqueta de estado junto al botón muestra "Enter cal frequency" en ámbar y la calibración no continúa.
2. El error de frecuencia almacenado en el radio se restablece a cero (`radio set freq_error_ppb=0`) antes de que comience el barrido.
3. El botón **Start** se deshabilita y su etiqueta cambia a **Busy** durante la calibración.
4. Una etiqueta de estado a la derecha del botón informa el progreso ("Starting...", y luego actualizaciones en tiempo real mientras se ejecuta la calibración).
5. Cuando la calibración finaliza o falla, el botón se vuelve a habilitar y la etiqueta de estado se actualiza con el resultado.

El procedimiento de calibración envía `radio set cal_freq=<value>`, luego `radio set freq_error_ppb=0`, y a continuación inicia el barrido PLL del radio. Los mensajes de diagnóstico se escriben en el canal de registro del protocolo.

**Para ejecutar una calibración de frecuencia manual:**

1. Abra la pestaña **RX**.
2. Ingrese una frecuencia de referencia conocida y precisa en **Cal Frequency (MHz):**.
3. Haga clic en **Start**.
4. Espere a que la etiqueta de estado confirme la finalización. No cambie la frecuencia ni transmita durante el barrido.

## Consejos

- Si opera a través de una VPN o SmartLink y escucha interrupciones de audio, aumente **Audio Buffer:** hacia el extremo superior de su rango de 50–1000 ms.
- **Auto-record on TX** combinado con **Idle timeout:** es útil para el registro de concursos: la grabación comienza cuando activa la transmisión y se detiene automáticamente tras un período de silencio configurable.
- El botón **TX Band Settings** en la pestaña TX abre el diálogo dedicado de potencia y sintonía por banda, el mismo disponible en `Settings > TX Band Settings...`.
- Si **Start** en la pestaña RX permanece con la etiqueta **Busy** más tiempo de lo esperado, verifique que el valor de **Cal Frequency (MHz):** sea una frecuencia válida alcanzable por el radio y que no haya otra calibración en curso.

## Relacionados

- [Establecer el apodo, el indicativo y el nombre de la estación del radio](set-the-radio-nickname-callsign-and-station-name.md)
- [Verificar el número de serie, la versión de hardware, la región y las opciones del radio](check-radio-serial-hardware-version-region-and-options.md)
- [Cargar un nuevo firmware .ssdr en el radio](upload-a-new-firmware-ssdr-to-the-radio.md)
- [Cambiar el radio entre DHCP e IP estática](switch-the-radio-between-dhcp-and-static-ip.md)
- [Cambiar el MTU de red para configuraciones VPN/remotas](change-network-mtu-for-vpn-remote-setups.md)
- [Establecer la potencia máxima de TX y el modo de sintonía por banda](set-per-band-tx-max-power-and-tune-mode.md)
- [Seleccionar el modo iambic A o B para el keyer del radio](select-iambic-mode-a-or-b-for-the-radio-keyer.md)
- [Calibrar el desplazamiento de frecuencia del GPSDO](calibrate-the-gpsdo-frequency-offset.md)
- [Cambiar a una referencia externa de 10 MHz](switch-to-an-external-10-mhz-reference.md)
- [Elegir los dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática al transmitir y elegir una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
