# Resumen de Medidores

El applet de Medidores muestra telemetría de hardware en tiempo real desde la FLEX-8600 conectada: temperatura del PA, tensión de alimentación de CC y velocidad del ventilador de refrigeración principal. Úselo para supervisar el estado de la radio durante la operación sin salir de la ventana principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Cómo funciona

El applet de Medidores está oculto por defecto. Ábralo o ciérrelo usando el botón **MTR** en la barra lateral derecha.

Una vez abierto, el applet muestra una sección "Radio Hardware" que contiene tres barras de medición horizontales. Cada barra se llena de izquierda a derecha y cambia de color a medida que el valor sube a través de las zonas de advertencia y alarma:

- La barra es **verde** por debajo del umbral amarillo.
- La barra se vuelve **amarillo-ámbar** entre los umbrales amarillo y rojo.
- La barra se vuelve **roja** por encima del umbral rojo.

Las etiquetas de las marcas a lo largo de la parte superior de cada barra están coloreadas para coincidir con la zona en la que se encuentran. Los valores se suavizan con animación balística para que los cambios rápidos no causen saltos bruscos.

La temperatura del PA y la tensión de alimentación se reportan directamente desde el flujo de telemetría del hardware de la radio. La velocidad del ventilador principal se resuelve por el nombre del medidor cuando la radio lo publica por primera vez y se actualiza a medida que llegan las lecturas.

El applet ahora aplica el tema activo de la aplicación al contenedor de medidores usando el administrador de temas. Esto asegura que el área de medidores coincida con la apariencia de otros applets en el tema actual.

## Qué hace cada control

| Medidor       | Qué muestra                     | Rango válido |
|---------------|---------------------------------|--------------|
| **PA Temp**   | Temperatura del amplificador de potencia | 0–120 °C     |
| **+13.8V**    | Tensión de alimentación de CC   | 10.0–16.0 V  |
| **Main Fan**  | Velocidad del ventilador de refrigeración principal | 0–3000 rpm   |

Ninguno de los medidores tiene ajustes persistentes ni controles ajustables por el usuario. No hay claves de `AppSettings` asociadas con este applet.

La etiqueta del medidor **+13.8V** se actualiza dinámicamente para reflejar el valor de tensión en vivo reportado por la radio. Por ejemplo, cuando la radio reporta 13.82 V, la etiqueta del medidor muestra **+13.82V**. Antes de la v26.6.1, la etiqueta siempre mostraba el texto estático **+13.8V** independientemente de la lectura real.

**Nota:** La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA está limitado a 10 A, lo que provoca que la lectura se sature bajo la máxima demanda del PA, haciéndolo poco fiable.

## Consejos

- Una lectura de temperatura del PA que alcance regularmente la zona roja (por encima de 70 °C) durante transmisiones largas puede indicar una ventilación inadecuada alrededor de la radio.
- El umbral rojo del medidor de tensión es 15 V. Lecturas consistentemente por encima de ese valor sugieren un problema de regulación de la fuente de alimentación que vale la pena investigar.
- La velocidad del ventilador principal mostrará cero hasta que la radio publique el medidor MAINFAN. Esto es normal durante los primeros segundos después de la conexión.

## Relacionado

- [Watch PA temperature during long overs](watch-pa-temperature-during-long-overs.md)
- [Check the radio's DC supply voltage](check-the-radio-s-dc-supply-voltage.md)
- [Monitor the main cooling fan speed](monitor-the-main-cooling-fan-speed.md)
