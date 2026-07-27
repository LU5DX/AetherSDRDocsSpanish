# Supervisar la Velocidad del Ventilador Principal

Utilice el applet Medidores para observar en tiempo real la velocidad del ventilador principal de enfriamiento de la FLEX-8600. Esto le ayuda a confirmar que el ventilador está funcionando y detectar velocidades inusualmente altas que pueden indicar estrés térmico.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Medidores requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón **MTR** en la barra lateral derecha del panel de applets.
2. Haga clic en **MTR** para abrir el applet Medidores.
3. Lea el indicador **Main Fan** bajo el encabezado de sección **Radio Hardware**.
4. Para alternar la visualización de temperatura del PA entre Celsius y Fahrenheit, haga clic en el botón **°C** o **°F** en la fila del encabezado junto a la etiqueta **Radio Hardware**. El ajuste persiste entre sesiones.

## Qué hace cada control

| Indicador      | Qué muestra                                                         | Rango válido |
|----------------|---------------------------------------------------------------------|--------------|
| **PA Temp**    | Temperatura del PA, leída del medidor PATEMP de la radio. Se muestra en Celsius por defecto; alterne a Fahrenheit usando el botón **°C/°F** en el encabezado. La etiqueta del indicador se actualiza dinámicamente para mostrar el valor de temperatura en vivo (ej. **+55.0°C** o **+131.0°F**). El indicador tiene un nombre accesible de "PA temperature" para compatibilidad con lectores de pantalla. | 0–120 °C (32–248 °F) |
| **+13.8V**     | Voltaje de alimentación en voltios. La etiqueta del indicador se actualiza dinámicamente para mostrar el valor en vivo reportado por la radio (por ejemplo, **+13.82V**) en lugar del marcador estático **+13.8V**. El indicador tiene un nombre accesible de "Supply voltage" para compatibilidad con lectores de pantalla. | 10.0–16.0 V |
| **Main Fan**   | Velocidad actual del ventilador de enfriamiento en rpm, leída del medidor MAINFAN de la radio. El indicador tiene un nombre accesible de "Main fan speed" para compatibilidad con lectores de pantalla. | 0–3000 rpm  |

Las barras de los indicadores son de color cian en el rango operativo normal. El indicador **PA Temp** se vuelve rojo por encima de 70 °C (158 °F), el indicador **+13.8V** se vuelve rojo por encima de 15 V, y el indicador **Main Fan** se vuelve rojo por encima de 2500 rpm.

## Controles

| Control | Qué hace |
|---------|----------|
| Botón **°C/°F** | Alterna la visualización de temperatura del PA entre Celsius y Fahrenheit. La etiqueta se actualiza para mostrar la unidad actual. El ajuste persiste entre reinicios de la aplicación. |

## Consejos

- El indicador **Main Fan** se actualiza a medida que la radio reporta nuevos valores del medidor. Puede haber un breve retraso después de abrir el applet mientras se resuelve el índice del medidor.
- El indicador utiliza animación suavizada para los cambios de valor, por lo que las fluctuaciones rápidas aparecerán como un barrido suave en lugar de un salto instantáneo.
- La etiqueta del indicador **+13.8V** refleja el valor de voltaje en vivo reportado por la radio. La etiqueta se actualiza cada vez que la radio envía una nueva lectura del medidor, por lo que el voltaje mostrado (por ejemplo, **+13.82V**) siempre está actualizado.
- Al hacer clic en el botón **°C/°F**, el indicador de temperatura del PA se actualiza inmediatamente para mostrar valores en la unidad seleccionada. Las marcas de graduación en el indicador también cambian para reflejar la escala seleccionada.

## Accesibilidad

- Cada indicador tiene un nombre accesible configurado para compatibilidad con lectores de pantalla:
  - **PA Temp** — "PA temperature"
  - **+13.8V** — "Supply voltage"
  - **Main Fan** — "Main fan speed"
- El botón **°C/°F** tiene una descripción accesible: "Toggles PA temperature display between Celsius and Fahrenheit".

## Solución de problemas

- **El indicador Main Fan no muestra movimiento después de abrir el applet** — El índice del medidor del ventilador se resuelve de forma perezosa en la primera actualización. Espere unos segundos a que la radio emita una lectura del medidor. Si el indicador permanece en cero, verifique que la conexión con la radio esté activa mediante `Settings > Connect to Radio...`.
- **El applet Medidores no se muestra correctamente con ciertos temas** — El applet ahora aplica el estilo del tema mediante la configuración del contenedor `applet/meter`. Si experimenta problemas visuales, asegúrese de usar un tema compatible en `Settings > Appearance`.
- **El indicador de temperatura del PA muestra "0" o no se actualiza** — Verifique que la radio esté transmitiendo y reportando valores PATEMP. Algunas radios pueden no reportar temperatura cuando están inactivas.

## Relacionados

- [Descripción general de Medidores](overview.md)
- [Supervisar la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Verificar el voltaje de alimentación DC de la radio](check-the-radio-s-dc-supply-voltage.md)
