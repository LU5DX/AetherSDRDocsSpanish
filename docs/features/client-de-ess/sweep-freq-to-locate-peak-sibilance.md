# Barrer la frecuencia para localizar el pico de sibilancia

Utilice el mando Freq para barrer el rango de sibilancia mientras transmite o monitorea el audio, observando la barra de reducción de ganancia para encontrar la frecuencia que provoca la mayor reducción. Esto identifica el centro de la banda de sibilancia problemática antes de ajustar los parámetros Q, Thresh y Amount.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN en el contenedor Aetherial Audio (TXDSP). El applet permanece oculto hasta que la etapa DESS esté activa.
- Necesita una fuente de audio en vivo, ya sea transmitiendo o enrutando audio a través de la cadena TX DSP, para que la barra de reducción de ganancia responda en tiempo real.
- Abra el applet del de-esser. El bypass y la habilitación se controlan con un solo clic en la etapa DESS del widget CHAIN. La edición se realiza a través del Aetherial Audio Channel Strip.

## Pasos

1. Ajuste Thresh a un valor justo por debajo de sus picos típicos de sibilancia; un punto de partida de -30,0 dB (el valor predeterminado) funciona para la mayoría de las voces.
2. Ajuste Amount a un valor claramente audible, como -12,0 dB o inferior, para que la reducción de ganancia sea fácil de ver en la barra.
3. Hable o reproduzca audio que contenga sonidos sostenidos de "S" y "T" de forma continua en el micrófono.
4. Gire lentamente el mando Freq desde su valor predeterminado de 6,0 kHz hacia arriba o hacia abajo en el rango de 1000 a 12000 Hz.
5. Observe la barra de reducción de ganancia. La barra se llena más hacia la derecha, lo que indica la atenuación máxima, cuando Freq está centrada en la banda de sibilancia dominante.
6. Deténgase en el valor de Freq que produce la lectura de reducción de ganancia más alta. Ese valor es su frecuencia central de sibilancia.
7. Una vez completado el barrido, regrese Amount a su valor operativo previsto (valor predeterminado -6,0 dB).

## Función de cada control

| Control                  | Valor predeterminado                                                                                           | Rango válido                                                                                             |
|--------------------------|---------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Freq                     | 6000 Hz                                                                                                       | 1000 a 12000 Hz                                                                                          |
| Q                        | 2,00                                                                                                          | 0,5 a 5,0                                                                                                |
| Thresh                   | -30,0 dB                                                                                                      | -60,0 a 0,0 dB                                                                                           |
| Amount                   | -6,0 dB                                                                                                       | -24,0 a 0,0 dB                                                                                           |
| Attack                   | 1,0 ms                                                                                                        | 0,1 a 30,0 ms                                                                                            |
| Release                  | 100 ms                                                                                                        | 10,0 a 500,0 ms                                                                                          |
| Curva de respuesta de sidechain | —                                                                                                             | —                                                                                                         |
| Barra de reducción de ganancia | —                                                                                                             | 0 a 24 dB GR                                                                                             |

## Atenuación por bypass

Cuando la etapa DESS está en bypass a través del widget CHAIN, todo el mosaico del applet del de-esser se renderiza con opacidad reducida (aproximadamente al 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve al brillo total tan pronto como se vuelve a habilitar la etapa.

## Instancias RX y TX

El Aetherial De-Esser tiene ajustes separados para las rutas TX y RX. El Applet Panel acoplado muestra la copia TX etiquetada como "Aetherial De-Esser". La copia RX, etiquetada como "Aetherial De-Esser — RX", es accesible a través del StripDeEssPanel del Aetherial Audio Channel Strip.

El StripDeEssPanel en el Channel Strip se puede abrir para TX o RX. Cuando se abre para TX, el título de la ventana muestra "Aetherial De-Esser — TX". Cuando se abre para RX, el título de la ventana muestra "Aetherial De-Esser — RX". Cada instancia guarda y restaura de forma independiente sus propios ajustes de los mandos utilizando claves de configuración separadas.

## Consejos

- Mantenga Q en su valor predeterminado de 2,00 durante el barrido inicial. Un Q muy estrecho puede hacer que pase por alto el pico real sin activar la barra. Reduzca el ancho de la banda con Q solo después de haber localizado el pico.
- Si la barra de reducción de ganancia nunca se mueve, Thresh está ajustado demasiado alto. Redúzcalo hasta que la barra responda a los sonidos de "S".
- La bola de frecuencia central en la curva de respuesta de sidechain se mueve a medida que gira Freq, lo que proporciona una referencia visual incluso antes de que haya audio presente.

## Solución de problemas

- **La barra de reducción de ganancia no se mueve durante el barrido**: Thresh está por encima del nivel de sus picos de sibilancia. Reduzca Thresh hasta que la barra comience a responder y luego vuelva a barrer.
- **La barra se mantiene cerca del máximo en un amplio rango de Freq**: Amount está ajustado a un valor negativo muy grande y Thresh está muy bajo. Aumente Thresh ligeramente para que la barra discrimine entre frecuencias en lugar de fijarse en el máximo en todas partes.
- **El applet no es visible**: La etapa DESS no se ha habilitado en el widget CHAIN. Habilítela allí primero; el applet permanece oculto hasta que la etapa esté activa.
- **El mosaico del applet aparece atenuado**: La etapa DESS está actualmente en bypass. Haga un solo clic en la etapa DESS del widget CHAIN para volver a habilitarla.

## Relacionados

- [Aetherial De-Esser overview](overview.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
