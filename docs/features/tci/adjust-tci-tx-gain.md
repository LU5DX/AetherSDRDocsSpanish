# Ajustar la ganancia de TX de TCI

Configure la ganancia de salida que el servidor TCI aplica al flujo de audio de transmisión antes de enviarlo a los clientes conectados (Log4OM, herramientas SunSDR y similares).

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet TCI requiere una conexión de radio activa.
- El servidor TCI debe ser visible. Si el panel del applet no muestra la sección TCI, haga clic en el botón de bandeja **TCI** en la barra lateral derecha para mostrarla.

## Pasos

1. Haga clic en el botón de bandeja **TCI** en la barra lateral derecha para abrir el applet del servidor TCI.
2. Localice la fila **TX:**. El indicador de slice a la derecha de la etiqueta muestra qué slice impulsa actualmente el canal TX (por ejemplo, `Slice A`), o `—` si no hay ningún slice TX asignado.
3. Arrastre el control deslizante **TX gain+meter** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es `0.0` a `1.0`; el valor predeterminado es `0.5`.
4. Suelte el control deslizante. El nuevo valor se guarda inmediatamente en `TciTxGain` y se aplica en el servidor en ejecución.

## Qué hace cada control

| Control       | Valor predeterminado                              | Rango válido                                                                                                                                                                                                                                                                                             |
|---------------|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TX gain+meter | Los arrastres establecen la ganancia TX de TCI y emiten tciTxGainChanged. | TciServer::setTxGain persiste TciTxGain internamente; la IU refleja el valor almacenado. El audio TX de TCI siempre está permitido independientemente de la plataforma o la disponibilidad de DAX alojado (evaluateDaxTxPolicy ahora permite incondicionalmente DaxTxRequestReason::TciTxAudio, v0.9.5.1, #2276). |

**TX gain+meter** es un medidor y control deslizante combinados. La porción del medidor refleja el nivel de audio TX en vivo del slice TX activo. La posición del control deslizante establece la ganancia aplicada a ese audio antes de enviarlo a los clientes TCI.

La etiqueta del slice junto a **TX:** (por ejemplo, `Slice A` o `—`) es de solo lectura. Muestra qué slice está asignado actualmente como slice TX y se actualiza automáticamente cuando cambia el slice TX. A partir de la versión v26.5.2.1, la etiqueta del slice usa formato de texto enriquecido para que las letras de slice renderizadas como HTML se muestren correctamente (#2606).

## Consejos

- Si no aparece ninguna etiqueta de slice junto a **TX:** (muestra `—`), no hay ningún slice TX asignado. Asigne un slice TX en la radio antes de ajustar la ganancia TX.
- El valor de ganancia persiste entre reinicios. AetherSDR lee `TciTxGain` al iniciar y establece el control deslizante en el valor almacenado.

## Relacionados

- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Descripción general del servidor TCI](overview.md)
