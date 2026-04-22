# Compensar los cambios de nivel con Output

Agregar Drive o Bias modifica el nivel general de la señal saturada. El control Output aplica una ganancia de ajuste post-tubo para que pueda restaurar el nivel original o establecer un nivel objetivo deliberado antes de que la señal continúe por la cadena TX.

## Antes de comenzar

- La etapa Tube Saturator debe estar habilitada. Consulte [Omitir el tubo de la cadena](bypass-the-tube-from-the-chain.md) para saber cómo habilitarla.
- Abra el subcontenedor TUBE dentro del contenedor principal PooDoo Audio (TXDSP). Si no está visible, haga doble clic en la etapa Tube en el widget CHAIN para abrir el editor flotante Tube.

## Pasos

1. Transmita una señal estable o use una fuente de tono para que la bola de entrada en vivo sobre la curva de transferencia esté en movimiento.
2. Localice el control Output — el cuarto control de la fila, etiquetado como **Output**.
3. Gire Output en sentido horario para aumentar el nivel post-tubo, o en sentido antihorario para reducirlo.
4. Deje de ajustar cuando el medidor de nivel de la etapa siguiente muestre el mismo valor que antes de agregar la saturación, o en el nivel que requiera su cadena TX.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistido |
|---|---|---|---|
| Output | 0.0 dB | −24.0 to 12.0 dB | `ClientTubeTxOutputGainDb` |

Output aplica una ganancia de compensación o recorte lineal después del modelo de tubo. No afecta la forma de la curva de transferencia: Drive, Tone y Bias permanecen sin cambios. La etiqueta del control muestra el valor actual como `X.X dB`.

## Consejos

- Un buen punto de partida es ajustar primero Drive hasta que la curva de transferencia se curve de forma notable, y luego usar Output para devolver el nivel a 0.0 dB. A partir de ahí, ajuste según su preferencia.
- Los cambios de Output se reflejan inmediatamente en la posición de la bola de entrada en vivo del widget de curva de transferencia, lo que le permite verificar que la señal sigue operando en el régimen de saturación deseado.
- Si utiliza el editor flotante Tube al mismo tiempo que el applet TUBE, los controles de ambas vistas se sincronizan automáticamente.

## Relacionado

- [Ajustar Drive hasta que la curva comience a doblarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Desplazar Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Mezcla en paralelo de la saturación con Mix](parallel-blend-saturation-with-mix.md)
- [Aclarar u oscurecer la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
