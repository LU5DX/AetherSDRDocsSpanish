# Activar grabación automática en TX y elegir una carpeta de destino

Use esta página para configurar AetherSDR para que inicie la grabación automáticamente cada vez que transmita, y para elegir dónde se guardan esas grabaciones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los ajustes de grabación no están disponibles hasta que se establezca una conexión.
- Decida si desea que el propio radio o su PC se encargue de la grabación. Consulte "Qué hace cada control" más adelante para conocer la diferencia.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio. La selección activa aparece resaltada.
4. En el campo **Save to:**, escriba la ruta completa a la carpeta donde deben guardarse las grabaciones, o haga clic en **...** para abrir un explorador de carpetas y seleccionarla.
5. Marque **Auto-record on TX**. A partir de ahora, la grabación se iniciará automáticamente cada vez que active el transmisor.
6. Establezca **Idle timeout:** con el número de segundos de silencio tras los cuales la grabación se detiene automáticamente.
7. Cierre el diálogo. Los ajustes se guardan de inmediato.

## Qué hace cada control

| Control | Qué hace | Valor predeterminado | Rango / valores válidos | Clave de ajuste |
|---|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en el hardware del radio o en el PC que ejecuta AetherSDR. | — | Radio Side, Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. | — | Cualquier ruta de directorio con permisos de escritura | `RecordDir` |
| **...** | Abre un explorador de carpetas para seleccionar la carpeta de destino. | — | — | — |
| **Auto-record on TX** | Cuando está marcado, la grabación se inicia automáticamente cada vez que el radio transmite y se detiene al expirar el tiempo de espera por inactividad. | — | Marcado / desmarcado | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio tras el fin de TX antes de que se cierre el archivo de grabación. | — | — | `RecordIdleTimeout` |

## Consejos

- Si deja **Save to:** vacío, haga clic en **...** para explorar hasta una carpeta en lugar de escribir la ruta, para evitar errores tipográficos que podrían impedir silenciosamente que se escriban los archivos.
- **Idle timeout:** mantiene las pausas breves sin transmisión dentro de un único archivo, en lugar de dividir cada transmisión en una grabación separada. Auméntelo si desea que los intercambios de un QSO queden capturados juntos.

## Relacionado

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
