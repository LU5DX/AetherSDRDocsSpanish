# Activar la grabación automática al transmitir y elegir una carpeta de destino

AetherSDR puede iniciar automáticamente la grabación de audio cada vez que usted transmite y detenerla tras un período de silencio configurable. Esta página explica cómo activar esa función y dónde se guardan las grabaciones.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. Radio Setup requiere una conexión de radio activa.
- Decida si desea que las grabaciones se realicen en el lado del radio o en el lado del cliente (PC) antes de empezar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. En **Recording:**, haga clic en **Radio Side** o en **Client Side** para seleccionar dónde se captura el audio. Esto establece `RecordMode`.
4. En el campo **Save to:**, escriba directamente una ruta de carpeta o haga clic en **...** para abrir un explorador de carpetas. La ruta elegida se guarda como `RecordDir`.
5. Marque **Auto-record on TX**. Esto establece `AutoRecordTx` y habilita la grabación automática cada vez que el radio comienza a transmitir.
6. Establezca **Idle timeout:** con el número de segundos de silencio tras los cuales se detiene la grabación. Esto establece `RecordIdleTimeout`.
7. Haga clic en **Close**.

## Qué hace cada control

| Control | Comportamiento | Predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| **Recording: Radio Side / Client Side** | Selecciona si el audio se captura en el radio o en este PC. | — | Radio Side, Client Side | `RecordMode` |
| **Save to:** | Ruta de la carpeta donde se escriben los archivos de grabación. | — | Cualquier ruta con permisos de escritura | `RecordDir` |
| **...** | Abre un cuadro de diálogo para seleccionar la carpeta de destino. | — | — | — |
| **Auto-record on TX** | Cuando está marcado, la grabación se inicia automáticamente cada vez que el radio transmite. | — | Marcado / desmarcado | `AutoRecordTx` |
| **Idle timeout:** | Segundos de silencio antes de que se cierre la grabación activa. | — | — | `RecordIdleTimeout` |

## Consejos

- El botón **...** abre un cuadro de diálogo estándar de exploración de carpetas. Si prefiere escribir una ruta, haga clic en **Save to:** y edítela directamente.
- La grabación en Radio Side utiliza la ruta de audio propia del radio. La grabación en Client Side captura el flujo de audio tal como llega al PC. Elija Client Side si opera de forma remota a través de SmartLink y desea grabar lo que realmente escucha.
- Establecer **Idle timeout:** en un valor bajo produce muchos archivos cortos si realiza transmisiones breves y frecuentes. Auméntelo para consolidar un intercambio de concurso o un pileup en CW en un solo archivo.

## Solución de problemas

- **No se crean grabaciones después de transmitir** — Confirme que **Auto-record on TX** esté marcado y que la ruta en **Save to:** exista y tenga permisos de escritura para el usuario que ejecuta AetherSDR. Si la carpeta no existe, créela primero.
- **El campo Save to: aparece vacío al volver a abrir el cuadro de diálogo** — La ruta se almacena en `RecordDir`. Si nunca se seleccionó una carpeta, el campo estará vacío. Haga clic en **...**, elija una carpeta y cierre el cuadro de diálogo para guardar la configuración.

## Temas relacionados

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
