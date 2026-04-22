# Ajustar Bias para modificar el balance de armónicos pares e impares

El control Bias desplaza el punto de operación en la curva de transferencia del tubo. Alejarlo de cero introduce asimetría en la saturación, cambiando la proporción de armónicos pares e impares en la señal procesada.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada. Si el subcontenedor TUBE no es visible, habilite la etapa desde el widget CHAIN o haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante de Tube.
- Es necesario aplicar algo de Drive antes de que Bias tenga un efecto audible — una curva de transferencia recta no produce saturación independientemente del valor de Bias.

## Pasos

1. Abra el subcontenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP).
2. Localice el control Bias en la fila de cinco controles.
3. Gire Bias en sentido horario para aumentar la asimetría. Observe la curva de transferencia — la curva se dobla asimétricamente a medida que Bias aumenta.
4. Monitoree la bola de entrada en vivo sobre la curva de transferencia para confirmar que la señal recorre la porción moldeada de la curva.
5. Ajuste a gusto. Regrese Bias a 0 % para restaurar una curva de transferencia simétrica.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Bias | 0 % | 0 % a 100 % (0.0 a 1.0) | `ClientTubeTxBiasAmount` | Desplaza el punto de operación en la curva de transferencia. Los valores más altos aumentan la asimetría, elevando la proporción de armónicos pares respecto a los impares. |
| Curva de transferencia | — | — | — | Dibuja la curva de transferencia actual del tubo y se actualiza en tiempo real conforme cambia Bias. |
| Bola de entrada en vivo | — | — | — | El punto sigue el nivel de entrada actual a lo largo de la curva de transferencia, mostrando qué porción de la curva utiliza la señal. |

## Consejos

- Bias interactúa con el modelo de tubo activo. El efecto de un valor de Bias determinado difiere entre Model A, Model B y Model C, ya que cada modelo aplica la asimetría de forma distinta.
- Después de aumentar Bias, revise el control Output. La saturación asimétrica puede desplazar el nivel de salida promedio; use Output para compensarlo.
- Para una coloración sutil de armónicos pares, mantenga Bias bajo (menos del 25 %) y use un Drive moderado.

## Relacionado

- [Ajustar Drive hasta que la curva comience a doblarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Descripción general del Tube Saturator](overview.md)
