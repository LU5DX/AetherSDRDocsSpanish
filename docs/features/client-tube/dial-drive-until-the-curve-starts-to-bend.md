# Ajuste Drive hasta que la curva comience a curvarse

Drive controla qué tan fuerte se empuja la señal hacia la etapa de válvula. Al aumentarlo, la curva de transferencia se dobla visiblemente alejándose de una línea recta — ese es el punto donde comienza la saturación armónica.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada. Si el subcontenedor TUBE está oculto, habilite la etapa desde el widget CHAIN o haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante de Tube.
- Abra el subcontenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP). Debería ver la curva de transferencia y los cinco controles giratorios debajo de ella.

## Pasos

1. Localice la curva de transferencia en la parte superior del applet TUBE. Con Drive en 0.0 dB, la curva es casi una línea diagonal recta.
2. Observe la bola de entrada en tiempo real — se desplaza a lo largo de la curva según el nivel de entrada actual, mostrando dónde se ubica su señal en la característica de transferencia.
3. Gire el control Drive lentamente en sentido horario. La curva de transferencia comienza a doblarse en la parte superior e inferior a medida que Drive aumenta, lo que indica el inicio de la saturación.
4. Detenga el ajuste cuando la curvatura sea visible en el nivel donde la bola de entrada en tiempo real se desplaza. Este es el régimen de saturación para su nivel de señal actual.
5. Si el nivel de salida ha aumentado notablemente, compénselo usando el control Output. Consulte [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Drive | 0.0 dB | 0.0 – 24.0 dB | `ClientTubeTxDriveDb` | Empuja más señal hacia la etapa de válvula. Valores más altos doblan la curva más lejos de la linealidad. |
| Curva de transferencia | — | — | — | Dibuja la curva de transferencia de válvula configurada en ese momento. Se actualiza en tiempo real al cambiar Drive. |
| Bola de entrada en tiempo real | — | — | — | Punto que se desplaza sobre la curva según el nivel de entrada actual, visualizando el régimen de saturación. |

## Consejos

- Comience con Drive por debajo de 6 dB y auméntelo lentamente. La curvatura se vuelve evidente mucho antes del máximo de 24.0 dB; valores elevados de Drive producen una distorsión armónica intensa.
- La forma de la curva también depende de Bias y del modelo de válvula seleccionado en el editor flotante. Si la curva se dobla asimétricamente, Bias tiene un valor distinto de cero — consulte [Ajustar Bias para modificar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md).
- Los cambios realizados en el editor flotante de Tube se reflejan en los controles del applet en aproximadamente 33 ms y viceversa, por lo que puede utilizar cualquiera de los dos para ajustar Drive.

## Solución de problemas

- **La curva de transferencia no es visible** — El subcontenedor TUBE solo es visible cuando la etapa Tube está habilitada. Habilite la etapa desde el widget CHAIN y regrese al applet TUBE.
- **La bola de entrada en tiempo real está fija en el borde izquierdo** — Ninguna señal está pasando por la cadena TX. Verifique que esté transmitiendo o enviando audio hacia la ruta TX.
- **Girar Drive no produce ningún cambio audible** — Compruebe que Mix esté por encima de 0 %. Con 0 % la señal completamente seca pasa por alto la válvula por completo. Consulte [Mezcla en paralelo de la saturación con Mix](parallel-blend-saturation-with-mix.md).

## Relacionados

- [Descripción general de Tube Saturator](overview.md)
- [Ajustar Bias para modificar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Mezcla en paralelo de la saturación con Mix](parallel-blend-saturation-with-mix.md)
- [Omitir la válvula desde la cadena](bypass-the-tube-from-the-chain.md)
