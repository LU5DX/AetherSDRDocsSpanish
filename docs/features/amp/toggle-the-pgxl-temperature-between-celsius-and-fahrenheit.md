# Cambiar la temperatura del PGXL entre Celsius y Fahrenheit

Cambie la lectura de temperatura del amplificador en el applet Amplifier entre Celsius y Fahrenheit. La unidad que elija se recordará la próxima vez que se inicie AetherSDR.

## Antes de comenzar

- AetherSDR debe detectar un amplificador Power Genius XL.
- El applet Amplifier debe estar visible. Si no lo está, haga clic en el botón **AMP** de la barra lateral derecha.

## Pasos

1. Ubique el botón de temperatura en el applet Amplifier. Muestra la temperatura actual y la unidad, por ejemplo `45.6 °C`.
2. Haga clic en el botón de temperatura para cambiar a la otra unidad. La pantalla se actualiza de inmediato y la información sobre herramientas anuncia la unidad a la que cambiaría el siguiente clic.
3. La unidad elegida se guarda automáticamente. No se requiere ninguna acción adicional.

## Qué hace cada control

| Control | Predeterminado | Configuración persistida | Comportamiento |
| :--- | :--- | :--- | :--- |
| Temp (botón C/F) | °C | `AmpApplet` (campo `tempFahrenheit`) | Muestra la temperatura del amplificador y alterna entre Celsius y Fahrenheit al hacer clic. Muestra `tempA/tempB °C` cuando ambos sensores informan, o `tempA °C` en caso contrario. |

## Consejos

- El botón de temperatura también muestra ambos sensores cuando el PGXL informa dos lecturas de temperatura (por ejemplo, `45.6/47.2 °C`).
- La elección de la unidad se guarda por aplicación, no por radio, por lo que se mantiene al reconectar la radio.

## Relacionados

- [Ver la temperatura del PGXL, la corriente de drenaje y el voltaje de la red](watch-pgxl-temperature-drain-current-and-mains-voltage.md)
- [Descripción general del amplificador](overview.md)
