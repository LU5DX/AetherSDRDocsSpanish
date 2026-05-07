# Resumen del amplificador

El applet Amplificador proporciona telemetría en tiempo real y control OPERATE/STANDBY para un amplificador Power Genius XL (PGXL) conectado. Úselo para monitorear la potencia directa, la ROE, la temperatura, la corriente de drenaje y el voltaje de la red eléctrica sin salir de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio Flex.
- La radio debe detectar un amplificador Power Genius XL. El applet y su botón de bandeja permanecen ocultos hasta que la radio reporta un PGXL.

## Cómo funciona

El applet Amplificador aparece en el panel de applets del lado derecho cuando AetherSDR detecta un amplificador PGXL en la red. Ábralo o ciérrelo con el botón de bandeja **AMP** en la barra lateral derecha.

Toda la telemetría se envía desde la radio en tiempo real. Los indicadores se actualizan a medida que el PGXL reporta nuevos valores; no es necesario sondeo ni actualización manual. El botón **OPERATE** / **STANDBY** refleja el estado actual del amplificador y le permite alternar entre ambos.

## Función de cada control

| Control          | Tipo             | Comportamiento                                                                                                                                                                                                                                                                                   |
|------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Fwd Pwr**      | Indicador        | Muestra la potencia de salida directa del PGXL.                                                                                                                                                                                                                                                  |
| **SWR**          | Indicador        | Muestra la ROE en la salida del amplificador PGXL.                                                                                                                                                                                                                                               |
| **Temp**         | Indicador        | Muestra la temperatura del disipador del PGXL.                                                                                                                                                                                                                                                   |
| **Volts / Amps** | Indicador textual | Muestra el voltaje de la red eléctrica y la corriente de drenaje como `Volts: xxxV  Amps: x.xA`. Oculto hasta que llega la primera telemetría.                                                                                                                                                   |
| **MEffA**        | Indicador textual | Muestra el valor MEffA del PGXL. Oculto hasta que la radio reporta un valor.                                                                                                                                                                                                                     |
| **OPERATE**      | Botón            | Alterna el amplificador entre OPERATE y STANDBY. Oculto hasta que la radio reporta el estado del amplificador. Muestra **OPERATE** (verde) cuando el PGXL está en estado IDLE, OPERATE, TRANSMIT_A o TRANSMIT_B. Muestra **STANDBY** cuando el PGXL está en estado STANDBY, POWERUP o FAULT. |

Los tres indicadores utilizan una barra codificada por colores: verde por debajo del umbral amarillo, amarillo-ámbar en la zona de precaución y rojo por encima del umbral rojo. Las etiquetas de marcas en cada indicador tienen el color correspondiente a su zona.

Ninguno de los controles tiene configuraciones persistentes; todos los valores provienen en vivo del PGXL.

## Relacionado

- [Poner el amplificador PGXL en OPERATE](put-the-pgxl-amplifier-in-operate.md)
- [Poner el amplificador PGXL en STANDBY](put-the-pgxl-amplifier-in-standby.md)
- [Monitorear la potencia directa y la ROE en la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Observar la temperatura del PGXL, la corriente de drenaje y el voltaje de la red eléctrica](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
