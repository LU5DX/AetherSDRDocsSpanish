# Monitorear la velocidad del ventilador de enfriamiento principal

Use el applet Meters para observar la velocidad del ventilador de enfriamiento principal del FLEX-8600 en tiempo real. Esto le ayuda a confirmar que el ventilador está funcionando y a detectar velocidades inusualmente altas que pueden indicar estrés térmico. El applet también muestra la temperatura del PA y los medidores de voltaje de alimentación.

## Antes de comenzar

- AetherSDR debe estar conectado a la radio. El applet Meters requiere una conexión activa con la radio.
- El panel de applets debe estar visible. Si está oculto, actívelo mediante `View > Applet Panel`.

## Pasos

1. Localice el botón de bandeja **MTR** en la barra lateral derecha del panel de applets.
2. Haga clic en **MTR** para alternar la apertura del applet Meters.
3. Lea el medidor **Main Fan** bajo el encabezado de sección **Radio Hardware**.
4. Para alternar la visualización de temperatura del PA entre Celsius y Fahrenheit, haga clic en el botón **°C** o **°F** en la fila del encabezado junto a la etiqueta **Radio Hardware**. La configuración se conserva entre sesiones.

## Qué hace cada control

| Medidor                  | Qué muestra                                                                                                                                                                                                                                                                                                                                      | Rango válido                                                           |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| **PA Temp**              | Temperatura del PA, leída del medidor PATEMP de la radio. Se muestra en Celsius por defecto; alterne a Fahrenheit usando el botón **°C/°F** en el encabezado. La etiqueta del medidor muestra el valor de temperatura en vivo con la unidad seleccionada (p. ej., **+55.0°C** o **+131.0°F**). El medidor tiene un nombre accesible de "PA temperature" para compatibilidad con lectores de pantalla. | 0–120 °C (32–248 °F); rojo por encima de 70 °C (158 °F)               |
| **Alternancia °C / °F**  | Alterna la visualización de temperatura del PA entre Celsius y Fahrenheit; la elección se conserva en el objeto de configuración `MtrApplet` (campo `tempFahrenheit`). Se encuentra en la fila del encabezado junto a la etiqueta de sección **Radio Hardware**.                                                                                 | °C / °F                                                               |
| **+13.8V (voltaje de alimentación)** | Voltaje de alimentación en voltios. La etiqueta del medidor refleja dinámicamente el valor reportado en vivo por la radio (p. ej., **+13.82V**) mediante `HGauge::setLabel`, en lugar del marcador estático **+13.8V**. El medidor tiene un nombre accesible de "Supply voltage" para compatibilidad con lectores de pantalla.               | 10.0–16.0 V; rojo por encima de 15 V                                  |
| **Main Fan**             | Velocidad actual del ventilador de enfriamiento en rpm, leída del medidor MAINFAN de la radio (resuelto de forma diferida mediante `MeterModel::findMeter`). La etiqueta muestra las rpm en vivo. El medidor tiene un nombre accesible de "Main fan speed" para compatibilidad con lectores de pantalla.                                        | 0–3000 rpm; rojo por encima de 2500 rpm                               |

Las barras de los medidores son cian en el rango operativo normal. El medidor **PA Temp** se vuelve rojo por encima de 70 °C (158 °F), el medidor **+13.8V** se vuelve rojo por encima de 15 V, y el medidor **Main Fan** se vuelve rojo por encima de 2500 rpm.

> **Nota:** El medidor **PACURRENT** se omite intencionalmente del applet Meters. El rango del medidor de 10 A se satura bajo el consumo máximo del PA en el hardware FLEX-8000.

## Controles

| Control            | Qué hace                                                                                   |
|--------------------|--------------------------------------------------------------------------------------------|
| Botón **°C/°F**    | Alterna la visualización de temperatura del PA entre Celsius y Fahrenheit. La etiqueta se actualiza para mostrar la unidad actual. La configuración se conserva entre reinicios de la aplicación. |

## Consejos

- El medidor **Main Fan** se actualiza a medida que la radio reporta nuevos valores de medidor. Puede haber un breve retraso después de que el applet se abre por primera vez mientras se resuelve el índice del medidor.
- El medidor utiliza animación suavizada para los cambios de valor, por lo que las fluctuaciones rápidas aparecerán como un barrido suave en lugar de un salto instantáneo.
- La etiqueta del medidor **+13.8V** refleja el valor de voltaje en vivo reportado por la radio. La etiqueta se actualiza cada vez que la radio envía una nueva lectura de medidor, por lo que el voltaje mostrado (por ejemplo, **+13.82V**) siempre está actualizado.
- Cuando haga clic en el botón **°C/°F**, el medidor de temperatura del PA se actualiza inmediatamente para mostrar valores en la unidad seleccionada. La escala del medidor y las marcas de graduación se vuelven a renderizar al instante para coincidir con la escala seleccionada, evitando cualquier animación a través del salto de unidad.
- El medidor **PA Temp** solo se actualiza cuando la radio reporta una lectura válida de temperatura del PA; si la radio no reporta una, el medidor conserva su estado anterior en lugar de caer a cero.

## Accesibilidad

- Cada medidor tiene un nombre accesible configurado para compatibilidad con lectores de pantalla:
  - **PA Temp** — "PA temperature"
  - **+13.8V** — "Supply voltage"
  - **Main Fan** — "Main fan speed"
- El botón **°C/°F** tiene una descripción accesible: "Toggles PA temperature display between Celsius and Fahrenheit".

## Solución de problemas

- **El medidor Main Fan no muestra movimiento después de abrir el applet** — El índice del medidor del ventilador se resuelve de forma diferida en la primera actualización. Espere unos segundos para que la radio emita una lectura de medidor. Si el medidor permanece en cero, verifique que la conexión con la radio esté activa mediante `Settings > Connect to Radio...`.
- **El applet Meters no se muestra correctamente con ciertos temas** — El applet ahora aplica el estilo del tema mediante la configuración del contenedor `applet/meter`. Si experimenta problemas visuales, asegúrese de usar un tema compatible en `Settings > Appearance`.
- **El medidor de temperatura del PA muestra "0" o no se actualiza** — Verifique que la radio esté transmitiendo y reportando valores PATEMP. Algunas radios pueden no reportar temperatura cuando están inactivas. Si la radio no reporta un valor PATEMP en absoluto, el medidor no se actualizará; esto es un comportamiento esperado.

## Relacionado

- [Descripción general de Meters](overview.md)
- [Observar la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Verificar el voltaje de alimentación de CC de la radio](check-the-radio-s-dc-supply-voltage.md)
