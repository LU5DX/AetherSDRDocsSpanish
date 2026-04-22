# Ajustar la potencia del portador de sintonía

El control deslizante "Tune Pwr" establece el nivel de potencia RF utilizado al activar un portador de sintonía. Mantener la potencia de sintonía baja protege su amplificador y antena, mientras que el ATU sigue siendo capaz de encontrar una concordancia de impedancia.

## Antes de comenzar

- AetherSDR debe estar conectado al radio. El applet TX no es funcional sin una conexión al radio.
- El applet TX debe estar visible en el Panel de Applets. Si no está visible, haga clic en el botón TX de la barra lateral derecha.

## Pasos

1. Localice el control deslizante "Tune Pwr" en el applet TX. Es la segunda fila de controles deslizantes, debajo de "RF Power".
2. Arrastre el control deslizante hacia la izquierda o la derecha para establecer el nivel de potencia del portador de sintonía deseado. El indicador numérico a la derecha del control se actualiza de inmediato.

## Qué hace cada control

| Control | Descripción | Predeterminado | Rango válido |
|---|---|---|---|
| Tune Pwr | Establece el nivel de potencia del portador de sintonía transmitido cuando TUNE está activo. | 10 | 0–100 |

## Consejos

- Establezca la potencia de sintonía antes de presionar TUNE. El valor toma efecto al inicio del siguiente ciclo de sintonía.
- Una potencia de sintonía baja (10–20) es suficiente para la concordancia del ATU en la mayoría de los casos y reduce el estrés en los componentes del PA.

## Relacionados

- [Iniciar un portador de sintonía para verificar la ROE](start-a-tune-carrier-to-check-swr.md)
- [Ejecutar el ATU interno](run-the-internal-atu.md)
- [Ajustar la potencia de salida RF](set-rf-output-power.md)
