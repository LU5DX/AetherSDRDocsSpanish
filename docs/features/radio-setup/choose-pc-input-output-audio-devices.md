# Elegir dispositivos de audio de entrada/salida del PC

Esta página explica cómo seleccionar qué dispositivos de audio del PC utiliza AetherSDR para la salida de audio de recepción y la entrada de micrófono. Debe hacerlo la primera vez que configure AetherSDR o cuando cambie de auriculares, altavoces o interfaces de audio.

## Antes de comenzar

- La radio debe estar conectada. Los controles de configuración de la radio no están disponibles sin una conexión activa a la radio.
- Sepa qué dispositivos de entrada y salida de audio expone su PC (consulte la configuración de audio de su sistema operativo si no está seguro).

## Pasos

1. Haga clic en `Settings > Radio Setup...` para abrir el diálogo Radio Setup.
2. Haga clic en la pestaña **Audio**.
3. En **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el dispositivo que desea usar para el micrófono o la entrada de audio.
4. Haga clic en el menú desplegable **Output:** y seleccione el dispositivo que desea usar para la reproducción de audio de recepción.
5. Cierre el diálogo. Las selecciones surten efecto de inmediato.

## Qué hace cada control

| Control | Qué hace |
|---------|---------------|
| **Input:** (PC Audio Devices) | Selecciona el dispositivo de entrada de audio del host utilizado para el micrófono o la entrada de línea. |
| **Output:** (PC Audio Devices) | Selecciona el dispositivo de salida de audio del host utilizado para la reproducción de audio de recepción. |
| **Audio Boost:** | Alternancia que habilita ganancia adicional en la ruta de audio del cliente. Se almacena en AppSettings como `AudioBoost`. |
| **Audio Buffer:** | Campo de texto (valor predeterminado 200, rango 50–1000 ms) que aumenta el búfer de audio para compensar la fluctuación de VPN/SmartLink. Se almacena como `AudioBufferMs` y se aplica al límite del búfer RX del motor de audio. |
| **Prevent system sleep while connected** | Casilla de verificación (desactivada por defecto) que mantiene el sistema operativo despierto mientras la radio está conectada para evitar cortes en las transmisiones de audio/TCP/UDP durante períodos de inactividad. Se almacena como `InhibitSleepWhileConnected`. |
| **Recording: Radio Side / Client Side** | Alternancia que selecciona si las grabaciones se realizan en la radio (SmartSDR) o en el PC del cliente. Se almacena como `RecordingMode`. |
| **Save to:** | Campo de texto que establece la carpeta para las grabaciones del lado del cliente. El valor predeterminado es Documents/AetherSDR/Recordings. Se almacena como `QsoRecordingDir`. |
| **...** (examinar) | Abre un selector de carpetas para el directorio de grabaciones. |
| **Auto-record on TX** | Casilla de verificación (desactivada por defecto) que inicia la grabación automáticamente al transmitir. Se almacena como `QsoRecordingAutoRecord`. |
| **Idle timeout:** | Cuadro giratorio (valor predeterminado 120, rango 10–3600 segundos) que detiene la grabación después de esta cantidad de segundos de silencio. Se almacena como `QsoRecordingIdleTimeout`. |
| **Line Out:** | Control deslizante que ajusta la ganancia de salida de línea. |
| **Mute (Line Out)** | Botón que silencia la salida de línea. |
| **Headphone:** | Control deslizante que ajusta la ganancia de los auriculares. |
| **Mute (Headphone)** | Botón que silencia la salida de auriculares. |
| **Front Speaker: / Mute** | Botón que silencia el altavoz frontal (específico del modelo). |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio para conexiones SmartLink/LAN. Se almacena en `AudioCompression`. |
| **NVIDIA BNR: Autostart Container / Start / Stop / Check Status** | Controla el contenedor de eliminación de ruido NVIDIA Broadcast. Un indicador de estado muestra En ejecución/Detenido/Desconocido. |

## Pestaña Calibration

La pestaña **Calibration** es nueva en v26.8.4. Proporciona calibración manual de frecuencia para radios que no pueden calibrar su propio oscilador (como la HL2). La pestaña está oculta a menos que el backend de la radio conectada informe la capacidad `hostFrequencyCalibration`; por ejemplo, no aparece en las radios FLEX-8000, que se calibran mediante los controles GPSDO de la pestaña RX.

| Control | Qué hace |
|---------|---------------|
| **Cal Frequency (MHz):** | Cuadro giratorio que establece la frecuencia utilizada para la calibración manual. Requiere que la radio esté en esta frecuencia. |
| **Start** | Inicia el barrido de calibración de frecuencia. |
| **Freq Offset (ppb):** | Desplazamiento de frecuencia manual en partes por mil millones, que se muestra después de completar el barrido. |
| **Trim** | Aplica el desplazamiento medido al reloj del host de la radio. |

El valor de calibración almacenado se vuelve a leer cada vez que se muestra el diálogo y cada vez que cambia la conexión de la radio, de modo que una pulsación de Trim no puede confirmar por error la calibración de una radio anterior.
