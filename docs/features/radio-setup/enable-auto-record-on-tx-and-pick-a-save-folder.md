# Habilitar grabación automática en TX y seleccionar una carpeta de destino

Esta página explica cómo configurar AetherSDR para iniciar la grabación automáticamente cada vez que transmite, y cómo elegir dónde se guardan esas grabaciones. Esto resulta útil para registrar sus transmisiones sin tener que iniciar y detener manualmente una grabadora.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio en Radio Setup no está disponible sin una conexión activa a la radio.
- Decida si desea grabación del lado de la radio o del lado del cliente antes de comenzar, ya que el modo de grabación determina dónde se captura el audio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En el control **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio. El modo activo aparece resaltado. Esta opción se guarda como `RecordMode`.
4. En el campo **Save to:**, revise la ruta de carpeta actual. Para cambiarla, haga clic en **...** junto al campo y elija una carpeta en el navegador de archivos. La ruta seleccionada se guarda como `RecordDir`.
5. Active **Auto-record on TX**. Cuando está marcada, AetherSDR inicia la grabación cada vez que la radio transmite y la detiene al finalizar la transmisión (sujeto al tiempo de espera por inactividad). Esta opción se guarda como `AutoRecordTx`.
6. Ajuste **Idle timeout:** al número de segundos de silencio tras los cuales se detiene la grabación. Esta opción se guarda como `RecordIdleTimeout`.
7. Cierre el diálogo. Los ajustes surten efecto de inmediato.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en la radio o en el PC que ejecuta AetherSDR. | — | Radio Side \| Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. | — | Cualquier ruta de directorio válida | `RecordDir` |
| **...** | Abre un navegador de carpetas para seleccionar el directorio de destino. | — | — | — |
| **Auto-record on TX** | Cuando está marcada, la grabación se inicia automáticamente al transmitir y se detiene al quedar inactiva. | — | Checked \| Unchecked | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio tras el fin de la transmisión antes de que se cierre el archivo de grabación. | — | — | `RecordIdleTimeout` |

## Consejos

- Si utiliza SmartLink o una VPN, considere si la grabación del lado de la radio o del lado del cliente captura mejor el audio que desea. La grabación del lado de la radio captura lo que procesa la radio; la grabación del lado del cliente captura lo que llega al PC.
- Ajuste **Idle timeout:** a un valor suficientemente largo para cubrir breves pausas en su transmisión (como los intercambios entre cambios de turno) sin crear un nuevo archivo por cada activación de la tecla.

## Relacionados

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
