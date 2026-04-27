# Habilitar la grabación automática en TX y elegir una carpeta de destino

Cuando la grabación automática en TX está habilitada, AetherSDR comienza a grabar audio automáticamente cada vez que transmite y se detiene tras un tiempo de inactividad configurable. Esta página explica cómo activar esa función y elegir dónde se guardan las grabaciones.

## Antes de comenzar

- La radio debe estar conectada. Radio Setup requiere una conexión de radio activa.
- Decida si desea grabación en el lado de la radio o en el lado del cliente, ya que esto afecta dónde se captura el audio.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o **Client Side** para seleccionar dónde se captura el audio. La selección activa aparece resaltada. Esta elección se guarda en `RecordMode`.
4. En el campo **Save to:**, escriba la ruta completa a su carpeta de grabaciones, o haga clic en **...** para buscar una carpeta. La ruta se guarda en `RecordDir`.
5. Active la casilla **Auto-record on TX**. Esto habilita la grabación automática cada vez que la radio pasa al modo de transmisión. La configuración se guarda en `AutoRecordTx`.
6. Establezca **Idle timeout:** con el número de segundos de silencio tras los cuales se detiene la grabación. El valor se guarda en `RecordIdleTimeout`.
7. Cierre el cuadro de diálogo. La configuración surte efecto de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en la radio o en este PC. | — | Radio Side \| Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. | — | Cualquier ruta de directorio válida | `RecordDir` |
| **...** | Abre un explorador de carpetas para seleccionar la ubicación de destino. | — | — | — |
| **Auto-record on TX** | Cuando está activada, la grabación comienza automáticamente en cada transmisión y se detiene tras cumplirse el tiempo de inactividad. | — | Checked \| Unchecked | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio antes de que se detenga la grabación tras finalizar la TX. | — | — | `RecordIdleTimeout` |

## Consejos

- Si utiliza SmartLink o una VPN, considere si **Radio Side** o **Client Side** se adapta mejor al lugar donde desea almacenar los archivos. Las grabaciones en el lado de la radio permanecen en el FLEX-8600; las grabaciones en el lado del cliente se guardan en la carpeta definida en **Save to:**.
- Establezca **Idle timeout:** en un valor bajo (pocos segundos) si desea que cada transmisión se capture como un archivo separado. Un valor más alto fusiona las pausas dentro de un QSO en un solo archivo.

## Solución de problemas

- **No aparecen archivos en la carpeta de destino después de transmitir** — Confirme que **Auto-record on TX** esté activada y que la ruta indicada en **Save to:** exista y tenga permisos de escritura. Si la carpeta no existe, AetherSDR no puede crear el archivo.
- **El campo Save to: no muestra ninguna ruta** — Haga clic en **...** y seleccione una carpeta de forma explícita. Dejar el campo vacío puede impedir que la grabación se inicie.

## Temas relacionados

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
