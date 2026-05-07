# Ajuste el umbral justo por debajo de los picos de 'S' más fuertes

Esta página explica cómo ajustar el mando Thresh para que el de-esser actúe únicamente sobre sibilancias genuinas y deje intacto el habla más suave. Un umbral bien colocado marca la diferencia entre un de-essing transparente y un bombeo audible.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN. Consulte [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md).
- El applet Aetherial De-Esser debe ser visible en el panel de applets (subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP)).
- Necesita una forma de transmitir o monitorear su propio audio de TX para que el habla real llegue a la cadena lateral del de-esser.

## Pasos

1. Abra los controles del de-esser: abra el Aetherial Audio Channel Strip, o trabaje directamente con el mando Thresh en el applet acoplado.
2. Comience a hablar por su micrófono, repitiendo una frase con sibilancias — una con sonidos repetidos de 'S' y 'T' funciona bien.
3. Observe la barra Gain-reduction. Si muestra un relleno rojo suave durante vocales y consonantes normales (no solo en picos de 'S'), el umbral es demasiado bajo. Si nunca se mueve durante sonidos fuertes de 'S', el umbral es demasiado alto.
4. Gire el mando Thresh en el sentido de las agujas del reloj para subir el umbral (hacia 0.0 dB) hasta que la barra Gain-reduction permanezca vacía durante el habla normal.
5. Luego, gire Thresh lentamente en sentido contrario a las agujas del reloj (hacia −60.0 dB) hasta que la barra Gain-reduction comience a llenarse justo en sus picos de 'S' más fuertes y no más.
6. Verifique: hable normalmente durante una oración completa. La barra Gain-reduction debe estar vacía la mayor parte del tiempo y llenarse brevemente solo en sibilancias fuertes.

## Qué hace cada control

| Control            | Por defecto | Rango válido    |
|--------------------|-------------|-----------------|
| Thresh             | −30.0 dB    | −60.0 a 0.0 dB  |
| Gain-reduction bar | —           | 0 a 24 dB GR    |
| Attack             | 1.0 ms      | 0.1 a 30.0 ms   |
| Release            | 100 ms      | 10.0 a 500.0 ms |

**Thresh** — el nivel por encima del cual el de-esser comienza a atenuar la banda de sibilancias. Aumentar este valor (hacia 0.0 dB) hace que el de-esser actúe solo en las sibilancias más fuertes. Reducirlo (hacia −60.0 dB) hace que el de-esser se active con señales progresivamente más silenciosas.

**Gain-reduction bar** — una barra horizontal roja suave que se llena desde la derecha para mostrar la atenuación actual. La escala va de 0 a 24 dB. Una marca indica la posición de −6 dB, que es el valor predeterminado de Amount. La barra se actualiza aproximadamente 30 veces por segundo.

**Attack** — la rapidez con la que el de-esser responde una vez que las sibilancias superan el umbral. Está presente en el StripDeEssPanel del Channel Strip tanto para RX como para TX. El applet acoplado ClientDeEssApplet omite este mando.

**Release** — la rapidez con la que la ganancia regresa después de que las sibilancias caen por debajo del umbral. Está presente en el StripDeEssPanel del Channel Strip tanto para RX como para TX. El applet acoplado ClientDeEssApplet omite este mando.

## Atenuación por bypass

Cuando la etapa DESS está en bypass a través del widget CHAIN, todo el mosaico del applet del de-esser se renderiza con opacidad reducida (aproximadamente el 55 % del brillo completo). Esto coincide con el efecto de atenuación aplicado a la curva EQ cuando esa etapa está en bypass. La opacidad completa se restaura tan pronto como la etapa se reactiva.

## Consejos

- El umbral interactúa con Amount (`ClientDeEssTxAmountDb`). Ajuste primero el umbral, luego ajuste Amount al gusto. Consulte [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md).
- Si no está seguro de dónde están los picos de sus sibilancias en frecuencia, localícelos primero antes de finalizar el umbral. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- Observar la barra Gain-reduction en tiempo real mientras habla es la forma más confiable de juzgar la colocación del umbral. Consulte [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Solución de problemas

- **La barra Gain-reduction se llena continuamente, incluso en vocales** — Thresh está demasiado bajo. Súbalo (en el sentido de las agujas del reloj) hasta que la barra esté vacía durante el habla sin sibilancias.
- **La barra Gain-reduction nunca se mueve, incluso en sonidos fuertes de 'S'** — Thresh está demasiado alto, o la banda de sibilancias (Freq, Q) no está centrada en las frecuencias problemáticas. Aumente el nivel de la banda bajando Thresh, o revise Freq. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- **El de-esser parece no hacer nada en absoluto** — confirme que la etapa DESS está habilitada en el widget CHAIN. Consulte [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md).
- **El mosaico del applet aparece atenuado** — la etapa DESS está actualmente en bypass en el widget CHAIN. Haga clic único en la etapa en el widget CHAIN para reactivarla y restaurar el brillo completo.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
- [Opening the RX de-esser panel](opening-the-rx-de-esser-panel.md)
