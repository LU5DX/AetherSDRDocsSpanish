# Confirmar si la telemétrica del PGXL es directa o mediante el proxy de la radio

Esta página le ayuda a determinar si AetherSDR lee la telemétrica del Power Genius XL (PGXL) directamente del amplificador o a través del proxy del radio FLEX-8600, y explica qué datos están disponibles en cada modo.

## Antes de comenzar

- Un amplificador Power Genius XL debe estar conectado y detectado por AetherSDR.
- El applet del Amplificador debe estar visible. Si no lo está, actívelo con el botón **AMP** de la barra lateral derecha.

## Pasos

1. Abra el applet del Amplificador haciendo clic en el botón **AMP** de la barra lateral derecha.
2. Observe la **etiqueta de fuente** en la parte inferior izquierda del applet.
   - **● RADIO** — la telemétrica se está recibiendo mediante el proxy del radio FLEX-8600.
   - **● DIRECT** — la telemétrica se está leyendo directamente del PGXL.

## Qué hace cada control

| Control | Comportamiento | Notas |
|---|---|---|
| **Etiqueta de fuente** | Muestra **● RADIO** o **● DIRECT** para indicar la ruta de la telemétrica. | Vdd, Vac y el modo de ventilador solo están disponibles en la ruta DIRECT. |
| **Vdd (tensión de drenaje)** | Muestra la tensión de drenaje como `Vdd  x.x V`. | Solo se actualiza con una conexión directa. Muestra un guion (`—`) cuando la fuente de drenaje está apagada (vdd < 1 V) o cuando la conexión es mediante el proxy del radio. Se atenúa en modo proxy. |
| **Vac (tensión de red)** | Muestra la tensión de red como `Vac  N V`. | Solo se actualiza con una conexión directa. Se atenúa cuando se recibe mediante el proxy del radio. |
| **Velocidad del ventilador** | Lista desplegable con opciones **STANDARD**, **CONTEST** y **BROADCAST**. | Se oculta hasta que una conexión directa del PGXL entregue el primer estado de modo de ventilador. |

## Consejos

- Cuando la **etiqueta de fuente** muestra **● RADIO**, la ausencia de los controles Vdd/Vac/modo de ventilador es un comportamiento esperado, no una falla. Esos valores solo están disponibles con una conexión directa.

## Relacionado

- [Información general del amplificador](overview.md)
- [Monitorear la potencia directa y la ROE a la salida del amplificador](monitor-forward-power-and-swr-at-the-amplifier-output.md)
- [Vigilar la temperatura, la corriente de drenaje y la tensión de red del PGXL](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Seleccionar la velocidad del ventilador del PGXL (Standard, Contest, Broadcast)](select-the-pgxl-fan-speed-standard-contest-broadcast.md)
