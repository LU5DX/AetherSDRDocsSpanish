# Barrer con Freq para localizar el pico de sibilancia

Use el control Freq para escanear el rango de sibilancia mientras transmite o monitorea audio, observando la barra de reducción de ganancia para identificar la frecuencia que provoca la mayor reducción. Esto identifica el centro de la banda de sibilancia problemática antes de finalizar los ajustes de Q, Thresh y Amount.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN en el contenedor Aetherial Audio (TXDSP). El applet permanece oculto hasta que la etapa DESS esté activa.
- Se necesita una fuente de audio activa — ya sea transmitiendo o enrutando audio a través de la cadena TX DSP — para que la barra de reducción de ganancia responda en tiempo real.
- Abra el applet del de-esser o el editor flotante. Para abrir el editor flotante, haga doble clic en la etapa DESS en el widget CHAIN. El editor se titula "Aetherial De-Esser — TX".

## Pasos

1. Ajuste Thresh a un valor ligeramente por debajo de sus picos de sibilancia típicos — un punto de partida de -30.0 dB (el valor predeterminado) funciona para la mayoría de las voces.
2. Ajuste Amount a un valor claramente audible, como -12.0 dB o menor, de modo que la reducción de ganancia sea fácil de ver en la barra.
3. Hable o reproduzca audio que contenga sonidos prolongados de "S" y "T" de forma continua hacia el micrófono.
4. Gire lentamente el control Freq desde su valor predeterminado de 6.0 kHz hacia arriba o hacia abajo, a lo largo del rango de 1000 a 12000 Hz.
5. Observe la barra de reducción de ganancia. La barra se llena más hacia la derecha — lo que indica la atenuación máxima — cuando Freq está centrado en la banda de sibilancia dominante.
6. Detenga el barrido en el valor de Freq que produzca la lectura más alta de reducción de ganancia. Ese valor es la frecuencia central de su sibilancia.
7. Restablezca Amount a su valor operativo previsto (predeterminado -6.0 dB) una vez que el barrido esté completo.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Freq | 6000 Hz | 1000 a 12000 Hz | `ClientDeEssTxFrequencyHz` | Establece la frecuencia central de la banda de sibilancia. Utiliza mapeo logarítmico. La curva de respuesta del sidechain y su indicador en vivo de frecuencia central se actualizan al girar el control. |
| Q | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` | Establece el ancho de banda de la banda de sibilancia. Un Q mayor = banda más estrecha. Mantenga Q en un valor moderado durante el barrido para no perder el pico. |
| Thresh | -30.0 dB | -60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel por encima del cual comienza la atenuación. Ajústelo suficientemente bajo durante el barrido para que la barra responda claramente a la sibilancia. |
| Amount | -6.0 dB | -24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada en el pico de sibilancia. Auméntelo temporalmente durante el barrido para facilitar la lectura de la barra de reducción de ganancia. |
| Curva de respuesta del sidechain | — | — | — | Dibuja la respuesta del filtro pasa-banda. El indicador en vivo marca la frecuencia central actual. |
| Barra de reducción de ganancia | — | 0 a 24 dB GR | — | Franja horizontal de color rojo suave, rellena de derecha. Una marca señala el punto de -6 dB. Se actualiza aproximadamente a 30 Hz. |

## Consejos

- Mantenga Q en su valor predeterminado de 2.00 durante el barrido inicial. Un Q muy estrecho puede hacer que el barrido pase por encima del pico real sin activar la barra. Reduzca el ancho de banda con Q solo después de haber localizado el pico.
- Si la barra de reducción de ganancia no se mueve, Thresh está configurado demasiado alto. Bájelo hasta que la barra responda a los sonidos de "S".
- El indicador de frecuencia central en la curva de respuesta del sidechain se mueve al girar Freq, proporcionando una referencia visual incluso antes de que haya audio presente.

## Solución de problemas

- **La barra de reducción de ganancia no se mueve durante el barrido** — Thresh está por encima del nivel de sus picos de sibilancia. Baje Thresh hasta que la barra comience a responder y luego repita el barrido.
- **La barra permanece cerca del máximo en un amplio rango de Freq** — Amount está ajustado a un valor negativo muy grande y Thresh está muy bajo. Suba Thresh ligeramente para que la barra discrimine entre frecuencias en lugar de saturarse al máximo en todas partes.
- **El applet no es visible** — La etapa DESS no ha sido habilitada en el widget CHAIN. Habilítela primero allí; el applet permanece oculto hasta que la etapa esté activa.

## Relacionado

- [Descripción general del Aetherial De-Esser](overview.md)
- [Reducir o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos más fuertes de "S"](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la reducción de ganancia en vivo mientras se lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
