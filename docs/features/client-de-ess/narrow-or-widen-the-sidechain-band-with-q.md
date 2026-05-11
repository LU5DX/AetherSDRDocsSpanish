# Ajustar la anchura de la banda de la cadena lateral con Q

El mando Q controla la anchura del filtro de paso de banda de la cadena lateral alrededor de la frecuencia central de sibilancia. Un Q más alto concentra la atenuación en una porción más estrecha del espectro; un Q más bajo afecta una banda más amplia. Ajuste Q después de localizar el pico de sibilancia con Freq para que el de-esser apunte exactamente al contenido problemático sin opacar consonantes cercanas.

## Antes de empezar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada y visible. Aparece como un subcontenedor dentro del contenedor principal Aetherial Audio (TXDSP).
- Si el applet no es visible, abra el Aetherial Audio Channel Strip, que alberga los controles del de-esser directamente. El editor flotante independiente "Aetherial De-Esser — TX" ya no existe.
- Para omitir (bypass) el de-esser, haga clic una vez en la etapa DESS en el widget CHAIN. Cuando está en bypass, todo el mosaico del applet se atenúa a aproximadamente un 55 % de opacidad como indicador visual.
- Ajuste la frecuencia central con Freq antes de afinar el Q. Consulte [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md).
- El de-esser está disponible en dos instancias específicas para cada lado: TX (para audio transmitido) y RX (para audio recibido). La versión TX está etiquetada como "Aetherial De-Esser" y la versión RX como "Aetherial De-Esser — RX". Ambas comparten controles y comportamiento idénticos. La instancia RX es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Abra el applet Aetherial De-Esser dentro del Aetherial Audio Channel Strip. Use **showForTx()** para acceder a la instancia TX o **showForRx()** para acceder a la instancia RX.
2. Localice el mando **Q** en la fila de cuatro mandos de sintonización.
3. Gire **Q** en el sentido de las agujas del reloj para aumentar el valor y estrechar la banda de la cadena lateral, o en sentido contrario para disminuir el valor y ensancharla.
4. Observe la curva de respuesta de la cadena lateral: el pico del paso de banda se ensancha o se afina a medida que cambia Q.
5. Mientras transmite o dice una frase sibilante, observe la barra de reducción de ganancia para confirmar que el de-esser sigue activándose con el ancho de banda ajustado. Consulte [Ver GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Qué hace cada control

| Control                    | Por defecto | Rango válido    | Comportamiento                                                                                           |
|----------------------------|-------------|-----------------|----------------------------------------------------------------------------------------------------------|
| **Q**                      | 2.00        | 0.5 a 5.0       | Mapeo lineal. Define el ancho de banda de la banda de sibilancia — Q más alto = más estrecho. Etiqueta 'X.XX'. |
| Curva de respuesta de la cadena lateral | —           | —               | Respuesta de paso de banda en modo compacto. Dibuja la respuesta del filtro de paso de banda con un punto móvil en la frecuencia central actual. Las etiquetas de los ejes (100, 500, 1k, etc.) se renderizan usando QStaticText para mejorar el rendimiento. |
| Barra de reducción de ganancia | —           | 0 a 24 dB GR    | Barra horizontal de color rojo suave, rellena desde la derecha. La escala máxima es 24 dB; una marca indica la cantidad típica de -6 dB. Se actualiza a ~30 Hz. |
| Attack                    | 1.0 ms      | 0.1 a 30.0 ms   | Mapeo exponencial (0.1 * 300^n). Define la rapidez con la que el de-esser responde una vez que la sibilancia supera el umbral. Presente en ambas instancias del Channel Strip (TX y RX). El ClientDeEssApplet acoplado omite este mando. |
| Release                   | 100 ms      | 0.1 a 500.0 ms  | Mapeo exponencial (10 * 50^n). Define la rapidez con la que la ganancia retorna después de que la sibilancia cae por debajo del umbral. Presente en ambas instancias del Channel Strip (TX y RX). El ClientDeEssApplet acoplado omite este mando. |

## Atenuación por bypass

Cuando la etapa DESS se omite (bypass) mediante un solo clic en el widget CHAIN, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el comportamiento de atenuación utilizado en la curva de EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. Haga clic nuevamente en la etapa DESS en el widget CHAIN para reactivarla y restaurar la opacidad completa.

## Consejos

- Comience con el valor por defecto de 2.00 y aumente Q solo si la atenuación se está derramando sobre vocales u otras consonantes adyacentes a la banda de sibilancia.
- Valores de Q muy altos (por encima de 4.0) pueden hacer que el de-esser no detecte sibilantes ligeramente descentrados. Si la GR deja de activarse de manera fiable, reduzca Q ligeramente o vuelva a barrer Freq.
- La curva de respuesta proporciona retroalimentación visual inmediata: úsela para juzgar si la campana es demasiado ancha o demasiado estrecha antes de confirmar un ajuste.
- Los ajustes se guardan de forma independiente para las instancias TX y RX mediante claves de configuración separadas: `ClientDeEssTxQ` para TX y `ClientDeEssRxQ` para RX.

## Relacionados

- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Ajustar el umbral justo por debajo de los picos más fuertes de 'S'](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Ver GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
