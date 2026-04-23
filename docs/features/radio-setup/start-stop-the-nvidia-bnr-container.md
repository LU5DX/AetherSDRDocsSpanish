# Iniciar/detener el contenedor NVIDIA BNR

Esta página explica cómo iniciar, detener y verificar el estado del contenedor NVIDIA Broadcast Noise Removal (BNR) desde AetherSDR. Use esta función para aplicar eliminación de ruido acelerada por GPU al audio recibido o transmitido.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. La pestaña Audio no está disponible sin una conexión activa al radio.
- El contenedor NVIDIA BNR debe estar instalado en su sistema de forma independiente. AetherSDR controla el contenedor, pero no lo instala.
- Abra la configuración del radio: `Settings > Radio Setup...`, luego haga clic en la pestaña **Audio**.

## Pasos

1. Vaya a `Settings > Radio Setup...`.
2. Haga clic en la pestaña **Audio**.
3. Localice la sección **NVIDIA BNR** cerca de la parte inferior de la pestaña.
4. Para que el contenedor se inicie automáticamente cada vez que AetherSDR se conecte al radio, haga clic en **Autostart Container**.
5. Para iniciar el contenedor de inmediato, haga clic en **Start**.
6. Para detener un contenedor en ejecución, haga clic en **Stop**.
7. Para consultar el estado actual del contenedor sin modificarlo, haga clic en **Check Status**.
8. Observe el indicador de estado de color junto a los controles de NVIDIA BNR para confirmar el resultado: el indicador muestra Running, Stopped o Unknown.

## Qué hace cada control

| Control | Tipo | Comportamiento |
|---|---|---|
| **Autostart Container** | Botón | Activa o desactiva el inicio automático del contenedor cada vez que AetherSDR se conecta al radio. |
| **Start** | Botón | Inicia el contenedor NVIDIA BNR de inmediato. |
| **Stop** | Botón | Detiene el contenedor NVIDIA BNR en ejecución de inmediato. |
| **Check Status** | Botón | Consulta el estado del contenedor y actualiza el indicador de estado sin modificar el contenedor. |
| Indicador de estado NVIDIA BNR | Indicador | Punto de color que muestra el estado del contenedor: Running, Stopped o Unknown. |

## Consejos

- Use **Check Status** después de hacer clic en **Start** o **Stop** si el indicador de estado no se actualiza de inmediato. Es posible que el contenedor tarde un momento en cambiar de estado.
- **Autostart Container** es útil para operación remota o desatendida cuando desea tener la eliminación de ruido activa sin pasos manuales en cada sesión.

## Solución de problemas

- **El indicador de estado muestra Unknown después de hacer clic en Start** — Es posible que el contenedor no esté instalado o no sea accesible. Verifique que el contenedor NVIDIA BNR esté instalado y que su sistema cumpla los requisitos de GPU; luego haga clic en **Check Status** nuevamente.
- **Stop no tiene efecto** — Es posible que el contenedor haya sido iniciado fuera de AetherSDR. Deténgalo desde el nivel del sistema y luego haga clic en **Check Status** para confirmar.

## Relacionados

- [Elegir dispositivos de audio de entrada/salida del PC](choose-pc-input-output-audio-devices.md)
- [Seleccionar Opus o audio sin comprimir para SmartLink](pick-opus-vs-uncompressed-audio-for-smartlink.md)
- [Activar el aumento de audio o ampliar el búfer de audio para operación remota](turn-on-audio-boost-or-enlarge-the-audio-buffer-for-remote-operation.md)
- [Habilitar la grabación automática en TX y seleccionar una carpeta de guardado](enable-auto-record-on-tx-and-pick-a-save-folder.md)
