# Ajuste la anchura de la banda de la cadena secundaria con Q

El control **Q** determina qué tan ancho o estrecho es el filtro de paso de banda de la cadena secundaria alrededor de la frecuencia central de sibilancia. Un valor de Q más alto concentra la atenuación en una franja más estrecha del espectro; un valor más bajo afecta una banda más amplia. Ajuste Q después de localizar el pico de sibilancia con Freq, para que el de-esser apunte exactamente al contenido correcto sin apagar las consonantes adyacentes.

## Antes de comenzar

- El módulo Aetherial De-Esser (DESS) debe estar habilitado y visible. Aparece como un subcontenedor dentro del contenedor principal Aetherial Audio (TXDSP).
- Si el applet no está visible, haga doble clic en el módulo DESS en el widget CHAIN para abrir el editor sin marco titulado "Aetherial De-Esser — TX", que expone el mismo control Q.
- Establezca la frecuencia central con Freq antes de ajustar Q. Consulte [Barra Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md).

## Pasos

1. Abra el applet Aetherial De-Esser o el editor "Aetherial De-Esser — TX".
2. Localice el control **Q** en la fila de cuatro controles de ajuste.
3. Gire **Q** en sentido horario para aumentar el valor y estrechar la banda de la cadena secundaria, o en sentido antihorario para disminuir el valor y ensancharla.
4. Observe la curva de respuesta de la cadena secundaria: el pico del paso de banda se ensancha o se estrecha a medida que Q cambia.
5. Mientras transmite o pronuncia una frase con sibilantes, observe la barra de reducción de ganancia para confirmar que el de-esser sigue activándose con el ancho de banda ajustado. Consulte [Observe la GR en vivo mientras lee una frase con sibilantes](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Q** | 2.00 | 0.5 a 5.0 | `ClientDeEssTxQ` | Mapeo lineal. Los valores más altos estrechan el paso de banda de la cadena secundaria; los valores más bajos lo ensanchan. |
| Curva de respuesta de la cadena secundaria | — | — | — | Muestra la forma del filtro de paso de banda. Se actualiza en tiempo real mientras Q cambia. La bola marca la frecuencia central actual. |
| Barra de reducción de ganancia | — | 0 a 24 dB GR | — | Muestra la atenuación aplicada actualmente a la banda de sibilancia, actualizada aproximadamente 30 veces por segundo. |

## Consejos

- Comience con el valor predeterminado de 2.00 y aumente Q solo si la atenuación se derrama hacia las vocales u otras consonantes adyacentes a la banda de sibilancia.
- Los valores de Q muy altos (por encima de 4.0) pueden hacer que el de-esser no detecte sibilantes ligeramente descentradas. Si la GR deja de activarse de manera confiable, reduzca Q ligeramente o vuelva a explorar con Freq.
- La curva de respuesta ofrece retroalimentación visual inmediata: úsela para juzgar si la campana es demasiado ancha o demasiado estrecha antes de confirmar un ajuste.

## Temas relacionados

- [Barra Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Establezca el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajuste Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observe la GR en vivo mientras lee una frase con sibilantes](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omita el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
