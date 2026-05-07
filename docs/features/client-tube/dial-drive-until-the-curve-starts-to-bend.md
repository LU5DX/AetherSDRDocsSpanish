# Drive (Conducción) hasta que la curva comience a doblarse

Drive (Conducción) controla cuán fuerte se inyecta la señal en la etapa de válvula. Aumentarlo hace que la curva de transferencia se desvíe visiblemente de una línea recta — el punto donde comienza la saturación armónica.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada. Si el subcontenedor TUBE está oculto, habilite la etapa mediante el widget CHAIN o haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante de Tube.
- Abra el subcontenedor TUBE dentro del contenedor padre PooDoo Audio (TXDSP). Debería ver la curva de transferencia y las cinco perillas debajo de ella.

## Pasos

1. Localice la curva de transferencia en la parte superior del applet TUBE. Con Drive en 0.0 dB, la curva es casi una línea recta diagonal.
2. Observe la bola de entrada en vivo — se mueve a lo largo de la curva al nivel de entrada actual, mostrando dónde se sitúa su señal en la característica de transferencia.
3. Gire la perilla Drive lentamente en sentido horario. La curva de transferencia comienza a doblarse en la parte superior e inferior a medida que Drive aumenta, indicando el inicio de la saturación.
4. Deténgase cuando la curvatura sea visible al nivel donde se desplaza la bola de entrada en vivo. Este es el régimen de saturación para su nivel de señal actual.
5. Si el nivel de salida ha aumentado notablemente, compense usando la perilla Output. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | Inyecta más señal en la etapa de válvula. Valores más altos doblan la curva más lejos de la linealidad. |
| Curva de transferencia | — | — | — | Dibuja la curva de transferencia de válvula actualmente configurada. Se actualiza en tiempo real a medida que Drive cambia. |
| Bola de entrada en vivo | — | — | — | Punto que recorre la curva al nivel de entrada actual, visualizando el régimen de saturación. |

## Consejos

- Comience con Drive por debajo de 6 dB y aumente lentamente. La curvatura se vuelve evidente mucho antes del máximo de 24.0 dB; los valores altos de Drive producen una fuerte distorsión armónica.
- La forma de la curva también depende de Bias y del modelo de válvula seleccionado en el editor flotante. Si la curva se dobla asimétricamente, Bias es distinto de cero — consulte [Desplazar Bias para ajustar el balance de armónicos pares/impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md).
- Los cambios realizados en el editor flotante de Tube se reflejan en las perillas del applet en aproximadamente 33 ms y viceversa, por lo que puede usar cualquiera de los dos para ajustar Drive.

## Solución de problemas

- **La curva de transferencia no es visible** — El subcontenedor TUBE solo es visible cuando la etapa Tube está habilitada. Habilite la etapa desde el widget CHAIN, luego regrese al applet TUBE.
- **La bola de entrada en vivo está atascada en el borde izquierdo** — No pasa señal a través de la cadena de TX. Verifique que está transmitiendo o inyectando audio en la ruta de TX.
- **Girar Drive no produce cambios audibles** — Verifique que Mix esté por encima del 0 %. Al 0 %, la señal completamente seca evita la válvula por completo. Consulte [Mezcla paralela de saturación con Mix](parallel-blend-saturation-with-mix.md).

## Relacionados

- [Resumen de Tube Saturator](overview.md)
- [Desplazar Bias para ajustar el balance de armónicos pares/impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Mezcla paralela de saturación con Mix](parallel-blend-saturation-with-mix.md)
- [Evitar la válvula desde la cadena](bypass-the-tube-from-the-chain.md)
