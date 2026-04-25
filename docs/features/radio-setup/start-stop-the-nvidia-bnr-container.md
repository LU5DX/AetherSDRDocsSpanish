# Iniciar/detener el contenedor NVIDIA BNR

Esta página explica cómo iniciar, detener y verificar el estado del contenedor de eliminación de ruido NVIDIA Broadcast (BNR) desde AetherSDR. Use BNR para aplicar reducción de ruido acelerada por GPU al audio recibido o transmitido.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio. La pestaña **Audio** en **Radio Setup** no es accesible sin una conexión de radio.
- El entorno de ejecución del contenedor NVIDIA Broadcast ya debe estar instalado en su sistema. AetherSDR no lo instala.
- Debe haber una GPU NVIDIA compatible presente y reconocida por su sistema.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Desplácese hasta la sección **NVIDIA BNR** en la parte inferior de la pestaña.
4. Para iniciar el contenedor, haga clic en **Start**.
5. Para detener el contenedor, haga clic en **Stop**.
6. Para confirmar el estado del contenedor sin modificarlo, haga clic en **Check Status**.
7. Para que AetherSDR inicie el contenedor automáticamente cada vez que se conecte a la radio, haga clic en **Autostart Container** para activarlo.

El indicador de estado de color junto a los controles de NVIDIA BNR se actualiza para reflejar el estado actual del contenedor: en ejecución, detenido o desconocido.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Cuando está activo, AetherSDR inicia el contenedor BNR automáticamente al conectarse a la radio. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR de inmediato. |
| **Stop** | Botón | Detiene el contenedor NVIDIA BNR de inmediato. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el indicador de estado sin modificar el contenedor. |
| Indicador de estado | Indicador | Punto de color que muestra Running, Stopped o Unknown. |

## Solución de problemas

- **El indicador de estado muestra Unknown después de hacer clic en Start** — Es posible que el entorno de ejecución del contenedor no esté instalado o que la GPU no sea accesible. Verifique la instalación de NVIDIA Broadcast y el controlador de GPU fuera de AetherSDR, luego haga clic en **Check Status** nuevamente.
- **Start y Stop no tienen efecto** — AetherSDR lanza el contenedor como subproceso. Si el binario de entorno de ejecución requerido no está en el PATH del sistema, el comando fallará silenciosamente. Confirme que el entorno de ejecución de NVIDIA Broadcast esté instalado y sea accesible desde una terminal antes de usar estos controles.

## Relacionado

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Seleccionar Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el refuerzo de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y elegir una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
