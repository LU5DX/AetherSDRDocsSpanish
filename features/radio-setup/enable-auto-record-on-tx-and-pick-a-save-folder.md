# Habilitar grabación automática en TX y elegir una carpeta de destino

AetherSDR puede iniciar la grabación automáticamente cada vez que transmita y detenerla después de un período de silencio configurable. Esta página muestra cómo activar esa función y elegir dónde se guardan las grabaciones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Los ajustes de grabación se encuentran en el diálogo Radio Setup, que requiere una conexión activa al radio.
- Decida si desea que las grabaciones se realicen en el radio mismo o en el PC que ejecuta AetherSDR (consulte "Recording: Radio Side / Client Side" más adelante).

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En la fila **Recording:**, haga clic en **Radio Side** o **Client Side** para elegir dónde se captura el audio. Esto establece `RecordMode`.
4. En el campo **Save to:**, escriba directamente una ruta de carpeta o haga clic en **...** para abrir un explorador de carpetas. La ruta elegida se guarda como `RecordDir`.
5. Marque **Auto-record on TX**. Esto establece `AutoRecordTx` y activa la grabación automática cada vez que el radio transmite.
6. Configure **Idle timeout:** con el número de segundos de silencio tras los cuales se detiene la grabación. Esto establece `RecordIdleTimeout`.
7. Cierre el diálogo con **Close**. Los ajustes se guardan de inmediato.

## Qué hace cada control

| Control | Función | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en el radio o en el PC cliente. | — | Radio Side, Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. | — | Cualquier ruta con permisos de escritura | `RecordDir` |
| **...** | Abre un explorador de carpetas para establecer **Save to:** sin escribir manualmente. | — | — | — |
| **Auto-record on TX** | Inicia la grabación automáticamente cuando el radio transmite; se detiene al expirar el tiempo de inactividad. | — | Activado / Desactivado | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio antes de que la grabación se detenga una vez finalizada la transmisión. | — | — | `RecordIdleTimeout` |

## Consejos

- Si selecciona la grabación en **Client Side**, los archivos guardados se almacenan en la ruta indicada en **Save to:** en la máquina que ejecuta AetherSDR. Si selecciona **Radio Side**, confirme que el radio dispone de almacenamiento disponible.
- Configure **Idle timeout:** con un valor corto (unos pocos segundos) para mantener cada transmisión como un archivo independiente, en lugar de combinar varios turnos en un único archivo largo.

## Solución de problemas

- **No se crean grabaciones después de habilitar Auto-record on TX** — Verifique que la ruta indicada en **Save to:** exista y tenga permisos de escritura. Si el campo está vacío, haga clic en **...** y seleccione una carpeta antes de habilitar la función.
- **El campo Save to: aparece deshabilitado o el botón ... no responde** — El diálogo requiere una conexión activa al radio. Confirme que el radio esté conectado antes de abrir `Settings > Radio Setup...`.

## Temas relacionados

- [Elegir dispositivos de audio de entrada/salida en el PC](choose-pc-input-output-audio-devices.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
