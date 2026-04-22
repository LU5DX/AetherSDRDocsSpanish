# Ajustar la ganancia TX de TCI

Esta página explica cómo configurar la ganancia TX de TCI en el applet TCI Server. Ajustar este valor controla el nivel de audio enviado a los clientes TCI conectados para el canal de transmisión.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet de TCI requiere una conexión de radio activa.
- El applet TCI Server debe estar visible. Si no lo ve, haga clic en el botón TCI del panel lateral derecho para mostrarlo.

## Pasos

1. Haga clic en el botón TCI del panel lateral derecho para abrir el applet TCI Server.
2. Localice la fila etiquetada como **TX:** cerca de la parte inferior del applet, encima de la fila Port.
3. Arrastre el control deslizante TX gain+meter hacia la izquierda para disminuir la ganancia o hacia la derecha para aumentarla. El rango válido es de 0.0 a 1.0. El valor predeterminado es 0.5.
4. Suelte el control deslizante. AetherSDR guarda el nuevo valor en `TciTxGain` de inmediato.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| TX gain+meter | 0.5 | 0.0–1.0 | `TciTxGain` | Arrastre para establecer la ganancia TX de TCI. El medidor refleja el nivel de audio de transmisión en tiempo real. La posición del control deslizante refleja el valor de ganancia almacenado. |
| Indicador de slice TX | — | — o `Slice <letter>` | — | Muestra qué slice es actualmente el slice TX. Se actualiza automáticamente cuando cambia el slice TX. |

## Consejos

- El TX gain+meter funciona también como medidor de nivel en tiempo real. La visualización del medidor utiliza suavizado exponencial con un ataque rápido y una caída más lenta, por lo que los picos breves aparecen rápidamente pero descienden de forma gradual.
- El indicador de slice junto al medidor TX muestra qué slice impulsa el canal TX. Si muestra `—`, ningún slice está asignado actualmente como slice TX.
- `TciTxGain` es persistido por el servidor TCI. El control deslizante lee este valor almacenado al iniciar, de modo que la visualización coincide con el estado del servidor.

## Solución de problemas

- **El medidor TX no muestra movimiento durante la transmisión** — Confirme que el servidor TCI está en ejecución (la línea de estado muestra `:<port> (N clients)` en lugar de `(stopped)`). Confirme también que el indicador de slice TX muestra una letra de slice en lugar de `—`.
- **El control deslizante vuelve a 0.5 después de reiniciar AetherSDR** — Esto indica que `TciTxGain` no fue guardado. Asegúrese de que AetherSDR tenía permisos de escritura suficientes en su almacenamiento de configuración al momento de realizar el cambio.

## Relacionado

- [Habilitar el servidor TCI para clientes Log4OM / SunSDR](enable-the-tci-server-for-log4om-sunsdr-clients.md)
- [Ajustar la ganancia RX de TCI por canal](adjust-tci-rx-gain-per-channel.md)
- [Cambiar el puerto TCI](change-the-tci-port.md)
