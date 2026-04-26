# Activar grabación automática en TX y seleccionar una carpeta de destino

AetherSDR puede iniciar automáticamente la grabación de audio cada vez que usted transmite y detenerla después de un período de silencio configurable. Esta página explica cómo activar esa función y configurar la carpeta donde se guardan las grabaciones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio en Radio Setup no está disponible sin una conexión al radio.
- Decida si desea que la grabación ocurra en el radio mismo o en el PC donde se ejecuta AetherSDR. Deberá configurar esto antes de activar la grabación automática.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se capturan las grabaciones. Esto establece `RecordMode`.
4. En el campo **Save to:**, escriba directamente una ruta de carpeta o haga clic en **...** para buscar una carpeta. La ruta elegida se guarda como `RecordDir`.
5. Marque **Auto-record on TX**. Esto establece `AutoRecordTx` y habilita la grabación automática cada vez que el radio pasa a modo de transmisión.
6. Ajuste **Idle timeout:** al número de segundos de silencio tras los cuales se detiene la grabación. Esto establece `RecordIdleTimeout`.
7. Cierre el diálogo. Los ajustes se guardan de inmediato.

## Qué hace cada control

| Control | Comportamiento | Clave persistida | Valor predeterminado | Rango válido |
|---|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en el radio o en el PC. | `RecordMode` | — | Radio Side, Client Side |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. | `RecordDir` | — | Cualquier ruta de directorio válida |
| **...** | Abre un explorador de carpetas para seleccionar el destino de las grabaciones. | — | — | — |
| **Auto-record on TX** | Cuando está marcado, la grabación se inicia automáticamente cada vez que usted transmite. | `AutoRecordTx` | — | Marcado / desmarcado |
| **Idle timeout:** | Segundos de silencio después de TX antes de que se cierre el archivo de grabación. | `RecordIdleTimeout` | — | — |

## Consejos

- Si desea que las grabaciones queden separadas por transmisión en lugar de combinarse en un único archivo largo, mantenga **Idle timeout:** corto para que el archivo se cierre poco después de soltar el PTT.
- La ruta de **Save to:** debe existir y tener permisos de escritura antes de iniciar la grabación. AetherSDR no crea el directorio automáticamente.

## Relacionado

- [Seleccionar dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
