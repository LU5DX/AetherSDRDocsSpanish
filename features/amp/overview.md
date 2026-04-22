# Descripción general del amplificador

El applet Amplifier proporciona telemetría en tiempo real y control OPERATE/STANDBY para un amplificador Power Genius XL (PGXL) conectado. Úselo para supervisar la potencia directa, el ROS, la temperatura, la corriente de drenaje y la tensión de red sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600.
- El radio debe detectar un amplificador Power Genius XL. El applet y su botón en la bandeja permanecen ocultos hasta que el radio reporte un PGXL.

## Cómo funciona

El applet Amplifier aparece en el panel de applets del lado derecho cuando AetherSDR detecta un amplificador PGXL en la red. Ábralo o ciérrelo con el botón **AMP** de la barra lateral derecha.

Toda la telemetría es enviada desde el radio en tiempo real. Los indicadores se actualizan a medida que el PGXL reporta nuevos valores; no se requiere sondeo ni actualización manual. El botón **OPERATE** / **STANDBY** refleja el estado actual del amplificador y permite alternar entre los dos.

## Qué hace cada control

| Control | Tipo | Comportamiento | Rango | Umbral rojo |
|---|---|---|---|---|
| **Fwd Pwr** | Indicador | Muestra la potencia de salida directa del PGXL. | 0–2000 W | > 1500 W |
| **SWR** | Indicador | Muestra el ROS en la salida del amplificador PGXL. | 1.0–3.0 | > 2.5 |
| **Temp** | Indicador | Muestra la temperatura del disipador del PGXL. | 0–100 °C | > 80 °C |
| **Volts / Amps** | Indicador de texto | Muestra la tensión de red y la corriente de drenaje como `Volts: xxxV  Amps: x.xA`. Permanece oculto hasta que llega la primera telemetría. | Voltios enteros, resolución de 0.1 A | — |
| **MEffA** | Indicador de texto | Muestra el valor MEffA del PGXL. Permanece oculto hasta que el radio reporte un valor. | — | — |
| **OPERATE** | Botón | Alterna el amplificador entre OPERATE y STANDBY. Permanece oculto hasta que el radio reporte el estado del amplificador. Muestra **OPERATE** (en verde) cuando el PGXL está en estado IDLE, OPERATE, TRANSMIT_A o TRANSMIT_B. Muestra **STANDBY** cuando el PGXL está en estado STANDBY, POWERUP o FAULT. | — | — |

Los tres indicadores utilizan una barra con código de colores: verde por debajo del umbral amarillo, amarillo-ámbar en la zona de precaución y rojo por encima del umbral rojo. Las etiquetas de escala en cada indicador tienen el color correspondiente a su zona.

Ninguno de los controles conserva configuraciones persistentes — todos los valores provienen en vivo del PGXL.

## Relacionados

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Supervisar la potencia directa y el ROS en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Monitorear la temperatura, la corriente de drenaje y la tensión de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
