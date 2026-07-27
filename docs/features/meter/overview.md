# Resumen de medidores

El applet Medidores muestra telemetría de hardware en tiempo real desde la FLEX-8600 conectada: temperatura del PA, voltaje de alimentación CD y velocidad del ventilador principal de enfriamiento. Úselo para supervisar la salud del radio durante la operación sin salir de la ventana principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a un radio FLEX-8600. El applet requiere una conexión activa con el radio.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Cómo funciona

El applet Medidores está oculto por defecto. Ábralo o ciérrelo usando el botón **MTR** en la bandeja de la barra lateral derecha.

Una vez abierto, el applet muestra una sección "Radio Hardware" que contiene tres barras de medidor horizontales. Cada barra se llena de izquierda a derecha y cambia de color a medida que el valor sube a través de zonas de advertencia y alarma:

- La barra es **verde** por debajo del umbral amarillo.
- La barra se vuelve **amarilla-ámbar** entre los umbrales amarillo y rojo.
- La barra se vuelve **roja** por encima del umbral rojo.

Las etiquetas de las marcas en la parte superior de cada barra están coloreadas según la zona en la que se encuentran. Los valores se suavizan con animación balística para que los cambios rápidos no provoquen saltos bruscos.

La temperatura del PA y el voltaje de alimentación se reportan directamente desde la transmisión de telemetría del hardware del radio. La velocidad del ventilador principal se resuelve por el nombre del medidor cuando el radio lo publica por primera vez y se actualiza a medida que llegan las lecturas.

El applet ahora aplica el tema activo de la aplicación al contenedor de medidores usando el administrador de temas. Esto asegura que el área de medidores coincida con la apariencia de otros applets en el tema actual.

## Qué hace cada control

| Medidor       | Qué muestra                     | Rango válido        |
|---------------|---------------------------------|---------------------|
| **PA Temp**   | Temperatura del amplificador de potencia | 0–120 °C o 32–248 °F |
| **+13.8V**    | Voltaje de alimentación CD      | 10.0–16.0 V         |
| **Main Fan**  | Velocidad del ventilador principal de enfriamiento | 0–3000 rpm |

### Medidor PA Temp

El medidor PA Temp muestra la lectura de temperatura del amplificador de potencia desde el medidor PATEMP. La etiqueta del medidor se actualiza dinámicamente para mostrar la temperatura actual en la unidad seleccionada (ej. "55.0°C" o "131.0°F").

Use el botón de alternancia **°C/°F** en la fila del encabezado para cambiar entre la visualización en Celsius y Fahrenheit. Al hacer clic en el botón, se alterna la unidad de temperatura para todas las lecturas de PA Temp. La configuración se conserva en `MtrApplet.tempFahrenheit` y sobrevive a los reinicios de la aplicación.

Las marcas del medidor se ajustan automáticamente al cambiar de unidad:
- Marcas en Celsius: 0, 30, 55, 70, 90, 120 °C
- Marcas en Fahrenheit: 32, 86, 131, 158, 194, 248 °F

El umbral rojo se alcanza a 70 °C (158 °F).

### Medidor de voltaje de alimentación

La etiqueta del medidor **+13.8V** se actualiza dinámicamente para reflejar el valor de voltaje en vivo reportado por el radio. Por ejemplo, cuando el radio reporta 13.82 V, la etiqueta del medidor muestra **+13.82V**. El umbral rojo del medidor es 15 V.

### Medidor Main Fan

El medidor Main Fan muestra el valor del medidor MAINFAN. La velocidad será cero hasta que el radio publique el medidor MAINFAN, lo cual es normal durante los primeros segundos después de la conexión.

**Nota:** La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA está limitado a 10 A, lo que causa que la lectura se recorte bajo la demanda máxima del PA, volviéndolo poco fiable.

### Botón de alternancia de unidad de temperatura

Un botón **°C/°F** aparece en la fila del encabezado del applet, a la derecha de la etiqueta "Radio Hardware". Este botón alterna la unidad de visualización de la temperatura del PA. Al hacer clic en él:

- La etiqueta del botón cambia a la unidad opuesta.
- El valor del medidor PA Temp y las etiquetas de las marcas se actualizan a la nueva unidad.
- La configuración se guarda en la configuración de la aplicación bajo la clave `MtrApplet.tempFahrenheit`.

El botón de alternancia tiene un estilo de resaltado y enfoque consistente con el tema actual. Incluye una descripción accesible para lectores de pantalla: "Toggles PA temperature display between Celsius and Fahrenheit".

## Accesibilidad

Cada medidor tiene un nombre accesible programático que los lectores de pantalla pueden anunciar:

- Medidor **PA Temp**: "PA temperature"
- Medidor **Supply voltage**: "Supply voltage"
- Medidor **Main Fan**: "Main fan speed"
- Botón de alternancia **Temperature unit toggle**: "Toggles PA temperature display between Celsius and Fahrenheit"

Estos nombres accesibles se establecen usando el marco de accesibilidad Qt y están disponibles para tecnologías de asistencia en todas las plataformas compatibles.

## Consejos

- Una lectura de PA Temp que alcanza regularmente la zona roja (por encima de 70 °C / 158 °F) durante transmisiones largas puede indicar ventilación inadecuada alrededor del radio.
- El umbral rojo del medidor de voltaje es 15 V. Lecturas consistentemente por encima de ese valor sugieren un problema de regulación de la fuente de alimentación que vale la pena investigar.
- La velocidad del Main Fan será cero hasta que el radio publique el medidor MAINFAN. Esto es normal durante los primeros segundos después de la conexión.

## Relacionado

- [Watch PA temperature during long overs](watch-pa-temperature-during-long-overs.md)
- [Check the radio's DC supply voltage](check-the-radio-s-dc-supply-voltage.md)
- [Monitor the main cooling fan speed](monitor-the-main-cooling-fan-speed.md)
