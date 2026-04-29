# Activar grabación automática al transmitir y elegir una carpeta de destino

Cuando la grabación automática al transmitir está habilitada, AetherSDR inicia la grabación de audio automáticamente cada vez que usted transmite y se detiene tras un tiempo de inactividad configurable. Esta página explica cómo activar esa función y elegir dónde se guardan las grabaciones.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Decida si desea grabación en el lado de la radio o en el lado del cliente, ya que esto afecta dónde se captura el audio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio. La selección activa aparece resaltada. Esta elección se guarda en `RecordingMode`.
4. En el campo **Save to:**, escriba la ruta completa a su carpeta de grabaciones o haga clic en **...** para buscar una carpeta. La ruta se guarda en `QsoRecordingDir`.
5. Marque la casilla **Auto-record on TX**. Esto habilita la grabación automática cada vez que la radio pasa al modo de transmisión. El ajuste se guarda en `QsoRecordingAutoRecord`.
6. Establezca **Idle timeout:** con la cantidad de segundos de silencio tras los cuales se detiene la grabación. El valor se guarda en `QsoRecordingIdleTimeout`.
7. Cierre el diálogo. Los ajustes surten efecto de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado |
|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en la radio o en este PC. | Radio Side |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. El valor predeterminado es Documents/AetherSDR/Recordings. | — |
| **...** | Abre un explorador de carpetas para seleccionar la ubicación de destino. | — |
| **Auto-record on TX** | Cuando está marcada, la grabación se inicia automáticamente en cada transmisión y se detiene tras expirar el tiempo de inactividad. | Sin marcar |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga después de finalizar la transmisión. | 120 s |
| **TX Follows Active Slice** | La TX sigue al slice (canal de recepción) activo. Es mutuamente exclusivo con **Active Slice Follows TX**. Se deshabilita automáticamente durante la operación en Split. | Off |
| **Active Slice Follows TX** | Cambia el slice activo cuando la TX se mueve externamente (p. ej., WSJT-X o CAT). Es mutuamente exclusivo con **TX Follows Active Slice**. | Off |
| **Controles deslizantes de nitidez de filtro Voice / CW / Digital** | Establece la nitidez del filtro (0 = menor latencia a 3 = mayor nitidez) por modo. El control se deshabilita cuando Auto está habilitado. Los comandos se envían como `radio filter_sharpness <mode> level=<N>`. | — |
| **Auto (Voice / CW / Digital)** | Habilita la selección automática del nivel de filtro para ese modo y deshabilita el control deslizante manual de nitidez. Los comandos se envían como `radio filter_sharpness <mode> auto_level=1`. | — |
| **Connect / Disconnect (TGXL)** | Abre o cierra la conexión TCP directa al TGXL en el puerto 9010. Guarda la IP y el puerto en `TGXL_ManualIp` y `TGXL_ManualPort` al conectar, para que AetherSDR se reconecte automáticamente al inicio. Es necesario para recuperar TUNE en el firmware 4.2 y posteriores. Cuando está conectado, el botón TUNE envía el comando nativo `autotune` directamente al TGXL en lugar de la ruta del lado de la radio que dejó de funcionar en el firmware 4.2. El TGXL controla el PTT de la radio mediante su cable de enclavamiento de hardware; no se requiere activación por parte del cliente. Si el campo IP está vacío y la radio ha detectado el TGXL, la IP detectada se completa automáticamente. | Connect |
| **Connect / Disconnect (PGXL)** | Abre o cierra la conexión TCP directa al Power Genius XL (puerto predeterminado 9008). Guarda la IP y el puerto en `PGXL_ManualIp` y `PGXL_ManualPort`. | Connect |
| **Connect / Disconnect (Antenna Genius)** | Abre o cierra la conexión al Antenna Genius (puerto predeterminado 9007). Guarda la IP y el puerto en `AG_ManualIp` y `AG_ManualPort`. | Connect |

## Calibración de frecuencia (pestaña RX)

La pestaña **RX** proporciona calibración manual de desplazamiento de frecuencia y selección de la fuente de referencia de 10 MHz.

En la versión v0.9.2.1, los controles de calibración están disponibles independientemente de si hay un GPSDO instalado. Cuando hay un GPSDO presente, la etiqueta de estado muestra "GPSDO installed. Manual frequency offset calibration available." (en verde). Sin un GPSDO, la etiqueta muestra "Manual frequency offset calibration available." (en ámbar).

### Controles de calibración

| Control | Función |
|---|---|
| **Cal Frequency (MHz):** | Introduzca la frecuencia de referencia conocida en MHz. El valor se envía a la radio como `radio set cal_freq=<value>` al terminar de editar el campo. |
| **Start** | Restablece el error de frecuencia a 0 ppb (`radio set freq_error_ppb=0`) y luego inicia el barrido de calibración. La etiqueta del botón cambia a **Busy** y se deshabilita mientras la calibración está en curso. Una etiqueta de estado junto al botón informa el progreso. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones. |
| **10 MHz Reference Source:** | Selecciona la referencia del oscilador: Auto, TCXO, GPSDO o External. Las opciones mostradas dependen del hardware instalado. Un indicador de estado de bloqueo en tiempo real (Locked / Unlocked) aparece junto al selector. |

### Iniciar una calibración

1. Haga clic en la pestaña **RX** en Radio Setup.
2. Introduzca la frecuencia de referencia conocida en **Cal Frequency (MHz):**.
3. Haga clic en **Start**. El botón muestra **Busy** mientras se ejecuta el barrido. Observe la etiqueta de estado para ver el progreso y el resultado.
4. Cuando la calibración finaliza, el botón se vuelve a habilitar y la etiqueta de estado muestra el resultado.

> **Nota:** Si deja **Cal Frequency (MHz):** vacío y hace clic en **Start**, aparecerá una advertencia ("Enter cal frequency") y la calibración no comenzará.

## Sugerencias

- Si utiliza SmartLink o una VPN, considere si **Radio Side** o **Client Side** se adapta mejor al lugar donde desea almacenar los archivos. Las grabaciones del lado de la radio permanecen en el FLEX-8600; las grabaciones del lado del cliente van a la carpeta establecida en **Save to:**.
- Establezca **Idle timeout:** en un valor bajo (unos pocos segundos) si desea que cada transmisión se capture como un archivo separado. Un valor más alto fusiona las pausas dentro de un QSO en un único archivo.

## Solución de problemas

- **No aparecen archivos en la carpeta de destino después de transmitir** — Confirme que **Auto-record on TX** esté marcada y que la ruta en **Save to:** exista y tenga permisos de escritura. Si la carpeta no existe, AetherSDR no puede crear el archivo.
- **El campo Save to: no muestra ninguna ruta** — Haga clic en **...** y seleccione una carpeta explícitamente. Dejar el campo vacío puede impedir que la grabación comience.
- **El botón Start permanece deshabilitado después de hacer clic** — Verifique que **Cal Frequency (MHz):** contenga un valor de frecuencia válido. El botón se vuelve a habilitar automáticamente cuando la calibración finaliza o falla.

## Relacionado

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre audio Opus o sin compresión para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
