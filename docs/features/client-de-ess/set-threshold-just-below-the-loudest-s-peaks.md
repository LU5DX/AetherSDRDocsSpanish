# Ajustar el umbral justo por debajo de los picos de 'S' más fuertes

Esta página explica cómo ajustar el mando Thresh para que el de-esser actúe solo sobre sibilancia genuina y deje intacto el habla más suave. Un umbral bien colocado es la diferencia entre un de-essing transparente y un bombeo audible.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN. Consulte [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md).
- El applet Aetherial De-Esser debe estar visible en el panel de applets (subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP)).
- Necesita una forma de transmitir o monitorear su propio audio de transmisión para que el habla genuina llegue a la cadena lateral del de-esser.

## Pasos

1. Abra los controles del de-esser: abra el Aetherial Audio Channel Strip, o trabaje directamente con el mando Thresh en el applet acoplado.
2. Comience a hablar por su micrófono, repitiendo una frase sibilante (una con sonidos repetidos de 'S' y 'T' funciona bien).
3. Observe la barra de Gain-reduction. Si muestra un relleno rojo suave durante vocales y consonantes normales (no solo en picos de 'S'), el umbral está demasiado bajo. Si nunca se mueve durante sonidos de 'S' fuertes, el umbral está demasiado alto.
4. Gire el mando Thresh en sentido horario para aumentar el umbral (hacia 0.0 dB) hasta que la barra de Gain-reduction permanezca vacía durante el habla normal.
5. Luego, gire Thresh lentamente en sentido antihorario (hacia −60.0 dB) hasta que la barra de Gain-reduction comience a llenarse solo en sus picos de 'S' más fuertes y nada más.
6. Verifique: hable normalmente durante una oración completa. La barra de Gain-reduction debe estar vacía la mayor parte del tiempo y llenarse brevemente solo en sibilantes duras.

## Qué hace cada control

| Control            | Por defecto | Rango válido    |
|--------------------|-------------|-----------------|
| Thresh             | −30.0 dB    | −60.0 a 0.0 dB  |
| Gain-reduction bar | —           | 0 a 24 dB GR    |
| Freq               | 6000 Hz     | 1000 a 12000 Hz |
| Q                  | 2.00        | 0.5 a 5.0       |
| Amount             | −6.0 dB     | −24.0 a 0.0 dB  |
| Attack             | 1.0 ms      | 0.1 a 30.0 ms   |
| Release            | 100 ms      | 10.0 a 500.0 ms |

**Thresh** — el nivel por encima del cual el de-esser comienza a atenuar la banda de sibilancia. Aumentar este valor (hacia 0.0 dB) hace que el de-esser actúe solo sobre la sibilancia más fuerte. Reducirlo (hacia −60.0 dB) hace que el de-esser se active con señales progresivamente más suaves.

**Gain-reduction bar** — una barra horizontal roja suave que se llena desde la derecha para mostrar la atenuación actual. La escala va de 0 a 24 dB. Una marca indica la posición de −6 dB, que es el valor predeterminado de Amount. La barra se actualiza aproximadamente 30 veces por segundo.

**Freq** — establece la frecuencia central de la banda de sibilancia (1000 a 12000 Hz, mapeo logarítmico). Valor predeterminado 6000 Hz. Las etiquetas muestran "6.0 kHz" por encima de 1 kHz y "N Hz" por debajo. Presione Enter o haga clic fuera después de escribir un valor para confirmarlo.

**Q** — establece el ancho de banda de la banda de sibilancia (0.5 a 5.0, mapeo lineal). Q más alto = banda más estrecha. Valor predeterminado 2.00. Formato de etiqueta "X.XX". Presione Enter o haga clic fuera después de escribir un valor para confirmarlo.

**Amount** — atenuación máxima aplicada en el pico de sibilancia (−24.0 a 0.0 dB, mapeo lineal). Los valores son negativos (o cero) porque representan reducción. Valor predeterminado −6.0 dB. Presione Enter o haga clic fuera después de escribir un valor para confirmarlo.

**Attack** — qué tan rápido responde el de-esser una vez que la sibilancia supera el umbral (0.1 a 30.0 ms, mapeo exponencial). Presente en el Channel Strip StripDeEssPanel tanto para RX como para TX. El applet acoplado ClientDeEssApplet omite este mando.

