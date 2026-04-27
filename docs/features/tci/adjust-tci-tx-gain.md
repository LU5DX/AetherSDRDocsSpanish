# Ajustar la ganancia TX de TCI

Configure la ganancia de salida que el servidor TCI aplica al flujo de audio de transmisión antes de enviarlo a los clientes conectados (Log4OM, herramientas SunSDR y similares).

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet de TCI requiere una conexión de radio activa.
- El servidor TCI debe ser visible. Si el panel de applets no muestra la sección TCI, haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para mostrarla.

## Pasos

1. Haga clic en el botón **TCI** de la bandeja en la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila **TX:**. El indicador de slice a la derecha de la etiqueta muestra qué slice controla actualmente el canal TX (por ejemplo, `Slice A`), o `—` si no hay ningún slice TX asignado.
3. Arrastre el control deslizante **TX gain+meter** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es de `0.0` a `1.0`; el valor predeterminado es `0.5`.
4. Suelte el control deslizante. El nuevo valor se guarda inmediatamente en `TciTxGain` y surte efecto en el servidor en ejecución.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| TX gain+meter | 0.5 | 0.0–1.0 | `TciTxGain` |

El control **TX gain+meter** es un medidor y control deslizante combinados. La parte del medidor refleja el nivel de audio TX en tiempo real del slice TX activo. La posición del control deslizante establece la ganancia aplicada a ese audio antes de enviarlo a los clientes TCI.

La etiqueta de slice junto a **TX:** (por ejemplo, `Slice A` o `—`) es de solo lectura. Muestra qué slice está asignado actualmente como slice TX y se actualiza automáticamente cuando cambia el slice TX.

## Consejos

- Si no aparece ninguna etiqueta de slice junto a **TX:** (muestra `—`), no hay ningún slice TX asignado. Asigne un slice TX en el radio antes de ajustar la ganancia TX.
- El valor de ganancia persiste entre reinicios. AetherSDR lee `TciTxGain` al iniciar y establece el control deslizante en el valor almacenado.

## Relacionados

- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Descripción general del servidor TCI](overview.md)
