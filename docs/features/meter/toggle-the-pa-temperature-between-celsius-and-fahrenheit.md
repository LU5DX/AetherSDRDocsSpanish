# Alternar la temperatura del PA entre Celsius y Fahrenheit

Esta página le muestra cómo cambiar el indicador de temperatura del PA en el applet Meters entre Celsius y Fahrenheit, y explica cómo la selección se conserva entre sesiones.

## Antes de comenzar

- Conéctese a su radio FLEX-8600.
- El applet Meters está oculto por defecto. Asegúrese de que el botón de bandeja MTR esté habilitado en la barra lateral derecha.

## Pasos

1. Haga clic en el botón de bandeja MTR en la barra lateral derecha para abrir el applet Meters.
2. Localice el encabezado "Radio Hardware" en el applet.
3. Haga clic en el botón de unidad de temperatura (etiquetado "°C" o "°F") junto al encabezado para alternar entre Celsius y Fahrenheit.

El indicador PA Temp se reescala al instante y muestra la temperatura en vivo en la unidad seleccionada. Su selección se guarda automáticamente.

## Qué hace cada control

| Control | Valor por defecto | Comportamiento | Clave de configuración |
|---------|---------|----------|-------------|
| Indicador PA Temp | °C | Muestra la lectura del medidor PATEMP de la radio. El rango de escala es 0–120 °C o 32–248 °F. Zona roja por encima de 70 °C / 158 °F. | Ninguna |
| Botón de alternancia °C / °F | °C | Alterna la visualización de la temperatura del PA entre Celsius y Fahrenheit. La etiqueta del indicador muestra el valor en vivo con la unidad seleccionada. | `MtrApplet` (campo tempFahrenheit) |

## Consejos

- La escala del indicador y las marcas de graduación se ajustan inmediatamente a la nueva unidad; no hay animación en el salto de °C a °F.
- La información sobre herramientas del botón de alternancia le indica a qué unidad cambiará a continuación (por ejemplo, "Haga clic para mostrar en Fahrenheit").
- La selección se conserva entre reinicios y se almacena en el objeto de configuración `MtrApplet` bajo el campo `tempFahrenheit`.

## Relacionado

- [Vigile la temperatura del PA durante transmisiones largas](watch-pa-temperature-during-long-overs.md)
- [Compruebe el voltaje de suministro de CC en vivo de la radio](check-the-radio-s-live-dc-supply-voltage.md)
- [Supervise la velocidad del ventilador de refrigeración principal](monitor-the-main-cooling-fan-speed.md)
- [Resumen de Meters](overview.md)
