# Barrer la frecuencia para localizar el pico de sibilancia

Use el mando Freq para explorar la banda de sibilancia hasta que el medidor de reducción de ganancia alcance su máximo, identificando así la frecuencia central donde su micrófono produce los sonidos más duros de "S" y "T".

## Antes de comenzar

- La etapa De-Ess debe estar habilitada en el widget CHAIN. El applet De-Esser (DESS) permanece oculto hasta que la etapa esté activa.
- Abra el subcontenedor DESS dentro del contenedor principal PooDoo Audio (TXDSP). Si no está visible, haga doble clic en la etapa DeEss del widget CHAIN para abrir el editor flotante, o haga clic derecho en la barra de título del subcontenedor DESS y seleccione la opción correspondiente.
- Ajuste Thresh a un nivel en el que la sibilancia ya produzca algo de reducción de ganancia antes de comenzar el barrido. Consulte [Ajustar el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md).

## Pasos

1. Hable o repita en voz alta una frase sibilante ("sixty-six", "Mississippi") en su micrófono a su nivel de operación habitual.
2. Observe la barra de reducción de ganancia en la parte superior del applet DESS — un relleno rojo suave que se desplaza hacia la derecha indica que el de-esser está atenuando activamente.
3. Gire el mando Freq lentamente desde su valor predeterminado de 6.0 kHz hacia arriba o hacia abajo a lo largo del rango de 1000–12000 Hz.
4. Deténgase en la posición donde la barra de reducción de ganancia muestre el relleno más profundo durante su frase sibilante — esa es la frecuencia central del pico de sibilancia para la combinación de su voz y su micrófono.
5. Observe la esfera de frecuencia central en la curva de respuesta del sidechain; se desplaza a lo largo del pico de la curva para confirmar la frecuencia sintonizada en ese momento.
6. Continúe pronunciando frases sibilantes y realice pequeños ajustes en Freq hasta que la barra de reducción de ganancia responda de forma más agresiva y constante.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Freq | 6000 Hz | 1000 a 12000 Hz | `ClientDeEssTxFrequencyHz` | Establece la frecuencia central de la banda de sibilancia. Usa mapeo logarítmico. Las etiquetas muestran "X.X kHz" en 1000 Hz o por encima. |
| Q | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` | Establece el ancho de banda de la banda de sibilancia. Mayor Q = muesca más estrecha. |
| Thresh | -30.0 dB | -60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel a partir del cual el de-esser comienza a atenuar. |
| Amount | -6.0 dB | -24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada en el pico de sibilancia. |
| Curva de respuesta del sidechain | — | — | — | Muestra la respuesta del filtro pasabanda con una esfera animada en la frecuencia central actual. |
| Barra de reducción de ganancia | — | 0 a 24 dB GR | — | Franja horizontal rojo suave, rellena de izquierda a derecha. Una marca señala el punto de -6 dB. Se actualiza a aproximadamente 30 Hz. |

## Consejos

- Reduzca el Q antes de barrer si su sibilancia es aguda y tonal — una banda más estrecha hace que la barra de reducción de ganancia responda de forma más selectiva, facilitando la localización del pico.
- Si la barra de reducción de ganancia permanece vacía durante todo el barrido, Thresh está ajustado demasiado alto. Bájelo hasta que vea una respuesta y luego repita el barrido.
- Un Q de 2.00 (el valor predeterminado) es un ancho inicial razonable para un primer barrido. Ajuste Q con mayor precisión una vez que encuentre la frecuencia.

## Solución de problemas

- **La barra de reducción de ganancia no muestra relleno en ninguna posición de Freq** — Thresh está ajustado por encima de su nivel de sibilancia. Baje Thresh hasta que la barra responda, o aumente la ganancia del micrófono y vuelva a intentarlo.
- **La barra de reducción de ganancia siempre aparece completamente rellena sin importar la posición de Freq** — Amount está ajustado muy alto o Thresh está muy por debajo de su nivel promedio, lo que hace que el de-esser se active con todo el audio y no solo con la sibilancia. Suba Thresh y reduzca Amount antes de barrer.
- **El applet DESS no está visible** — La etapa De-Ess no está habilitada en el widget CHAIN. Habilítela allí primero.

## Relacionados

- [Descripción general del De-Esser](overview.md)
- [Estrechar o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la GR en tiempo real mientras se lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
