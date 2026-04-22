# Aclarar u oscurecer la señal saturada con Tone

Use el control **Tone** del applet Tube Saturator para modificar el carácter tonal de la señal saturada — los valores negativos la oscurecen y los valores positivos la aclaran.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada desde el widget CHAIN o el editor flotante Tube. El applet TUBE permanece oculto hasta que la etapa esté activa.
- Abra el subcontenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP). Si no está visible, haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante, o haga clic derecho en la barra de título del subcontenedor TUBE y seleccione la opción correspondiente.

## Pasos

1. Localice el control **Tone** en la fila de cinco controles en la parte inferior del applet TUBE.
2. Gire el control hacia la izquierda (hacia −1.0) para oscurecer la señal saturada, o hacia la derecha (hacia +1.0) para aclararla.
3. Observe la curva de transferencia y la bola de entrada en vivo sobre los controles para ver cómo cambia el régimen de saturación al ajustar Tone.
4. Suelte el control. El valor se guarda automáticamente en `ClientTubeTxTone`.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Tone | 0.00 | −1.0 a 1.0 | `ClientTubeTxTone` | Los valores negativos oscurecen la señal saturada; los valores positivos la aclaran. La etiqueta muestra el valor con dos decimales. |

## Consejos

- Un valor de Tone de 0.00 deja el carácter tonal de la señal saturada sin cambios respecto al modelo de tubo y al ajuste de Drive.
- Los cambios realizados aquí se reflejan en el editor flotante Tube en aproximadamente 33 ms, y viceversa — ambas vistas permanecen sincronizadas.
- Después de ajustar Tone, revise el control Output para compensar cualquier cambio de nivel percibido introducido por el desplazamiento tonal.

## Relacionados

- [Descripción general de Tube Saturator](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Desplazar Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Mezcla en paralelo de la saturación con Mix](parallel-blend-saturation-with-mix.md)
- [Omitir el tubo desde la cadena](bypass-the-tube-from-the-chain.md)
