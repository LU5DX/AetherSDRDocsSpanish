# Descripción general de medidores

El applet de medidores (Meters) muestra telemetría de hardware en tiempo real del FLEX-8600 conectado: temperatura del amplificador de potencia (PA), tensión de alimentación DC y velocidad del ventilador principal. Úselo para supervisar el estado del equipo durante la operación sin salir de la ventana principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet requiere una conexión de radio activa.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Cómo funciona

El applet de medidores está oculto por defecto. Ábralo o ciérrelo con el botón de bandeja **MTR** en la barra lateral derecha.

Una vez abierto, el applet muestra una sección "Radio Hardware" que contiene tres barras de progreso horizontales. Cada barra se llena de izquierda a derecha y cambia de color a medida que el valor sube a través de zonas de advertencia y alarma:

- La barra es **verde** por debajo del umbral amarillo.
- La barra se vuelve **amarillo-ámbar** entre los umbrales amarillo y rojo.
- La barra se vuelve **roja** por encima del umbral rojo.

Las etiquetas de escala en la parte superior de cada barra están coloreadas para coincidir con la zona en que se encuentran. Los valores se suavizan con animación balística para que los cambios rápidos no produzcan saltos bruscos.

La temperatura del PA y la tensión de alimentación se obtienen directamente del flujo de telemetría de hardware del radio. La velocidad del ventilador principal se resuelve por nombre de medidor cuando el radio lo publica por primera vez y se actualiza a medida que llegan las lecturas.

## Qué hace cada control

| Indicador | Qué muestra | Rango válido | Rojo por encima de |
|---|---|---|---|
| **PA Temp** | Temperatura del amplificador de potencia | 0–120 °C | 70 °C |
| **+13.8V** | Tensión de alimentación DC | 10.0–16.0 V | 15 V |
| **Main Fan** | Velocidad del ventilador principal | 0–3000 rpm | 2500 rpm |

Ninguna de las barras tiene configuraciones persistentes ni controles ajustables por el usuario. No hay claves de `AppSettings` asociadas a este applet.

**Nota:** La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA tiene un límite máximo de 10 A, lo que provoca que la lectura se recorte bajo una carga total del PA y la hace poco confiable.

## Consejos

- Una lectura de PA Temp que alcanza regularmente la zona roja (por encima de 70 °C) durante transmisiones prolongadas puede indicar ventilación insuficiente alrededor del radio.
- El umbral rojo del indicador +13.8V es 15 V. Lecturas consistentemente por encima de ese valor sugieren un problema de regulación de la fuente de alimentación que vale la pena investigar.
- La velocidad del Main Fan mostrará cero hasta que el radio publique el medidor MAINFAN. Esto es normal durante los primeros segundos después de conectar.

## Relacionados

- [Supervisar la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Verificar la tensión de alimentación DC del radio](check-the-radio-s-dc-supply-voltage.md)
- [Monitorear la velocidad del ventilador principal](monitor-the-main-cooling-fan-speed.md)
