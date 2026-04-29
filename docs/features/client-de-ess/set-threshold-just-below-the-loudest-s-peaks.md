# Ajuste el umbral justo por debajo de los picos 'S' más fuertes

Esta página explica cómo ajustar el mando Thresh para que el de-esser actúe únicamente sobre la sibilancia genuina y deje el habla más suave sin procesar. Un umbral bien colocado marca la diferencia entre un de-essing transparente y un bombeo audible.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN. Consulte [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md).
- El applet Aetherial De-Esser debe estar visible en el panel de applets (subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP)).
- Necesita una forma de transmitir o monitorear su propio audio TX para que el habla genuina llegue a la cadena lateral del de-esser.

## Pasos

1. Abra los controles del de-esser: haga doble clic en la etapa DESS en el widget CHAIN para abrir el editor flotante "Aetherial De-Esser — TX", o trabaje directamente en el mando Thresh del applet acoplado.
2. Comience a hablar frente a su micrófono, repitiendo una frase con sibilantes — algo con sonidos 'S' y 'T' repetidos funciona bien.
3. Observe la barra de reducción de ganancia (Gain-reduction bar). Si muestra un relleno rojo tenue durante las vocales y consonantes normales (no solo en los picos de 'S'), el umbral está demasiado bajo. Si nunca se mueve durante los sonidos 'S' fuertes, el umbral está demasiado alto.
4. Gire el mando Thresh en sentido horario para subir el umbral (hacia 0.0 dB) hasta que la barra Gain-reduction permanezca vacía durante el habla normal.
5. Luego gire Thresh lentamente en sentido antihorario (hacia −60.0 dB) hasta que la barra Gain-reduction comience a llenarse justo en sus picos 'S' más fuertes y no antes.
6. Verifique: hable normalmente a lo largo de una oración completa. La barra Gain-reduction debe estar vacía la mayor parte del tiempo y llenarse brevemente solo en las sibilantes más marcadas.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Thresh | −30.0 dB | −60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` |
| Barra Gain-reduction | — | 0 a 24 dB GR | — |

**Thresh** — el nivel por encima del cual el de-esser comienza a atenuar la banda de sibilancia. Subir este valor (hacia 0.0 dB) hace que el de-esser actúe solo sobre la sibilancia más fuerte. Bajarlo (hacia −60.0 dB) provoca que el de-esser se active ante señales progresivamente más suaves.

**Barra Gain-reduction** — una franja horizontal de color rojo tenue que se llena desde la derecha para mostrar la atenuación actual. La escala va de 0 a 24 dB. Una marca señala la posición de −6 dB, que es el valor predeterminado de Amount. La barra se actualiza aproximadamente 30 veces por segundo.

## Consejos

- El umbral interactúa con Amount (`ClientDeEssTxAmountDb`). Ajuste primero el umbral y luego regule Amount según su preferencia. Consulte [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md).
- Si no está seguro de dónde se encuentran sus picos de sibilancia en frecuencia, localícelos primero antes de fijar el umbral. Consulte [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md).
- Observar la barra Gain-reduction en tiempo real mientras habla es la forma más fiable de juzgar la colocación del umbral. Consulte [Monitorear la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Solución de problemas

- **La barra Gain-reduction se llena continuamente, incluso en las vocales** — Thresh está demasiado bajo. Súbalo (en sentido horario) hasta que la barra esté vacía durante el habla no sibilante.
- **La barra Gain-reduction nunca se mueve, ni siquiera con sonidos 'S' fuertes** — Thresh está demasiado alto, o la banda de sibilancia (Freq, Q) no está centrada en las frecuencias problemáticas. Aumente el nivel de la banda bajando Thresh, o revise Freq. Consulte [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md).
- **El de-esser parece no hacer nada en absoluto** — confirme que la etapa DESS está habilitada en el widget CHAIN. Consulte [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md).

## Relacionados

- [Barrer Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md)
- [Reducir o ampliar la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Monitorear la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
