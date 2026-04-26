# Ajustar la ganancia de TX en TCI

Use esta página para configurar la ganancia aplicada al flujo de audio de transmisión que el servidor TCI de AetherSDR envía a los clientes conectados. Ajustar la ganancia de TX permite igualar el nivel de señal esperado por su software de modos digitales o de registro sin modificar los ajustes principales de TX del radio.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet de TCI requiere una conexión activa con el radio.
- El servidor TCI debe estar en ejecución (Enable activado). El control deslizante de ganancia de TX está presente en todo momento, pero no tiene efecto sobre el audio hasta que el servidor esté activo y haya un cliente conectado.

## Pasos

1. Haga clic en el botón **TCI** del panel lateral derecho para abrir el applet TCI Server.
2. Localice la fila **TX:**. El indicador de asignación de slice a la derecha de la etiqueta muestra qué slice está controlando actualmente la TX (por ejemplo, `Slice A`), o `—` si no hay ningún slice de TX asignado.
3. Arrastre el control deslizante **TX gain+meter** hacia la izquierda para reducir la ganancia o hacia la derecha para aumentarla. El rango válido es de `0.0` a `1.0`; el valor predeterminado es `0.5`.
4. Suelte el control deslizante. AetherSDR guarda el nuevo valor de inmediato en `TciTxGain`.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango | Clave persistida |
|---|---|---|---|---|
| TX gain+meter | Medidor de nivel y control deslizante de ganancia combinados para el canal TX de TCI. Arrastre para ajustar la ganancia; el medidor muestra el nivel de audio TX en tiempo real. | `0.5` | `0.0`–`1.0` | `TciTxGain` |
| Indicador de slice TX | Etiqueta de solo lectura que muestra qué slice controla la TX (`Slice A`, `Slice B`, etc.) o `—` si ninguno. | `—` | `—` o `Slice <letter>` | — |

## Consejos

- El medidor muestra el nivel suavizado en tiempo real del audio TX que llega al servidor TCI. Úselo para confirmar que el audio está fluyendo antes de ajustar la ganancia.
- La posición del control deslizante se restaura desde `TciTxGain` cada vez que AetherSDR se inicia, por lo que su configuración persiste entre sesiones.

## Solución de problemas

- **El indicador de slice TX muestra `—`** — Ningún slice tiene TX asignado en el radio. Asigne un slice de TX en los controles de slice de su radio; la etiqueta se actualiza automáticamente.
- **Arrastrar el control deslizante no tiene efecto audible en el cliente** — Confirme que el servidor TCI está en ejecución (el estado del servidor muestra `:<port> (N clients)`, no `(stopped)`). Si el estado muestra `(port in use)`, consulte [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md).

## Relacionados

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
- [Inicio automático de TCI al lanzar la aplicación](autostart-tci-on-launch.md)
