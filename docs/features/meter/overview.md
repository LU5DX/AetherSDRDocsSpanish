# Descripción general de los medidores

El applet de medidores muestra telemetría de hardware en tiempo real del FLEX-8600 conectado: temperatura del amplificador de potencia (PA), tensión de alimentación de CC y velocidad del ventilador de refrigeración principal. Úselo para vigilar el estado térmico y eléctrico del radio durante la operación.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet no muestra datos sin una conexión de radio activa.
- El panel del applet debe estar visible. Si está oculto, actívelo con `View > Applet Panel`.

## Cómo funciona

El applet de medidores está oculto de forma predeterminada. Haga clic en el botón de bandeja **MTR** en la barra lateral derecha para mostrarlo u ocultarlo.

Una vez abierto, el applet muestra tres barras indicadoras horizontales bajo el encabezado de sección **Radio Hardware**. Cada barra se llena de izquierda a derecha y cambia de color a medida que la lectura asciende por las zonas normal, de precaución y de advertencia. La barra es cian en el rango normal, amarilla en la zona de precaución y roja cuando la lectura supera el umbral.

Los valores de las barras se suavizan con animación balística: la barra sigue los cambios rápidos con un breve movimiento de asentamiento en lugar de saltar instantáneamente. Esto reproduce la sensación de un medidor físico de aguja.

La temperatura del PA y la tensión de alimentación se entregan como telemetría en caché desde el radio. La velocidad del ventilador se resuelve por separado una vez que el radio informa su lista de medidores; la barra del ventilador puede mostrar cero brevemente al momento de la conexión hasta que esa consulta se complete.

La corriente del PA no se muestra. El hardware de la serie FLEX-8000 reporta la corriente del PA en una escala de 10 A, lo que se satura bajo la demanda máxima del PA y produce una lectura engañosa.

## Qué hace cada control

| Barra | Qué muestra | Rango normal | Rojo por encima de | Unidad |
|---|---|---|---|---|
| **PA Temp** | Temperatura del amplificador de potencia | 0–70 °C | 70 °C | °C |
| **+13.8V** | Tensión de alimentación de CC | 10.0–15.0 V | 15 V | V |
| **Main Fan** | Velocidad del ventilador de refrigeración principal | 0–2500 rpm | 2500 rpm | rpm |

Valores de fondo de escala: PA Temp 120 °C, +13.8V 16.0 V, Main Fan 3000 rpm.

Ninguna de las barras tiene configuraciones persistentes ni controles ajustables por el usuario. Son indicadores de solo lectura de los valores reportados por el radio.

## Consejos

- Observe **PA Temp** durante transmisiones prolongadas u operación en concursos. Una lectura consistentemente por encima de 70 °C justifica prestar atención a la ventilación alrededor del radio.
- Una lectura de **+13.8V** por encima de 15 V o por debajo de aproximadamente 12 V sugiere un problema de fuente de alimentación que conviene investigar antes de continuar la operación.
- Lecturas de **Main Fan** por encima de 2500 rpm indican que el radio está trabajando con alta carga térmica; verifique el flujo de aire y la temperatura ambiente.

## Relacionados

- [Vigilar la temperatura del PA durante transmisiones prolongadas](watch-pa-temperature-during-long-overs.md)
- [Verificar la tensión de alimentación de CC del radio](check-the-radio-s-dc-supply-voltage.md)
- [Monitorear la velocidad del ventilador de refrigeración principal](monitor-the-main-cooling-fan-speed.md)
