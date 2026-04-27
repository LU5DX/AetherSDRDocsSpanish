# Descripción general de los medidores

El applet Meters muestra telemetría de hardware en tiempo real desde el FLEX-8600 conectado: temperatura del amplificador de potencia (PA), tensión de alimentación de CC y velocidad del ventilador principal de refrigeración. Utilícelo para supervisar el estado del radio durante la operación sin salir de la ventana principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet requiere una conexión de radio activa.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Cómo funciona

El applet Meters está oculto de forma predeterminada. Ábralo o ciérrelo alternadamente usando el botón de bandeja **MTR** en la barra lateral derecha.

Una vez abierto, el applet muestra una sección "Radio Hardware" que contiene tres barras indicadoras horizontales. Cada barra se llena de izquierda a derecha y cambia de color a medida que el valor avanza por las zonas de advertencia y alarma:

- La barra es de color **verde** por debajo del umbral amarillo.
- La barra se vuelve **amarillo-ámbar** entre los umbrales amarillo y rojo.
- La barra se vuelve **roja** por encima del umbral rojo.

Las etiquetas de escala a lo largo de la parte superior de cada barra están coloreadas para coincidir con la zona en la que se encuentran. Los valores se suavizan con animación balística para que los cambios rápidos no provoquen saltos bruscos.

La temperatura del PA y la tensión de alimentación se reportan directamente desde el flujo de telemetría de hardware del radio. La velocidad del ventilador principal se resuelve por nombre de medidor cuando el radio la publica por primera vez y se actualiza a medida que llegan las lecturas.

## Qué hace cada control

| Indicador | Qué muestra | Rango válido | Rojo por encima de |
|---|---|---|---|
| **PA Temp** | Temperatura del amplificador de potencia | 0–120 °C | 70 °C |
| **+13.8V** | Tensión de alimentación de CC | 10.0–16.0 V | 15 V |
| **Main Fan** | Velocidad del ventilador principal de refrigeración | 0–3000 rpm | 2500 rpm |

Ninguno de los indicadores tiene configuraciones persistentes ni controles ajustables por el usuario. No hay claves de `AppSettings` asociadas a este applet.

**Nota:** La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA tiene un límite de 10 A, lo que provoca que la lectura se sature bajo una extracción completa del PA, haciéndola poco confiable.

## Consejos

- Una lectura de PA Temp que regularmente alcanza la zona roja (por encima de 70 °C) durante transmisiones prolongadas puede indicar una ventilación insuficiente alrededor del radio.
- El umbral rojo del indicador +13.8V es 15 V. Las lecturas consistentemente por encima de ese valor sugieren un problema de regulación de la fuente de alimentación que vale la pena investigar.
- La velocidad de Main Fan mostrará cero hasta que el radio publique el medidor MAINFAN. Esto es normal durante los primeros segundos tras la conexión.

## Relacionados

- [Supervisar la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Verificar la tensión de alimentación de CC del radio](check-the-radio-s-dc-supply-voltage.md)
- [Monitorear la velocidad del ventilador principal de refrigeración](monitor-the-main-cooling-fan-speed.md)
