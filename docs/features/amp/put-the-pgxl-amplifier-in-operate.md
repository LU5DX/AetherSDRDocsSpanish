# Poner el amplificador PGXL en OPERATE

Esta página explica cómo cambiar un amplificador Power Genius XL conectado de STANDBY a OPERATE mediante el applet Amplifier de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet Amplifier permanece oculto hasta que el radio detecte un Power Genius XL.
- El PGXL debe estar encendido y comunicándose con el radio Flex para que haya llegado la telemetría de estado. El botón OPERATE permanece oculto hasta que se recibe la primera actualización de estado.

## Pasos

1. Localice el botón de bandeja AMP en la barra lateral derecha del panel de applets.
2. Haga clic en AMP para abrir el applet Amplifier.
3. Confirme que el botón del applet muestra "STANDBY". Esto indica que el PGXL se encuentra actualmente en espera.
4. Haga clic en STANDBY. La etiqueta del botón cambia a "OPERATE" y se vuelve verde, lo que indica que el amplificador está ahora en OPERATE.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| OPERATE | Cuando el botón muestra "OPERATE" (verde), el PGXL se encuentra en estado IDLE, OPERATE o TRANSMIT. Haga clic en él para enviar el amplificador a STANDBY. | Oculto hasta que llegue la primera actualización de estado desde el radio. |
| STANDBY | Cuando el botón muestra "STANDBY" (estilo predeterminado), el PGXL se encuentra en STANDBY, POWERUP o FAULT. Haga clic en él para enviar el amplificador a OPERATE. | Es el mismo botón; la etiqueta y el color cambian según el estado. |
| Fwd Pwr | Indicador de barra horizontal que muestra la potencia de salida directa. Rango: 0–2000 W. La barra se vuelve roja por encima de 1500 W. | |
| SWR | Indicador de barra horizontal que muestra la ROS. Rango: 1.0–3.0. La barra se vuelve roja por encima de 2.5. | |
| Temp | Indicador de barra horizontal que muestra la temperatura del disipador térmico. Rango: 0–100 °C. La barra se vuelve roja por encima de 80 °C. | |

## Consejos

- Si el panel de applets no es visible, vaya a `View > Applet Panel` para mostrarlo.
- El botón OPERATE refleja el estado reportado por el PGXL, no un interruptor rastreado localmente. Si el amplificador entra en FAULT o POWERUP, el botón vuelve a "STANDBY" automáticamente.

## Resolución de problemas

- **El botón de bandeja AMP no aparece** — El radio no ha detectado ningún Power Genius XL. Confirme que el PGXL está encendido y correctamente conectado al radio Flex.
- **El botón OPERATE no es visible dentro del applet** — El applet se ha abierto, pero aún no ha llegado ninguna telemetría de estado desde el PGXL. Espere un momento; el botón aparece tras la primera actualización de estado.
- **El botón muestra "STANDBY" inmediatamente después de hacer clic** — Es posible que el PGXL esté en FAULT o POWERUP y no pueda entrar en OPERATE. Revise el panel frontal del amplificador para verificar si hay indicadores de fallo.

## Relacionados

- [Descripción general del amplificador](overview.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Monitorear la potencia directa y la ROS en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Observar la temperatura, la corriente de drenaje y el voltaje de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
