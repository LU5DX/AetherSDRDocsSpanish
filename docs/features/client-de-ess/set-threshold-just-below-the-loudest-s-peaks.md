# Ajuste el umbral justo por debajo de los picos de 'S' más fuertes

Esta página explica cómo ajustar el mando Thresh para que el de-esser actúe solo sobre la sibilancia genuina y deje el habla más suave sin alterar. Un umbral bien colocado marca la diferencia entre un de-essing transparente y un bombeo audible.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN. Consulte [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md).
- El applet Aetherial De-Esser debe ser visible en el panel de applets (subcontenedor "Aetherial De-Esser" dentro del contenedor principal Aetherial Audio (TXDSP)).
- Necesita una forma de transmitir o monitorear su propio audio de TX para que el habla genuina llegue a la cadena lateral (sidechain) del de-esser.

## Pasos

1. Abra los controles del de-esser: abra el Aetherial Audio Channel Strip, o trabaje directamente con el mando Thresh en el applet acoplado.
2. Comience a hablar por su micrófono, repitiendo una frase con sibilantes — algo con sonidos repetidos de 'S' y 'T' funciona bien.
3. Observe la barra Gain-reduction. Si muestra un relleno rojo suave durante las vocales y consonantes normales (no solo en los picos de 'S'), el umbral está demasiado bajo. Si nunca se mueve durante los sonidos de 'S' fuertes, el umbral está demasiado alto.
4. Gire el mando Thresh en el sentido de las agujas del reloj para subir el umbral (hacia 0.0 dB) hasta que la barra Gain-reduction permanezca vacía durante el habla normal.
5. Luego, gire Thresh lentamente en sentido contrario a las agujas del reloj (hacia −60.0 dB) hasta que la barra Gain-reduction apenas comience a llenarse en sus picos de 'S' más fuertes y no más.
6. Verifique: hable normalmente con una frase completa. La barra Gain-reduction debería estar vacía la mayor parte del tiempo y llenarse brevemente solo en las sibilantes duras.

## Función de cada control

| Control            | Valor predeterminado | Rango válido                             |
|--------------------|----------------------|------------------------------------------|
| Thresh             | −30.0 dB             | −60.0 a 0.0 dB                           |
| Barra Gain-reduction | —                  | 0 a 24 dB GR                             |
| Freq               | 6000 Hz              | 1000 a 12000 Hz                          |
| Q                  | 2.00                 | 0.5 a 5.0                                |
| Amount             | −6.0 dB              | −24.0 a 0.0 dB                           |
| Attack             | 1.0 ms               | 0.1 a 30.0 ms                            |
| Release            | 100 ms               | 10.0 a 500.0 ms                          |
| Slope              | 24 dB/oct (2 etapas) | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas) |

**Thresh** — el nivel por encima del cual el de-esser comienza a atenuar la banda de sibilancia. Aumentar este valor (hacia 0.0 dB) hace que el de-esser actúe solo sobre la sibilancia más fuerte. Reducirlo (hacia −60.0 dB) hace que el de-esser se active con señales progresivamente más suaves.

**Barra Gain-reduction** — una tira roja suave horizontal que se llena desde la derecha para mostrar la atenuación actual. La escala va de 0 a 24 dB. Una marca indica la posición de −6 dB, que es el valor predeterminado de Amount. La barra se actualiza aproximadamente 30 veces por segundo. El color de la barra proviene del valor `color.accent.danger` del tema.

**Freq** — establece la frecuencia central de la banda de sibilancia (1000 a 12000 Hz, mapeo logarítmico). Valor predeterminado 6000 Hz. Las etiquetas muestran "6.0 kHz" por encima de 1 kHz y "N Hz" por debajo. Presione Enter o haga clic fuera después de escribir un valor para confirmarlo. Clave de configuración: `ClientDeEssTxFrequencyHz`.

**Q** — establece el ancho de banda de la banda de sibilancia (0.5 a 5.0, mapeo lineal). Q más alto = banda más estrecha. Valor predeterminado 2.00. Formato de etiqueta "X.XX". Presione Enter o haga clic fuera después de escribir un valor para confirmarlo. Clave de configuración: `ClientDeEssTxQ`.

**Amount** — atenuación máxima aplicada en el pico de sibilancia (−24.0 a 0.0 dB, mapeo lineal). Los valores son negativos (o cero) porque representan reducción. Valor predeterminado −6.0 dB. Presione Enter o haga clic fuera después de escribir un valor para confirmarlo. Clave de configuración: `ClientDeEssTxAmountDb`.

**Attack** — la rapidez con la que responde el de-esser cuando la sibilancia cruza el umbral (0.1 a 30.0 ms, mapeo exponencial). Presente en el Channel Strip StripDeEssPanel tanto para RX como para TX. El applet acoplado ClientDeEssApplet omite este mando. Clave de configuración: `ClientDeEssTxAttackMs`.

**Release** — la rapidez con la que la ganancia regresa después de que la sibilancia cae por debajo del umbral (10.0 a 500.0 ms, mapeo exponencial). Presente en el Channel Strip StripDeEssPanel tanto para RX como para TX. El applet acoplado ClientDeEssApplet omite este mando. Clave de configuración: `ClientDeEssTxReleaseMs`.

