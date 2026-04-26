# Compensar cambios de nivel con Output

El control **Output** aplica un ajuste de ganancia posterior al tubo, permitiéndole restaurar o reducir el nivel general después de que la etapa de tubo da forma a la señal. Úselo para igualar el nivel de salida saturado al que tenía antes de agregar Drive, o para reducir la señal si un Drive elevado la hace demasiado alta.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada y visible. Consulte [Omitir el tubo de la cadena](bypass-the-tube-from-the-chain.md) si el subcontenedor TUBE no aparece.
- Abra el subcontenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP), o haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante de Tube.

## Pasos

1. Localice el control **Output** — el cuarto control en la fila de cinco, etiquetado como "Output".
2. Gire **Output** en sentido horario para aumentar la ganancia posterior al tubo, o en sentido antihorario para reducirla.
3. Observe la curva de transferencia y su medidor de TX para confirmar que el nivel de salida está donde lo desea.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistente |
|---------|----------------------|--------------|-------------------|
| Output | 0.0 dB | −24.0 a 12.0 dB | `ClientTubeTxOutputGainDb` |

La etiqueta del control muestra el valor actual como `X.X dB`. La ganancia se aplica de forma lineal después del modelo de tubo, funcionando como una etapa de compensación o ajuste fino. No afecta la forma de la curva de transferencia.

## Consejos

- Un punto de partida habitual: anote su nivel de TX con Drive en 0.0 dB, luego aumente Drive hasta que la curva se doble a su gusto, y después reduzca Output hasta que el nivel de TX regrese a la lectura original.
- Los cambios de Output realizados en el editor flotante de Tube se reflejan en el control del applet en aproximadamente 33 ms, y viceversa.

## Relacionados

- [Ajustar Drive hasta que la curva comience a doblarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Mezcla en paralelo de la saturación con Mix](parallel-blend-saturation-with-mix.md)
- [Descripción general del Tube Saturator](overview.md)
