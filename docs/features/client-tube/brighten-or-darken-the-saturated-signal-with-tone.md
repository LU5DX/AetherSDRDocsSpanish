# Aclarar u oscurecer la señal saturada con Tone

El control **Tone** inclina el balance de frecuencias de la señal saturada por el tubo hacia un carácter más brillante o más oscuro. Úselo después de ajustar Drive para dar forma al color tonal de la saturación sin cambiar el nivel de salida general.

## Antes de comenzar

- El applet Tube Saturator debe estar visible. Aparece como el sub-contenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP).
- La etapa de tubo debe estar habilitada mediante el widget CHAIN. Si el applet está oculto, habilite la etapa primero para que aparezca el sub-contenedor TUBE.

## Pasos

1. Localice el sub-contenedor TUBE en el panel del applet.
2. Encuentre el control **Tone** — el segundo control desde la izquierda en la fila de cinco controles, entre Drive y Bias.
3. Gire **Tone** en sentido horario para aclarar la señal saturada (hacia `1.00`), o en sentido antihorario para oscurecerla (hacia `-1.00`).
4. Observe la etiqueta debajo del control; muestra el valor actual como un número con dos decimales, por ejemplo `0.25` o `-0.50`.
5. Para volver al punto neutro, haga doble clic en **Tone** para restablecerlo a su valor predeterminado de `0.00`.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---------|----------------|--------------|------------------|----------------|
| Tone | `0.00` | `-1.0` a `1.0` | `ClientTubeTxTone` | Los valores negativos oscurecen; los valores positivos aclaran la señal saturada. Mapeo lineal en todo el rango. |

## Consejos

- El control Tone afecta únicamente la porción saturada de la señal. Si Mix está por debajo del 100 %, la ruta seca no se ve afectada, por lo que el cambio tonal se mezclará de forma proporcional.
- Los cambios realizados en Tone desde el editor flotante de Tube se reflejan en el control del applet en aproximadamente 33 ms, y viceversa. Puede ajustar desde cualquiera de las dos ubicaciones.
- Los ajustes pequeños — valores entre `-0.30` y `0.30` — suelen ser suficientes. Los valores extremos pueden sonar poco naturales dependiendo de los ajustes de Drive y Bias.

## Relacionados

- [Descripción general del Tube Saturator](overview.md)
- [Ajustar Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Desplazar Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Compensar cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcla paralela de saturación con Mix](parallel-blend-saturation-with-mix.md)
