# Seleccionar dispositivos de audio de entrada/salida del PC

Seleccione qué tarjeta de sonido o interfaz de audio del PC usa AetherSDR para reproducir el audio recibido y capturar el audio del micrófono. Esto es independiente de las salidas Line Out y Headphone propias del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio no es accesible sin una conexión activa al radio.
- Su interfaz de audio debe estar reconocida por el sistema operativo antes de abrir este diálogo.

## Pasos

1. Vaya a `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Bajo **PC Audio Devices:**, haga clic en el menú desplegable **Input:** y seleccione el dispositivo a usar para el micrófono o la entrada de audio.
4. Haga clic en el menú desplegable **Output:** y seleccione el dispositivo a usar para la reproducción del audio recibido.
5. Cierre el diálogo. La selección tiene efecto de inmediato.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango / valores válidos | Clave de configuración |
|---|---|---|---|---|
| **PC Audio Devices: Input:** | Selecciona el dispositivo de entrada de audio del sistema operativo (micrófono, línea de entrada). | Predeterminado del sistema | Dispositivos enumerados por el sistema operativo | — |
| **PC Audio Devices: Output:** | Selecciona el dispositivo de salida de audio del sistema operativo (altavoces, auriculares, interfaz de audio). | Predeterminado del sistema | Dispositivos enumerados por el sistema operativo | — |
| **Audio Boost:** | Aplica ganancia adicional en la ruta de audio del cliente. | Off | On / Off | `AudioBoost` |
| **Audio Buffer:** | Aumenta la profundidad del búfer de audio para absorber jitter en conexiones VPN o SmartLink. | — | 50–1000 ms | `AudioBuffer` |
| **Audio Compression (SmartLink): Auto / Uncompressed / Opus** | Selecciona el códec de audio usado a través de SmartLink o LAN. | Auto | Auto / Uncompressed / Opus | `AudioCompression` |
| **Recording: Radio Side / Client Side** | Elige si la grabación se realiza en el radio o en este PC. | — | Radio Side / Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se guardan las grabaciones. | — | Cualquier directorio con permiso de escritura | `RecordDir` |
| **...** | Abre un explorador de carpetas para elegir el directorio de grabación. | — | — | — |
| **Auto-record on TX** | Inicia automáticamente la grabación cuando el radio transmite. | Off | On / Off | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio tras los cuales se detiene una grabación activa. | — | — | `RecordIdleTimeout` |

## Consejos

- Si el dispositivo preferido no aparece en el menú desplegable, confirme que el sistema operativo lo reconoce y luego cierre y vuelva a abrir el diálogo **Radio Setup**. La pestaña Audio enumera los dispositivos cuando se muestra por primera vez.
- Use **Audio Buffer:** para reducir interrupciones de audio al operar a través de una VPN o un enlace de red lento. Los valores más altos añaden latencia; 50 ms es adecuado para LAN local, mientras que 200–400 ms es adecuado para la mayoría de las configuraciones remotas.
- **Audio Boost:** es útil cuando el nivel de audio entrante es bajo incluso con el volumen del slice (receptor parcial) al máximo.

## Solución de problemas

- **No aparecen dispositivos de audio en los menús desplegables Input u Output** — La pestaña Audio pospone la enumeración de dispositivos hasta que se abre. Si la lista sigue vacía, verifique que el subsistema de audio del sistema operativo esté en funcionamiento y que al menos un dispositivo esté habilitado en la configuración de sonido del sistema.
- **El audio se interrumpe durante la operación remota** — Aumente **Audio Buffer:** (rango 50–1000 ms) y considere cambiar **Audio Compression (SmartLink):** de Auto a Opus para reducir los requisitos de ancho de banda.

## Temas relacionados

- [Elegir Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática al transmitir y elegir una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
- [Iniciar/detener el contenedor NVIDIA BNR](start-stop-the-nvidia-bnr-container.md)
