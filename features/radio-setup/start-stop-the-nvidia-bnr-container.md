# Iniciar/detener el contenedor NVIDIA BNR

El contenedor NVIDIA BNR (Broadcast Noise Removal) proporciona supresión de ruido basada en inteligencia artificial para el audio del micrófono. Use esta página para iniciar, detener y verificar el estado de ese contenedor desde AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio no funciona sin una conexión de radio activa.
- El entorno de ejecución del contenedor NVIDIA BNR debe estar instalado y accesible en su sistema antes de que AetherSDR pueda iniciarlo.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Desplácese hasta la sección **NVIDIA BNR** en la parte inferior de la pestaña.
4. Para iniciar el contenedor, haga clic en **Start**.
5. Para detener el contenedor, haga clic en **Stop**.
6. Para verificar si el contenedor está en ejecución, haga clic en **Check Status**. El indicador de estado de color ubicado junto a los controles se actualiza para reflejar Running, Stopped o Unknown.
7. Para que el contenedor se inicie automáticamente cada vez que AetherSDR se conecte al radio, haga clic en **Autostart Container** para activarlo.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Habilita el inicio automático del contenedor cuando AetherSDR se conecta al radio. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR. |
| **Stop** | Botón | Detiene el contenedor NVIDIA BNR. |
| **Check Status** | Botón | Consulta el contenedor y actualiza el indicador de estado. |
| Indicador de estado NVIDIA BNR | Indicador | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown. |

## Consejos

- Después de hacer clic en **Start**, haga clic en **Check Status** para confirmar que el contenedor alcanzó el estado Running antes de transmitir.
- Si no necesita BNR en cada sesión, deje **Autostart Container** inactivo e inicie el contenedor manualmente solo cuando sea necesario.

## Solución de problemas

- **El indicador de estado muestra Unknown después de hacer clic en Start** — Es posible que el entorno de ejecución del contenedor no esté instalado o no se encuentre en el PATH del sistema. Verifique que el entorno de ejecución de NVIDIA Broadcast esté correctamente instalado e intente de nuevo.
- **Start no tiene efecto** — Confirme que AetherSDR está conectado al radio. Los controles de la pestaña Audio están inactivos sin una conexión de radio activa.

## Temas relacionados

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Seleccionar Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
