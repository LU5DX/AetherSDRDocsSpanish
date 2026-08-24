# Descripción general de los medidores

El applet Meters muestra telemetría de hardware en tiempo real de la FLEX-8600 conectada: temperatura del amplificador de potencia (PA), voltaje de alimentación de CC y velocidad del ventilador de enfriamiento principal. Úselo para supervisar la salud de la radio durante la operación sin salir de la ventana principal de AetherSDR.

## Antes de comenzar

- AetherSDR debe estar conectado a una radio FLEX-8600. El applet requiere una conexión de radio activa.
- El panel del applet debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Cómo funciona

El applet Meters está oculto de forma predeterminada. Ábralo o ciérrelo usando el botón de la bandeja **MTR** en la barra lateral derecha.

Una vez abierto, el applet muestra una sección "Radio Hardware" que contiene tres medidores de barra horizontales. Cada medidor se llena de izquierda a derecha y cambia de color a medida que el valor asciende por las zonas de advertencia y alarma:

- La barra es **verde** por debajo del umbral amarillo.
- La barra se vuelve **amarillo-ámbar** entre los umbrales amarillo y rojo.
- La barra se vuelve **roja** por encima del umbral rojo.

Las etiquetas de las marcas en la parte superior de cada medidor están coloreadas para coincidir con la zona en la que se encuentran. Los valores se suavizan con animación balística para que los cambios rápidos no causen saltos bruscos.

La temperatura del PA y el voltaje de alimentación se reportan directamente desde el flujo de telemetría de hardware de la radio. La velocidad del ventilador principal se resuelve por nombre del medidor cuando la radio la publica por primera vez y se actualiza a medida que llegan las lecturas.

El applet ahora aplica el tema activo de la aplicación al contenedor de medidores mediante el administrador de temas. Esto garantiza que el área de medidores coincida con la apariencia de otros applets en el tema actual.

## Qué hace cada control

| Medidor                 | Qué muestra                                                                                                                                     | Rango válido                                                            |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **PA Temp**             | Temperatura del amplificador de potencia                                                                                                        | 0–120 °C o 32–248 °F                                                    |
| **+13.8V**              | Voltaje de alimentación de CC                                                                                                                   | 10.0–16.0 V                                                             |
| **Main Fan**            | Velocidad del ventilador de enfriamiento principal                                                                                              | 0–3000 rpm                                                              |
| **Alternar °C / °F**    | Alterna la visualización de temperatura del PA entre Celsius y Fahrenheit; la elección se guarda en el objeto de configuración `MtrApplet` (campo tempFahrenheit). | Ubicado en la fila de encabezado junto a la etiqueta de la sección 'Radio Hardware'. |
| **+13.8V (voltaje de alimentación)** | Muestra el medidor de voltaje de alimentación; la etiqueta se actualiza dinámicamente para mostrar el valor de voltaje en vivo (p. ej. '+13.82V') mediante HGauge::setLabel. | 10.0–16.0 V (rojo > 15)                                                 |

### Medidor PA Temp

El medidor PA Temp muestra la lectura de temperatura del amplificador de potencia desde el medidor PATEMP. La etiqueta del medidor se actualiza dinámicamente para mostrar la temperatura actual en la unidad seleccionada (p. ej. "55.0°C" o "131.0°F").

Use el botón de alternancia **°C/°F** en la fila de encabezado para cambiar entre la visualización en Celsius y Fahrenheit. Al hacer clic en el botón se alterna la unidad de temperatura para todas las lecturas de PA Temp. El ajuste se guarda en `MtrApplet.tempFahrenheit` y sobrevive a los reinicios de la aplicación.

Las marcas del medidor se ajustan automáticamente al cambiar de unidad:
- Marcas en Celsius: 0, 30, 55, 70, 90, 120 °C
- Marcas en Fahrenheit: 32, 86, 131, 158, 194, 248 °F

El umbral rojo se alcanza a 70 °C (158 °F).

### Medidor de voltaje de alimentación

La etiqueta del medidor **+13.8V** se actualiza dinámicamente para reflejar el valor de voltaje en vivo reportado por la radio. Por ejemplo, cuando la radio reporta 13.82 V, la etiqueta del medidor muestra **+13.82V**. El umbral rojo del medidor es 15 V.

### Medidor Main Fan

El medidor Main Fan muestra el valor del medidor MAINFAN. La velocidad mostrará cero hasta que la radio publique el medidor MAINFAN, lo cual es normal durante los primeros segundos después de la conexión.

**Nota:** La corriente del PA no se muestra. En el hardware de la serie FLEX-8000, el medidor de corriente del PA está limitado a 10 A, lo que hace que la lectura se recorte bajo consumo máximo del PA, volviéndola poco confiable.

### Alternancia de unidad de temperatura

Un botón **°C/°F** aparece en la fila de encabezado del applet, a la derecha de la etiqueta "Radio Hardware". Este botón alterna la unidad de visualización de temperatura del PA. Cuando hace clic en él:

- La etiqueta del botón cambia a la unidad opuesta.
- El valor del medidor PA Temp y las etiquetas de las marcas se actualizan a la nueva unidad.
- El ajuste se guarda en la configuración de la aplicación bajo la clave `MtrApplet.tempFahrenheit`.

El botón de alternancia tiene estilo de desplazamiento y enfoque consistente con el tema actual. Incluye una descripción accesible para lectores de pantalla: "Toggles PA temperature display between Celsius and Fahrenheit".

## Accesibilidad

Cada medidor tiene un nombre accesible programático que los lectores de pantalla pueden anunciar:

- Medidor **PA Temp**: "PA temperature"
- Medidor de **voltaje de alimentación**: "Supply voltage"
- Medidor **Main Fan**: "Main fan speed"
- Botón de **alternancia de unidad de temperatura**: "Toggles PA temperature display between Celsius and Fahrenheit"

Estos nombres accesibles se establecen mediante el marco de accesibilidad de Qt y están disponibles para la tecnología de asistencia en todas las plataformas compatibles.

## Consejos

- Una lectura de PA Temp que alcanza regularmente la zona roja (por encima de 70 °C / 158 °F) durante transmisiones largas puede indicar ventilación inadecuada alrededor de la radio.
- El umbral rojo del medidor de voltaje es 15 V. Lecturas consistentemente por encima de ese valor sugieren un problema de regulación de la fuente de alimentación que vale la pena investigar.
- La velocidad del Main Fan mostrará cero hasta que la radio publique el medidor MAINFAN. Esto es normal durante los primeros segundos después de la conexión.

## Relacionados

- [Vigile la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Compruebe el voltaje de alimentación de CC de la radio](check-the-radio-s-dc-supply-voltage.md)
- [Supervise la velocidad del ventilador de enfriamiento principal](monitor-the-main-cooling-fan-speed.md)