**Release** — qué tan rápido regresa la ganancia después de que la sibilancia cae por debajo del umbral (10.0 a 500.0 ms, mapeo exponencial). Presente en el Channel Strip StripDeEssPanel tanto para RX como para TX. El applet acoplado ClientDeEssApplet omite este mando.

## Curva de respuesta de la cadena lateral

El indicador de curva de respuesta de la cadena lateral dibuja la respuesta del filtro de paso de banda con un punto vivo en la frecuencia central actual. El eje de frecuencia está etiquetado con líneas de cuadrícula principales en 100, 500, 1k, 2k, 3k, 4k, 5k, 6k, 7k, 8k, 9k, 10k, 11k y 12k Hz. Estas etiquetas se dibujan como objetos de texto estático de alto rendimiento almacenados en caché después de la primera representación. Las etiquetas aparecen solo cuando el widget de curva no está en modo compacto.

El punto de frecuencia central descansa en el pico de la curva, marcando la frecuencia central de sibilancia actualmente sintonizada.

## Edición de valor en línea

Cada mando de sintonización (Freq, Q, Thresh, Amount, Attack, Release) admite la entrada de valor directa. Haga clic en el valor mostrado para activar una superposición de editor en línea. El editor aparece como un campo de texto con borde cian sobre un fondo oscuro.

- **Enter** — confirma el valor escrito y cierra el editor.
- **Clic en otro lugar (pérdida de foco)** — confirma el valor escrito y cierra el editor.
- **Escape** — descarta el valor escrito y vuelve al valor anterior.

El editor en línea acepta formatos de número según la configuración regional (por ejemplo, "12,5" en configuraciones regionales que usan coma decimal). También tolera texto adicional como sufijos de unidad ("6 kHz", "−30 dB") eliminando caracteres no numéricos antes de analizar. Si el análisis falla, el editor vuelve silenciosamente al último valor mostrado válido.

El editor está oculto por defecto en el applet acoplado ClientDeEssApplet, y visible por defecto en el Channel Strip StripDeEssPanel. Cuando está oculto, los valores de los mandos se muestran solo como texto pintado.

Esta función es proporcionada por `ClientCompKnob`, que también es utilizado por el compresor y otros widgets de procesamiento de audio en el Aetherial Audio Channel Strip. Consulte [Inline edit knob values](inline-edit-knob-values.md).

## Atenuación por bypass

Cuando la etapa DESS está en bypass a través del widget CHAIN, el mosaico completo del applet de-esser se renderiza con opacidad reducida (aproximadamente 55 % del brillo completo). Esto coincide con el efecto de atenuación aplicado a la curva del ecualizador cuando esa etapa está en bypass. La opacidad completa se restaura tan pronto como la etapa se vuelve a habilitar.

## Consejos

- El umbral interactúa con Amount (`ClientDeEssTxAmountDb`). Ajuste primero el umbral, luego configure Amount al gusto. Consulte [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md).
- Si no está seguro de dónde están sus picos de sibilancia en frecuencia, localícelos primero antes de finalizar el umbral. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- Observar la barra de Gain-reduction en tiempo real mientras habla es la forma más fiable de juzgar la colocación del umbral. Consulte [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Solución de problemas

- **La barra de Gain-reduction se llena continuamente, incluso en vocales** — Thresh está demasiado bajo. Súbalo (en sentido horario) hasta que la barra esté vacía durante el habla no sibilante.
- **La barra de Gain-reduction nunca se mueve, incluso en sonidos de 'S' fuertes** — Thresh está demasiado alto, o la banda de sibilancia (Freq, Q) no está centrada en las frecuencias problemáticas. Aumente el nivel de la banda bajando Thresh, o revise Freq. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- **El de-esser parece no hacer nada en absoluto** — confirme que la etapa DESS esté habilitada en el widget CHAIN. Consulte [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md).
- **El mosaico del applet aparece atenuado** — la etapa DESS está actualmente en bypass en el widget CHAIN. Haga clic una vez en la etapa en el widget CHAIN para volver a habilitarla y restaurar el brillo completo.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
- [Opening the RX de-esser panel](opening-the-rx-de-esser-panel.md)
- [Inline edit knob values](inline-edit-knob-values.md)
