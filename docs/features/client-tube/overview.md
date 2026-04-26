# Descripción general del Tube Saturator

El Tube Saturator es una etapa de procesamiento de audio en el lado TX que moldea la señal transmitida mediante un modelo de válvula con barrido de polarización, añadiendo riqueza armónica y saturación. Úselo para darle mayor presencia y carácter a su audio antes de que llegue al radio.

## Antes de comenzar

- El applet Tube Saturator permanece oculto hasta que la etapa Tube esté habilitada. Habilítela desde el widget CHAIN en el contenedor PooDoo Audio (TXDSP), o haga doble clic en la etapa Tube dentro del widget CHAIN para abrir el editor flotante.
- El applet aparece como el subcontenedor `TUBE` dentro del contenedor principal PooDoo Audio (TXDSP).

## Cómo funciona

El Tube Saturator procesa la señal de audio TX a través de una curva de transferencia no lineal que modela el comportamiento de saturación de válvulas. La forma de la curva cambia en tiempo real a medida que se ajustan Drive, Bias y el modelo de válvula activo.

El applet muestra un gráfico compacto de la curva de transferencia. Una bola de entrada en vivo se desplaza a lo largo de la curva, indicando en qué punto del régimen de saturación se encuentra el nivel de señal actual: completamente lineal cerca del centro y progresivamente saturado hacia los bordes. La posición de la bola se actualiza a aproximadamente 30 Hz y se suaviza ligeramente para evitar saltos bruscos.

Los cinco controles determinan con qué intensidad se impulsa la señal hacia la válvula (Drive), el carácter tonal del resultado (Tone), la asimetría del punto de operación (Bias), el nivel de salida posterior a la saturación (Output) y la mezcla entre la señal seca original y la señal saturada (Mix). Todos los ajustes se guardan y se mantienen sincronizados entre el applet y el editor flotante.

El bypass se gestiona desde el widget CHAIN, no desde el applet en sí.

## Qué hace cada control

| Control | Valor predeterminado | Rango | Ajuste guardado | Descripción |
|---|---|---|---|---|
| Transfer curve | — | — | — | Muestra la curva de transferencia actual de la válvula. Se curva y desplaza al cambiar Drive, Bias y el modelo. |
| Live input ball | — | — | — | El punto se mueve a lo largo de la curva de transferencia según el nivel de entrada actual, mostrando el régimen de saturación activo. |
| Drive | 0.0 dB | 0.0 a 24.0 dB | `ClientTubeTxDriveDb` | Impulsa más señal hacia la etapa de válvula. Valores más altos curvan la curva con mayor agresividad. |
| Tone | 0.00 | -1.0 a 1.0 | `ClientTubeTxTone` | Valores negativos oscurecen la señal saturada; valores positivos la aclaran. |
| Bias | 0 % | 0 % a 100 % | `ClientTubeTxBiasAmount` | Desplaza el punto de operación en la curva de transferencia, modificando el balance entre armónicos pares e impares. |
| Output | 0.0 dB | -24.0 a 12.0 dB | `ClientTubeTxOutputGainDb` | Ganancia de compensación o recorte posterior a la válvula. Úsela para compensar los cambios de nivel introducidos por la saturación. |
| Mix | 100 % | 0 % a 100 % | `ClientTubeTxDryWet` | Mezcla las señales seca (sin procesar) y saturada. Al 100 % solo pasa la señal saturada. |

El estado habilitado de la etapa Tube se guarda como `ClientTubeTxEnabled` y se controla desde el widget CHAIN.

## Consejos

- Comience con Drive en 0.0 dB y auméntelo lentamente hasta que la curva de transferencia se curve de forma visible. Ese punto de curvatura es donde comienza la saturación.
- Use Mix por debajo del 100 % para incorporar solo una porción de la señal saturada, lo que puede añadir calidez sin una coloración evidente.
- Aumentar Bias desplaza la curva de forma asimétrica, lo que introduce más armónicos de orden par y modifica el carácter de la saturación.
- Si la saturación eleva su nivel percibido, reduzca Output para compensar antes de ajustar otros parámetros.
- Los cambios realizados en el editor flotante se reflejan automáticamente en los controles del applet, y viceversa.

## Relacionados

- [Ajuste Drive hasta que la curva comience a curvarse](dial-drive-until-the-curve-starts-to-bend.md)
- [Modifique Bias para ajustar el balance de armónicos pares e impares](shift-bias-to-tweak-the-even-odd-harmonic-balance.md)
- [Aclare u oscurezca la señal saturada con Tone](brighten-or-darken-the-saturated-signal-with-tone.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle la saturación en paralelo con Mix](parallel-blend-saturation-with-mix.md)
- [Desactive la válvula desde la cadena](bypass-the-tube-from-the-chain.md)
