# Ajustar la ganancia TX de TCI

Esta página explica cómo configurar la ganancia TX de TCI en el applet TCI Server. Ajustar este valor controla el nivel de audio enviado a los clientes TCI conectados para el canal de transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TCI requiere una conexión activa con el radio.
- El applet TCI Server debe estar visible. Si no lo está, haga clic en el botón TCI del área de notificación en la barra lateral derecha para mostrarlo.

## Pasos

1. Haga clic en el botón TCI del área de notificación en la barra lateral derecha para abrir el applet TCI Server.
2. Localice la fila etiquetada como **TX:** en el applet. El indicador de slice a su derecha muestra qué slice (canal de recepción/transmisión) controla actualmente el canal TX (por ejemplo, `Slice A`), o `—` si no hay ninguno asignado.
3. Arrastre el control deslizante **TX gain+meter** hacia la izquierda o la derecha para disminuir o aumentar la ganancia TX. El control deslizante también funciona como medidor de nivel en tiempo real, mostrando la actividad de audio de transmisión mientras opera.
4. Suelte el control deslizante. El nuevo valor se guarda automáticamente en `TciTxGain` y surte efecto de inmediato para todos los clientes TCI conectados.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango válido | Clave de configuración |
|---|---|---|---|---|
| TX gain+meter | Medidor y control deslizante combinados. Arrastre para establecer el nivel de ganancia TX de TCI. La parte del medidor refleja el audio de transmisión en tiempo real. | 0.5 | 0.0–1.0 | `TciTxGain` |
| Etiqueta de asignación de slice RX/TX | Indicador que muestra qué slice controla la fila TX. Solo lectura. | `—` | `—` o `Slice <letra>` | — |

## Consejos

- El **TX gain+meter** muestra la actividad de audio en tiempo real durante la transmisión. Si el medidor no se mueve durante la transmisión, confirme que el slice correcto esté asignado como slice TX; la etiqueta junto a **TX:** mostrará `—` si no hay ningún slice TX asignado.
- El valor de ganancia TX se conserva entre reinicios. No es necesario volver a ingresarlo en cada sesión.

## Solución de problemas

- **La etiqueta TX gain+meter muestra `—` en lugar del nombre de un slice** — Actualmente no hay ningún slice configurado como slice TX en el radio. Asigne un slice TX en los controles de slice del radio y luego regrese al applet TCI; la etiqueta se actualiza automáticamente.
- **Arrastrar el control deslizante no tiene efecto audible en el cliente TCI** — Confirme que el servidor TCI esté en ejecución (la línea de estado debe mostrar `:<port> (N clients)`, no `(stopped)`). Haga clic en Enable si el servidor no está en ejecución.

## Relacionados

- [Descripción general de TCI Server](overview.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
