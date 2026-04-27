# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) aplica supresión de ruido basada en inteligencia artificial al audio del micrófono. Use los controles de la pestaña Audio para iniciar, detener o verificar el estado del contenedor sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. La pestaña Audio no es accesible cuando está desconectado.
- El contenedor NVIDIA Broadcast debe estar instalado en su sistema de forma independiente a AetherSDR. AetherSDR lo controla, pero no lo instala.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Ubique la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que AetherSDR arranque, haga clic en **Autostart Container** de modo que esté activo.
5. Para iniciar el contenedor de inmediato, haga clic en **Start**.
6. Para detener un contenedor en ejecución, haga clic en **Stop**.
7. Para consultar el estado actual sin modificarlo, haga clic en **Check Status**. El indicador de estado de color ubicado junto a los controles se actualiza para reflejar Running, Stopped o Unknown.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Cuando está activo, AetherSDR inicia el contenedor NVIDIA BNR automáticamente al arrancar. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR de inmediato. |
| **Stop** | Botón | Detiene un contenedor NVIDIA BNR en ejecución de inmediato. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el indicador de estado. |
| Indicador de estado NVIDIA BNR | Indicador | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown. |

## Consejos

- Haga clic en **Check Status** después de hacer clic en **Start** o **Stop** si el indicador de estado no se actualiza por sí solo, para confirmar que el contenedor alcanzó el estado esperado.

## Relacionados

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Seleccionar Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el realce de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
