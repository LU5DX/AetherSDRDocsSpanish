# Ajuste el umbral justo por debajo de los picos 'S' más fuertes

Esta página explica cómo ajustar el control Thresh para que el de-esser actúe únicamente sobre la sibilancia genuina y deje el habla más suave sin procesar. Un umbral bien colocado es la diferencia entre un de-essing transparente y un efecto de bombeo audible.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN. Consulte [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md).
- El applet Aetherial De-Esser debe estar visible en el panel de applets (subcontenedor "Aetherial De-Esser" dentro del contenedor padre Aetherial Audio (TXDSP)).
- Necesita una forma de transmitir o monitorear su propio audio TX para que el habla genuina llegue al sidechain del de-esser.

## Pasos

1. Abra los controles del de-esser: haga doble clic en la etapa DESS del widget CHAIN para abrir el editor flotante "Aetherial De-Esser — TX", o trabaje directamente sobre el control Thresh en el applet acoplado.
2. Comience a hablar al micrófono repitiendo una frase sibilante; algo con sonidos 'S' y 'T' repetidos funciona bien.
3. Observe la barra de reducción de ganancia (Gain-reduction). Si muestra un relleno rojo suave durante vocales y consonantes normales (no solo en los picos 'S'), el umbral es demasiado bajo. Si nunca se mueve durante los sonidos 'S' fuertes, el umbral es demasiado alto.
4. Gire el control Thresh en sentido horario para subir el umbral (hacia 0.0 dB) hasta que la barra Gain-reduction permanezca vacía durante el habla normal.
5. Luego gire Thresh lentamente en sentido antihorario (hacia −60.0 dB) hasta que la barra Gain-reduction comience a llenarse justo en sus picos 'S' más fuertes y nada más.
6. Verifique: hable normalmente a lo largo de una oración completa. La barra Gain-reduction debe estar vacía la mayor parte del tiempo y llenarse brevemente solo en las sibilantes más marcadas.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Thresh | −30.0 dB | −60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` |
| Barra Gain-reduction | — | 0 a 24 dB GR | — |

**Thresh** — el nivel por encima del cual el de-esser comienza a atenuar la banda de sibilancia. Subir este valor (hacia 0.0 dB) hace que el de-esser actúe solo sobre la sibilancia más fuerte. Bajarlo (hacia −60.0 dB) hace que el de-esser se active con señales progresivamente más suaves.

**Barra Gain-reduction** — una franja horizontal rojo suave que se llena desde la derecha para mostrar la atenuación actual. La escala va de 0 a 24 dB. Una marca señala la posición −6 dB, que es el valor predeterminado de Amount. La barra se actualiza aproximadamente 30 veces por segundo.

## Consejos

- El umbral interactúa con Amount (`ClientDeEssTxAmountDb`). Ajuste primero el umbral y luego regule Amount a su gusto. Consulte [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md).
- Si no está seguro de en qué frecuencia se encuentran sus picos de sibilancia, localícelos primero antes de fijar el umbral. Consulte [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md).
- Observar la barra Gain-reduction en tiempo real mientras habla es la forma más confiable de evaluar la colocación del umbral. Consulte [Observar la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Solución de problemas

- **La barra Gain-reduction se llena continuamente, incluso en vocales** — Thresh está demasiado bajo. Súbalo (en sentido horario) hasta que la barra esté vacía durante el habla no sibilante.
- **La barra Gain-reduction no se mueve nunca, ni siquiera en sonidos 'S' fuertes** — Thresh está demasiado alto, o la banda de sibilancia (Freq, Q) no está centrada en las frecuencias problemáticas. Suba el nivel de la banda bajando Thresh, o revise Freq. Consulte [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md).
- **El de-esser parece no hacer nada en absoluto** — confirme que la etapa DESS está habilitada en el widget CHAIN. Consulte [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md).

## Relacionados

- [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ampliar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
