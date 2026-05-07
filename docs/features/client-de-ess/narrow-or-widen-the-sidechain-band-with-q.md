# Reducir o ampliar la banda de la cadena lateral con Q

El control Q determina qué tan estrecha o ancha es la banda del filtro pasabanda de la cadena lateral alrededor de la frecuencia central de sibilancia. Un valor Q más alto enfoca la atenuación en una porción más ajustada del espectro; un valor Q más bajo afecta una banda más amplia. Ajuste Q después de localizar el pico de sibilancia con Freq para que el de-esser apunte exactamente al contenido correcto sin opacar consonantes cercanas.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada y visible. Aparece como un subcontenedor dentro del contenedor principal Aetherial Audio (TXDSP).
- Si el applet no está visible, abra el Aetherial Audio Channel Strip, que alberga los controles del de-esser directamente. El editor flotante separado "Aetherial De-Esser — TX" ya no existe.
- Para omitir el de-esser, haga clic una vez en la etapa DESS en el widget CHAIN. Al omitirse, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad como indicador visual.
- Ajuste la frecuencia central con Freq antes de afinar Q. Consulte [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md).
- El de-esser está disponible en dos instancias específicas por canal: TX (para audio transmitido) y RX (para audio recibido). La versión TX está etiquetada como "Aetherial De-Esser — TX" y la versión RX como "Aetherial De-Esser — RX". Ambas comparten controles y comportamiento idénticos.

## Pasos

1. Abra el applet Aetherial De-Esser dentro del Aetherial Audio Channel Strip. Use **showForTx()** para acceder a la instancia TX o **showForRx()** para acceder a la instancia RX.
2. Localice el control **Q** en la fila de cuatro controles de sintonización.
3. Gire **Q** en sentido horario para aumentar el valor y estrechar la banda de la cadena lateral, o en sentido antihorario para disminuir el valor y ampliarla.
4. Observe la curva de respuesta de la cadena lateral: el pico del pasabanda se ensancha o se agudiza a medida que Q cambia.
5. Mientras transmite o pronuncia una frase con sibilancia, observe la barra de reducción de ganancia para confirmar que el de-esser sigue activándose con el ancho de banda ajustado. Consulte [Observar GR en vivo mientras lee una frase con sibilancia](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Qué hace cada control

| Control                    | Valor predeterminado | Rango válido    | Comportamiento                                                                                                         |
|----------------------------|----------------------|-----------------|------------------------------------------------------------------------------------------------------------------------|
| **Q**                      | 2.00                 | 0.5 a 5.0       | Mapeo lineal. Define el ancho de banda de la banda de sibilancia — Q más alto = más estrecho. Etiqueta 'X.XX'.         |
| Curva de respuesta de la cadena lateral | —                    | —               | Respuesta del pasabanda en modo compacto. Dibuja la respuesta del filtro pasabanda con un punto móvil en la frecuencia central actual. |
| Barra de reducción de ganancia        | —                    | 0 a 24 dB GR    | Barra horizontal rojo suave, rellena desde la derecha. La escala máxima es 24 dB; una marca indica la cantidad típica de -6 dB. Se actualiza a ~30 Hz. |
| Attack (Ataque)            | 1.0 ms               | 0.1 a 30.0 ms   | Mapeo exponencial (0.1 * 300^n). Define la rapidez con que el de-esser responde cuando la sibilancia supera el umbral. Presente en ambas instancias TX y RX del Channel Strip. |
| Release (Liberación)       | 100 ms               | 10.0 a 500.0 ms | Mapeo exponencial (10 * 50^n). Define la rapidez con que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Presente en ambas instancias TX y RX del Channel Strip. |

## Atenuación por omisión

Cuando la etapa DESS se omite mediante un solo clic en el widget CHAIN, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el comportamiento de atenuación utilizado en la curva EQ y ofrece una indicación clara de un vistazo de que la etapa está inactiva. Haga clic nuevamente en la etapa DESS en el widget CHAIN para reactivarla y restaurar la opacidad completa.

## Consejos

- Comience con el valor predeterminado de 2.00 y aumente Q solo si la atenuación se extiende a vocales u otras consonantes adyacentes a la banda de sibilancia.
- Valores Q muy altos (superiores a 4.0) pueden hacer que el de-esser pase por alto sibilantes ligeramente descentrados. Si la reducción de ganancia deja de activarse de manera confiable, reduzca Q ligeramente o vuelva a barrer Freq.
- La curva de respuesta proporciona retroalimentación visual inmediata: úsela para juzgar si la campana es demasiado ancha o demasiado aguda antes de comprometerse con un ajuste.
- Los ajustes se guardan de forma independiente para las instancias TX y RX mediante claves de configuración separadas: `ClientDeEssTxQ` para TX y `ClientDeEssRxQ` para RX.

## Relacionados

- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Ajustar el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar GR en vivo mientras lee una frase con sibilancia](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
