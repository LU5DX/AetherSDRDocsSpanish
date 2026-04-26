# Iniciar/detener el contenedor NVIDIA BNR

Esta página explica cómo iniciar, detener y verificar el estado del contenedor de eliminación de ruido de fondo (BNR) NVIDIA Broadcast desde AetherSDR. Use esta función para aplicar eliminación de ruido de fondo basada en inteligencia artificial al audio recibido o transmitido.

## Antes de comenzar

- Debe estar conectado a una radio FLEX-8600. La pestaña Audio no está disponible sin una conexión de radio activa.
- El contenedor NVIDIA BNR ya debe estar instalado en su sistema. AetherSDR controla el contenedor, pero no lo instala.

## Pasos

1. Abra `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que AetherSDR se conecte, haga clic en **Autostart Container**.
5. Para iniciar el contenedor de inmediato, haga clic en **Start**.
6. Para detener el contenedor, haga clic en **Stop**.
7. Para consultar el estado actual del contenedor, haga clic en **Check Status**.

## Qué hace cada control

| Control | Comportamiento |
|---|---|
| **Autostart Container** | Inicia el contenedor NVIDIA BNR automáticamente cuando AetherSDR se conecta a la radio. |
| **Start** | Inicia el contenedor de inmediato. |
| **Stop** | Detiene el contenedor de inmediato. |
| **Check Status** | Consulta el contenedor y actualiza el indicador de estado. |
| Indicador de estado NVIDIA BNR | Punto de color que muestra el estado actual del contenedor: Running, Stopped o Unknown. |

## Solución de problemas

- **El indicador de estado muestra Unknown después de hacer clic en Check Status** — Es posible que el entorno de ejecución del contenedor no sea accesible. Verifique que el entorno de ejecución de contenedores de NVIDIA esté instalado y que su usuario tenga permiso para administrar contenedores. Haga clic en **Check Status** nuevamente después de resolver cualquier problema de permisos.
- **Start no tiene efecto** — Confirme que la imagen del contenedor NVIDIA BNR esté presente en su sistema. AetherSDR no puede instalar el contenedor por sí mismo.

## Relacionado

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Elegir entre Opus y audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de destino](enable-auto-record-on-tx-and-pick-a-save-folder.md)
