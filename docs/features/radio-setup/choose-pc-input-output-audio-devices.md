# Seleccionar dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué dispositivos de audio del PC utiliza AetherSDR para la salida de audio de recepción del radio y la entrada de micrófono. Es necesario hacer esto al configurar AetherSDR por primera vez o al cambiar auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- El radio debe estar conectado. Los controles de Radio Setup no están disponibles sin una conexión activa al radio.
- Verifique qué dispositivos de entrada y salida de audio expone su PC (consulte la configuración de audio del sistema operativo si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el dispositivo que desea usar para el micrófono o la entrada de audio.
4. Haga clic en el menú desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones tienen efecto de inmediato.

## Qué hace cada control

| Control | Qué hace | Predeterminado |
|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del sistema (micrófono, interfaz de audio, etc.). | Predeterminado del sistema |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del sistema (altavoces, auriculares, interfaz de audio, etc.). | Predeterminado del sistema |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Off |
| **Audio Buffer:** | Aumenta el búfer de audio del cliente para absorber la fluctuación en conexiones VPN o SmartLink. | — |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio utilizado a través de SmartLink o LAN. | Auto |
| **Recording: Radio Side / Client Side** | Selecciona si las grabaciones se capturan en el radio o en el cliente. | — |
| **Save to:** | Carpeta donde se guardan las grabaciones. | — |
| **...** | Abre un explorador de carpetas para seleccionar el directorio de grabación. | — |
| **Auto-record on TX** | Inicia la grabación automáticamente al transmitir. | Off |
| **Idle timeout:** | Segundos de silencio tras los cuales una grabación activa se detiene automáticamente. | — |
| **TX Follows Active Slice** | La TX sigue al slice (canal) activo. Mutuamente excluyente con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. | Off |
| **Active Slice Follows TX** | Cambia el slice activo cuando la TX se mueve externamente (por ejemplo, WSJT-X o CAT). Mutuamente excluyente con **TX Follows Active Slice**. | Off |
| **Voice / CW / Digital filter sharpness sliders** | Establece la nitidez del filtro (0=menor latencia a 3=mayor nitidez) por modo. Se deshabilita cuando Auto está activado para ese modo. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante de nitidez manual. | — |
| **Connect / Disconnect (TGXL)** | Abre/cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al iniciar. | Requerido para recuperar TUNE en firmware 4.2+. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado del radio que quedó inoperativa en el firmware 4.2. El TGXL controla el PTT del radio a través de su cable de enclavamiento de hardware; no se necesita control de tecla del lado del cliente. Si el campo de IP está vacío y el radio ha detectado el TGXL, la IP detectada se completa automáticamente. |
| **Connect / Disconnect (PGXL)** | Abre/cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | — |
| **Connect / Disconnect (Antenna Genius)** | Abre/cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. | — |

## Cambios en la calibración de frecuencia en v0.9.2.1

El panel de calibración de la pestaña **RX** ha sido rediseñado. En versiones anteriores, el campo **Cal Frequency (MHz):**, el botón **Start** y los controles manuales **Freq Offset (ppb):** estaban ocultos cuando se detectaba un GPSDO. A partir de v0.9.2.1, estos controles son siempre visibles independientemente de si hay un GPSDO instalado.

El indicador de estado en la parte superior del grupo de calibración ahora muestra:

- **Verde** — "GPSDO installed. Manual frequency offset calibration available." (GPSDO presente)
- **Ámbar** — "Manual frequency offset calibration available." (sin GPSDO)

### Cómo funciona la calibración ahora

Al hacer clic en **Start**, AetherSDR:

1. Valida que el campo **Cal Frequency (MHz):** no esté vacío. Si está vacío, la etiqueta de estado muestra "Enter cal frequency" y la calibración no continúa.
2. Restablece el error de frecuencia a cero (`radio set freq_error_ppb=0`) antes de comenzar, de modo que cada ejecución de calibración parte desde una línea base conocida.
3. Deshabilita y cambia la etiqueta del botón **Start** a **Busy** mientras la calibración está en curso.
4. Envía `radio pll_start` y monitorea la respuesta. La etiqueta de estado se actualiza en tiempo real para reflejar el progreso (Starting… / estados en ejecución / resultado).
5. Reactiva el botón **Start** cuando la calibración se completa o falla.

El botón **Start** es seguro de usar mientras hay un GPSDO instalado; la referencia del GPSDO no se ve afectada.

Si navega fuera de la pestaña **RX** o cierra Radio Setup mientras la calibración está en curso, las devoluciones de llamada en progreso se descartan de forma segura — no se escribe ningún estado parcial.

## Consejos

- Los menús desplegables Input y Output listan únicamente los dispositivos que el sistema operativo expone actualmente. Si falta un dispositivo, conéctelo y vuelva a abrir la pestaña Audio — la enumeración de dispositivos ocurre cuando la pestaña se muestra por primera vez.
- Si el audio de recepción suena demasiado bajo con el dispositivo de salida elegido, active **Audio Boost:** antes de aumentar el volumen del sistema operativo.
- En conexiones VPN o SmartLink, aumente **Audio Buffer:** para reducir los cortes. Valores superiores a 200 ms añaden un retardo perceptible.
- En la pestaña **RX**, ingrese siempre una frecuencia de referencia precisa y conocida en **Cal Frequency (MHz):** antes de hacer clic en **Start**. El uso de una frecuencia incorrecta produce una corrección de desplazamiento errónea.

## Solución de problemas

- **No aparecen dispositivos de audio en los menús desplegables** — La pestaña Audio enumera los dispositivos al cargarse por primera vez. Cierre Radio Setup, verifique que el sistema operativo reconozca el dispositivo y luego vuelva a abrir `Settings > Radio Setup...` y haga clic en la pestaña Audio nuevamente.
- **El audio de recepción se reproduce a través del dispositivo incorrecto** — Es posible que el menú desplegable Output aún esté configurado con un dispositivo seleccionado anteriormente. Abra la pestaña Audio y vuelva a seleccionar la salida correcta.
- **El radio no escucha el micrófono** — Confirme que el dispositivo correcto esté seleccionado en el menú desplegable **Input:** y que el sistema operativo no haya silenciado ni bloqueado el acceso a ese dispositivo.
- **El botón Start permanece con la etiqueta Busy** — Una ejecución de calibración anterior no se completó. Cierre y vuelva a abrir Radio Setup para restablecer el estado de calibración y vuelva a intentarlo.
- **Aparece "Enter cal frequency" al hacer clic en Start** — Ingrese una frecuencia válida en MHz en el campo **Cal Frequency (MHz):** antes de hacer clic en **Start**.

## Relacionado

- [Elegir entre Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar Audio Boost o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
