# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) aplica reducción de ruido basada en inteligencia artificial al audio transmitido. Use esta página para iniciar, detener y verificar el estado del contenedor desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio solo es accesible mientras haya conexión activa.
- NVIDIA BNR requiere una GPU NVIDIA compatible y el entorno de ejecución de contenedores instalado en su sistema. Confirme que el entorno de contenedores funciona correctamente fuera de AetherSDR antes de continuar.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice el grupo **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para iniciar el contenedor, haga clic en **Start**.
5. Para detener el contenedor, haga clic en **Stop**.
6. Para habilitar el inicio automático, haga clic en **Autostart Container** para que se active cada vez que AetherSDR se conecte al radio.
7. Para verificar el estado actual, haga clic en **Check Status**. El indicador de estado de color junto a los controles se actualiza para reflejar Running, Stopped o Unknown.

## Qué hace cada control

| Control | Descripción |
|---|---|
| **Autostart Container** | Inicia el contenedor BNR automáticamente cada vez que AetherSDR se conecta al radio. |
| **Start** | Inicia el contenedor NVIDIA BNR de inmediato. |
| **Stop** | Detiene el contenedor NVIDIA BNR de inmediato. |
| **Check Status** | Consulta el estado del contenedor y actualiza el indicador de estado. |
| Indicador de estado | Indicador de color que muestra el estado del contenedor: Running, Stopped o Unknown. |

## Consejos

- Si usa BNR con regularidad, habilite **Autostart Container** para no tener que iniciarlo manualmente en cada sesión.
- Después de hacer clic en **Start** o **Stop**, haga clic en **Check Status** para confirmar que el estado cambió según lo esperado.

## Solución de problemas

- **El indicador de estado muestra Unknown después de hacer clic en Start** — Es posible que el entorno de ejecución de contenedores no esté instalado o no sea accesible. Verifique que el entorno de ejecución de contenedores NVIDIA esté correctamente instalado en su sistema y que la imagen de contenedor requerida esté disponible.
- **Start no tiene efecto** — Confirme que su sistema tiene una GPU NVIDIA compatible y que el motor de contenedores (por ejemplo, Docker o Podman con soporte NVIDIA) está en ejecución antes de iniciar AetherSDR.

## Relacionados

- [Seleccionar dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre audio Opus o sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
