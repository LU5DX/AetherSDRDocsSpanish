# Barrer frecuencia para localizar el pico de sibilancia

Use el mando Freq para barrer el rango de sibilancia mientras transmite o monitorea audio, observando la barra de reducción de ganancia para identificar la frecuencia que provoca la mayor reducción. Esto determina el centro de la banda problemática de sibilancia antes de ajustar los valores definitivos de Q, Thresh y Amount.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN en el contenedor Aetherial Audio (TXDSP). La applet permanece oculta hasta que la etapa DESS esté activa.
- Necesita una fuente de audio en vivo (ya sea transmitiendo o enrutando audio a través de la cadena TX DSP) para que la barra de reducción de ganancia responda en tiempo real.
- Abra la applet del de-esser. La activación y desactivación se controlan con un solo clic en la etapa DESS dentro del widget CHAIN. La edición se realiza a través del Aetherial Audio Channel Strip.

## Pasos

1. Ajuste Thresh a un valor justo por debajo de sus picos típicos de sibilancia: un punto de partida de -30.0 dB (el valor predeterminado) funciona para la mayoría de las voces.
2. Ajuste Amount a un valor claramente audible, como -12.0 dB o inferior, para que la reducción de ganancia sea fácil de ver en la barra.
3. Hable o reproduzca audio que contenga sonidos sostenidos de "S" y "T" de forma continua en el micrófono.
4. Gire lentamente el mando Freq desde su valor predeterminado de 6.0 kHz hacia arriba o hacia abajo en el rango de 1000 a 12000 Hz.
5. Observe la barra de reducción de ganancia. La barra se llena más hacia la derecha (lo que indica la atenuación máxima) cuando Freq está centrado en la banda de sibilancia dominante.
6. Deténgase en el valor de Freq que produzca la lectura más alta de reducción de ganancia. Ese valor es su frecuencia central de sibilancia.
7. Una vez completado el barrido, regrese Amount a su valor operativo deseado (valor predeterminado -6.0 dB).

## Función de cada control

| Control                    | Valor predeterminado | Rango válido     |
|----------------------------|----------------------|------------------|
| Freq                       | 6000 Hz            | 1000 a 12000 Hz  |
| Q                          | 2.00                | 0.5 a 5.0        |
| Thresh                     | -30.0 dB            | -60.0 a 0.0 dB   |
| Amount                     | -6.0 dB             | -24.0 a 0.0 dB   |
| Attack                     | 1.0 ms              | 0.1 a 30.0 ms    |
| Release                    | 100 ms              | 10.0 a 500.0 ms  |
| Curva de respuesta de sidechain | —               | —                |
| Barra de reducción de ganancia | —               | 0 a 24 dB GR     |

**Nota:** Los mandos Attack y Release solo aparecen en el Channel Strip StripDeEssPanel (tanto RX como TX). La applet acoplada ClientDeEssApplet omite estos controles.

## Etiquetas de los ejes de la curva de respuesta de sidechain

El widget de la curva dibuja las etiquetas del eje de frecuencia usando QStaticText para mejorar el rendimiento del renderizado. Las etiquetas se muestran como "100", "500", "1k", "2k", etc. El texto de la etiqueta se almacena en caché después del primer trazado y se reutiliza en los redibujados posteriores. Las etiquetas de los ejes se ocultan cuando el widget de la curva está en modo compacto.

## Atenuación por bypass

Cuando la etapa DESS está desactivada mediante el widget CHAIN, el mosaico completo de la applet del de-esser se renderiza con opacidad reducida (aproximadamente 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve al brillo total tan pronto como se vuelve a habilitar la etapa.

## Instancias RX y TX

El Aetherial De-Esser tiene configuraciones independientes para las rutas TX y RX. El Applet Panel acoplado muestra la copia TX etiquetada como "Aetherial De-Esser". La copia RX, etiquetada como "Aetherial De-Esser — RX", es accesible a través del StripDeEssPanel del Aetherial Audio Channel Strip.

El StripDeEssPanel en el Channel Strip se puede abrir para TX o RX. Cuando se abre para TX, el título de la ventana muestra "Aetherial De-Esser — TX". Cuando se abre para RX, el título de la ventana muestra "Aetherial De-Esser — RX". Cada instancia guarda y restaura de forma independiente su propia configuración de mandos utilizando claves de configuración separadas:
- TX: `ClientDeEssTxFrequencyHz`, `ClientDeEssTxQ`, `ClientDeEssTxThresholdDb`, `ClientDeEssTxAmountDb`, `ClientDeEssTxAttackMs`, `ClientDeEssTxReleaseMs`
- RX: `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, `ClientDeEssRxThresholdDb`, `ClientDeEssRxAmountDb`, `ClientDeEssRxAttackMs`, `ClientDeEssRxReleaseMs`

## Consejos

- Mantenga Q en su valor predeterminado de 2.00 durante el barrido inicial. Un Q muy estrecho puede hacer que pase por alto el pico real sin activar la barra. Reduzca el ancho de banda con Q solo después de haber localizado el pico.
- Si la barra de reducción de ganancia nunca se mueve, Thresh está configurado demasiado alto. Redúzcalo hasta que la barra responda a los sonidos "S".
- La bola de frecuencia central en la curva de respuesta de sidechain se mueve a medida que gira Freq, lo que proporciona una referencia visual incluso antes de que haya audio presente.

## Solución de problemas

- **La barra de reducción de ganancia no se mueve durante el barrido**: Thresh está por encima del nivel de sus picos de sibilancia. Reduzca Thresh hasta que la barra comience a responder, luego vuelva a barrer.
- **La barra permanece cerca del máximo en un rango amplio de Freq**: Amount está configurado con un valor negativo muy grande y Thresh está muy bajo. Aumente Thresh ligeramente para que la barra discrimine entre frecuencias en lugar de fijarse al máximo en todas partes.
- **La applet no es visible**: La etapa DESS no se ha habilitado en el widget CHAIN. Habilítela allí primero; la applet permanece oculta hasta que la etapa esté activa.
- **El mosaico de la applet aparece atenuado**: La etapa DESS está actualmente en modo bypass. Haga clic una vez en la etapa DESS en el widget CHAIN para volver a habilitarla.

## Relacionado

- [Descripción general de Aetherial De-Esser](overview.md)
- [Reducir o ampliar la banda de sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar GR en vivo mientras se lee una frase con sibilancia](watch-live-gr-while-reading-a-sibilant-phrase.md)
