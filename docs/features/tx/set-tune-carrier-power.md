# Establecer la potencia del portador de sintonía

El control deslizante "Tune Pwr" determina cuánta potencia RF emite la radio cuando se presiona TUNE. Mantenerlo bajo protege el sistema de antena y cualquier amplificador conectado durante la sintonización.

## Antes de comenzar

- AetherSDR debe estar conectado a su radio FLEX-8600.
- El applet TX debe estar visible en el Panel de Applets. Si no lo está, haga clic en el botón TX del panel lateral derecho.

## Pasos

1. Localice el control deslizante "Tune Pwr:" en el applet TX.
2. Arrastre el control hacia la izquierda para disminuir la potencia o hacia la derecha para aumentarla. El valor numérico a la derecha del control se actualiza de inmediato.
3. Suelte el control deslizante. El nuevo valor se envía a la radio.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| Tune Pwr | 10 | 0–100 | Establece el nivel de potencia del portador de sintonía. El valor se aplica la próxima vez que se presiona TUNE. |

## Consejos

- Un valor de 10 es suficiente para que el ATU interno encuentre concordancia en la mayoría de las bandas. Auméntelo solo si el ATU necesita más potencia para medir la ROE con precisión.
- El control deslizante "Tune Pwr:" es independiente del control "RF Power:", que regula la potencia de transmisión normal. Modificar uno no afecta al otro.
- También puede establecer la potencia de sintonía por banda mediante `Settings > TX Band Settings...`, lo cual reemplaza el control global para cada banda individual.

## Temas relacionados

- [Iniciar un portador de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Establecer la potencia de salida RF](set-rf-output-power.md)
- [Descripción general de los controles TX](overview.md)
