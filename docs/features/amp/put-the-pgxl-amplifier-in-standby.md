# Poner el amplificador PGXL en STANDBY

Use esta página para pasar un amplificador Power Genius XL conectado del modo OPERATE al modo STANDBY, impidiendo que amplíe las señales transmitidas.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El botón AMP del área de notificación aparece únicamente después de que se detecta un Power Genius XL.
- El applet Amplifier debe estar abierto. Si no está visible, haga clic en el botón AMP del área de notificación en la barra lateral derecha para mostrarlo.
- El botón OPERATE permanece oculto hasta que llega el primer mensaje de estado del amplificador. Confirme que esté visible antes de continuar.

## Pasos

1. Abra el applet Amplifier haciendo clic en el botón AMP del área de notificación en la barra lateral derecha, si aún no está visible.
2. Confirme que el botón OPERATE muestre la etiqueta "OPERATE" en verde. Esto indica que el amplificador se encuentra actualmente en un estado de operación (IDLE, OPERATE o TRANSMIT).
3. Haga clic en OPERATE.

La etiqueta del botón cambia a "STANDBY" y el fondo verde es reemplazado por el estilo oscuro predeterminado, confirmando que el amplificador ha pasado al modo STANDBY.

## Qué hace cada control

| Control | Comportamiento | Estados |
|---|---|---|
| OPERATE | Alterna el amplificador entre OPERATE y STANDBY. | Muestra "OPERATE" (verde) cuando el estado del amplificador es IDLE, OPERATE o TRANSMIT_A/TRANSMIT_B. Muestra "STANDBY" (estilo oscuro predeterminado) cuando el estado es STANDBY, POWERUP o FAULT. |

## Solución de problemas

- **El botón AMP del área de notificación no está visible** — El applet permanece oculto hasta que la radio detecta un Power Genius XL. Confirme que el PGXL esté encendido y conectado al radio Flex.
- **El botón OPERATE no está visible** — El botón permanece oculto hasta que llega el primer mensaje de estado del amplificador. Espere un momento después de que el applet se abra; si no aparece, verifique la conexión del amplificador.
- **Hacer clic en OPERATE no tiene efecto** — Confirme que AetherSDR siga conectado a la radio. Desconecte y vuelva a conectar si es necesario.

## Relacionados

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Monitorear la potencia directa y el ROS en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Supervisar la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Descripción general del amplificador](overview.md)