**Slope** — establece el recuento de cascada del filtro de paso de banda de la cadena lateral. Cada etapa agrega 12 dB/oct de atenuación fuera de la banda de sibilancia. Una pendiente más alta = muesca efectiva más estrecha, menos atenuación colateral de la banda media en frases con muchas 'S'. Haga clic en el botón para alternar entre 12 → 24 → 36 → 48 dB/oct (1 a 4 etapas). Presente en el Channel Strip StripDeEssPanel (columna izquierda, parte inferior). Se persiste como `ClientDeEssTxSlopeStages` para TX y `ClientDeEssRxSlopeStages` para RX.

## Curva de respuesta de la cadena lateral

El indicador Sidechain response curve dibuja la respuesta del filtro de paso de banda con un punto móvil en la frecuencia central actual. El eje de frecuencia está etiquetado con líneas de cuadrícula principales en 100, 500, 1k, 2k, 3k, 4k, 5k, 6k, 7k, 8k, 9k, 10k, 11k y 12k Hz. Estas etiquetas se dibujan como objetos de texto estático de alto rendimiento almacenados en caché después del primer trazo. Las etiquetas aparecen solo cuando el widget de curva no está en modo compacto.

Los colores de la curva y la cuadrícula provienen del tema: `color.background.0`, `color.background.1`, `color.text.label`, `color.accent.danger` y `color.accent.dim`. El color de la curva utiliza un rojo suave ("banda de sibilancia").

El punto de frecuencia central descansa en el pico de la curva, marcando la frecuencia central de sibilancia actualmente sintonizada. El punto utiliza `color.accent.dim` para el resplandor y `color.text.primary` para el núcleo.

La curva se actualiza automáticamente cuando se cambian las etapas de Slope para reflejar la atenuación más pronunciada o más suave.

## Edición de valor en línea

Cada mando de sintonía (Freq, Q, Thresh, Amount, Attack, Release) admite la entrada directa de valores. Haga clic en el texto del valor mostrado para activar un editor superpuesto en línea. El editor aparece como un campo de texto con borde cian sobre un fondo oscuro.

- **Enter** — confirma el valor escrito y cierra el editor.
- **Haga clic en otro lugar (pérdida de foco)** — confirma el valor escrito y cierra el editor.
- **Escape** — descarta el valor escrito y revierte al valor anterior.

El editor en línea acepta formatos de número según la configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal). También tolera texto adicional, como sufijos de unidad ("6 kHz", "−30 dB"), eliminando los caracteres no numéricos antes de analizar. Si el análisis falla, el editor se revierte silenciosamente al último valor mostrado válido.

El editor está oculto de forma predeterminada en el ClientDeEssApplet acoplado, y visible de forma predeterminada en el Channel Strip StripDeEssPanel. Cuando está oculto, los valores de los mandos se muestran solo como texto pintado.

Esta función es proporcionada por `ClientCompKnob`, que también es utilizado por el Compressor y otros widgets de procesamiento de audio en el Aetherial Audio Channel Strip. Consulte Inline edit knob values.

## Atenuación por bypass

Cuando la etapa DESS está en bypass a través del widget CHAIN, el mosaico completo del applet del de-esser se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación aplicado a la curva del EQ cuando esa etapa está en bypass. La opacidad completa se restablece tan pronto como la etapa se vuelve a habilitar.

## Colores de mandos conscientes del tema

A partir de la versión v26.6.1, los mandos del de-esser leen sus colores del espacio de nombres `color.knob.*` del sistema de temas:

| Clave del tema | Componente | Descripción |
|----------------|------------|-------------|
| `color.knob.background` | Fondo del anillo | La parte no iluminada del arco del mando |
| `color.knob.foreground` | Arco del anillo | La parte iluminada del arco del mando |
| `color.knob.handle` | Indicador | La línea indicadora del mando |
| `color.text.secondary` | Etiqueta | La etiqueta del componente del mando |
| `color.text.primary` | Valor | El valor numérico actual |

El contenedor del applet `applet/deess` tiene anulaciones de color por applet. Si un tema define una sección `applet/deess`, sus colores tienen prioridad sobre los valores globales de `color.knob.*`.

## Consejos

- El umbral interactúa con Amount (`ClientDeEssTxAmountDb`). Ajuste primero el umbral, luego ajuste Amount al gusto. Consulte [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md).
- Si no está seguro de dónde están los picos de sibilancia en frecuencia, localícelos primero antes de finalizar el umbral. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- Observar la barra Gain-reduction en tiempo real mientras habla es la forma más fiable de juzgar la colocación del umbral. Consulte [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md).
- Utilice valores de Slope más altos (36 o 48 dB/oct) cuando tenga pasajes densos de sibilancia para minimizar la atenuación colateral de la banda media del habla. Un Slope de 24 dB/oct es un buen punto de partida para la mayoría de las voces.

## Solución de problemas

- **La barra Gain-reduction se llena continuamente, incluso en las vocales** — Thresh está demasiado bajo. Súbalo (en el sentido de las agujas del reloj) hasta que la barra esté vacía durante el habla no sibilante.
- **La barra Gain-reduction nunca se mueve, incluso en sonidos de 'S' fuertes** — Thresh está demasiado alto, o la banda de sibilancia (Freq, Q) no está centrada en las frecuencias problemáticas. Aumente el nivel de la banda bajando Thresh, o revise Freq. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- **El de-esser parece no hacer nada en absoluto** — confirme que la etapa DESS está habilitada en el widget CHAIN. Consulte [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md).
- **El mosaico del applet aparece atenuado** — la etapa DESS está actualmente en bypass en el widget CHAIN. Haga clic una vez en la etapa en el widget CHAIN para volver a habilitarla y restaurar el brillo completo.

## Relacionado

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
- Opening the RX de-esser panel
- Inline edit knob values
