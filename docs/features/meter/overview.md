# Resumen de medidores

El applet Medidores muestra la telemetría de hardware en tiempo real desde la FLEX-8600 conectada: temperatura del PA, tensión de alimentación CC y velocidad del ventilador de refrigeración principal. Úselo para supervisar el estado del equipo durante la operación sin salir de la ventana principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Cómo funciona

El applet Medidores está oculto por defecto. Ábralo o ciérrelo usando el botón de bandeja **MTR** en la barra lateral derecha.

Una vez abierto, el applet muestra una sección "Radio Hardware" que contiene tres barras de medidor horizontales. Cada barra se llena de izquierda a derecha y cambia de color a medida que el valor asciende a través de zonas de advertencia y alarma:

- La barra es **verde** por debajo del umbral amarillo.
- La barra se vuelve **amarillo-ámbar** entre los umbrales amarillo y rojo.
- La barra se vuelve **roja** por encima del umbral rojo.

Las etiquetas de graduación en la parte superior de cada medidor están coloreadas para coincidir con la zona en la que se encuentran. Los valores se suavizan con animación balística para que los cambios rápidos no provoquen saltos bruscos.

La temperatura del PA y la tensión de alimentación se reportan directamente desde el flujo de telemetría de hardware de la radio. La velocidad del ventilador principal se resuelve por nombre de medidor cuando la radio lo publica por primera vez y se actualiza a medida que llegan las lecturas.

El applet ahora aplica el tema activo de la aplicación al contenedor de medidores utilizando el gestor de temas. Esto asegura que el área de medidores coincida con la apariencia de otros applets en el tema actual.

## Qué hace cada control

| Medidor       | Qué muestra                     | Rango válido |
|---------------|---------------------------------|--------------|
| **PA Temp**   | Temperatura del amplificador de potencia | 0–120 °C     |
| **+13.8V**    | Tensión de alimentación CC      | 10.0–16.0 V  |
| **Main Fan**  | Velocidad del ventilador de refrigeración principal | 0–3000 rpm   |

Ninguno de los medidores tiene ajustes persistentes ni controles ajustables por el usuario. No hay claves `AppSettings` asociadas con este applet.

La etiqueta del medidor **+13.8V** se actualiza dinámicamente para reflejar el valor de tensión en vivo reportado por la radio. Por ejemplo, cuando la radio reporta 13.82 V, la etiqueta del medidor muestra **+13.82V**. En la v26.6.3, la etiqueta sigue mostrando la tensión en vivo reportada por la radio (ej. '+13.82V') en lugar del marcador de posición estático '+13.8V'.

**Nota:** La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA está limitado a 10 A, lo que hace que la lectura se recorte bajo consumo máximo del PA, volviéndolo poco fiable.

### Accesibilidad

Cada medidor tiene un nombre accesible programático que los lectores de pantalla pueden anunciar:

- Medidor **PA Temp**: "PA temperature"
- Medidor **Supply voltage**: "Supply voltage"
- Medidor **Main Fan**: "Main fan speed"

Estos nombres accesibles se establecen mediante el marco de accesibilidad Qt y están disponibles para tecnología de asistencia en todas las plataformas compatibles.

## Consejos

- Una lectura de PA Temp que alcanza regularmente la zona roja (por encima de 70 °C) durante transmisiones largas puede indicar ventilación inadecuada alrededor de la radio.
- El umbral rojo del medidor de tensión es 15 V. Lecturas consistentemente por encima de ese valor sugieren un problema de regulación de la fuente de alimentación que vale la pena investigar.
- La velocidad del ventilador principal se mostrará como cero hasta que la radio publique el medidor MAINFAN. Esto es normal durante los primeros segundos después de la conexión.

## Relacionados

- [Watch PA temperature during long overs](watch-pa-temperature-during-long-overs.md)
- [Check the radio's DC supply voltage](check-the-radio-s-dc-supply-voltage.md)
- [Monitor the main cooling fan speed](monitor-the-main-cooling-fan-speed.md)
