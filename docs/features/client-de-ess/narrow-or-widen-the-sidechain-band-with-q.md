# Ajustar la banda de la cadena lateral con Q (factor de calidad)

El mando Q controla la anchura o estrechez del filtro de paso de banda de la cadena lateral alrededor de la frecuencia central de sibilancia. Un Q más alto concentra la atenuación en una porción más ajustada del espectro; un Q más bajo afecta a una banda más ancha. Ajuste Q después de localizar el pico de sibilancia con Freq para que el de-esser apunte exactamente al contenido correcto sin apagar las consonantes cercanas.

## Antes de empezar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada y visible. Aparece como un subcontenedor dentro del contenedor principal Aetherial Audio (TXDSP).
- Si el applet no está visible, abra el Aetherial Audio Channel Strip, que alberga los controles del de-esser directamente. El panel flotante StripDeEssPanel (accesible a través del Channel Strip) incluye el botón Slope; el applet acoplado Aetherial De-Esser omite los mandos/botones Attack, Release y Slope.
- Para omitir el de-esser, haga clic una vez en la etapa DESS en el widget CHAIN. Cuando está omitido, todo el mosaico del applet se oscurece aproximadamente al 55 % de opacidad como indicador visual.
- Ajuste la frecuencia central con Freq antes de ajustar finamente Q. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- El de-esser está disponible en dos instancias específicas por lateral: TX (para audio transmitido) y RX (para audio recibido). La versión TX está etiquetada como "Aetherial De-Esser" y la versión RX como "Aetherial De-Esser — RX". Ambas comparten controles y comportamiento idénticos. La instancia RX es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Abra el applet Aetherial De-Esser dentro del Aetherial Audio Channel Strip. Use **showForTx()** para acceder a la instancia TX o **showForRx()** para acceder a la instancia RX.
2. Localice el mando **Q** en la fila de seis mandos de sintonía (Freq, Q, Thresh, Amount, Attack, Release). Nota: En el ClientDeEssApplet acoplado, solo están presentes Freq, Q, Thresh y Amount; Attack y Release se omiten.
3. Gire **Q** en el sentido de las agujas del reloj para aumentar el valor y estrechar la banda de la cadena lateral, o en sentido contrario para disminuir el valor y ensancharla.
4. Observe la curva de respuesta de la cadena lateral: el pico de paso de banda se ensancha o se agudiza a medida que cambia Q.
5. Mientras transmite o dice una frase con sibilancia, observe la barra de reducción de ganancia para confirmar que el de-esser sigue activándose con el ancho de banda ajustado. Consulte [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Función de cada control

| Control                  | Valor predeterminado                                                                                                                                                                                                                    | Rango válido                                                                                                                                                                                                                                                                   |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Freq**                 | 6000 Hz                                                                                                                                                                                                                                 | 1000 a 12000 Hz                                                                                                                                                                                                                                                                |
| **Q**                    | 2.00                                                                                                                                                                                                                                    | 0.5 a 5.0                                                                                                                                                                                                                                                                      |
| **Thresh**               | -30.0 dB                                                                                                                                                                                                                                | -60.0 a 0.0 dB                                                                                                                                                                                                                                                                 |
| **Amount**               | -6.0 dB                                                                                                                                                                                                                                 | -24.0 a 0.0 dB                                                                                                                                                                                                                                                                 |
| **Attack**               | 1.0 ms (presente solo en el Channel Strip StripDeEssPanel RX y TX; omitido en el ClientDeEssApplet acoplado)                                                                                                                            | 0.1 a 30.0 ms                                                                                                                                                                                                                                                                  |
| **Release**              | 100 ms (presente solo en el Channel Strip StripDeEssPanel RX y TX; omitido en el ClientDeEssApplet acoplado)                                                                                                                            | 10.0 a 500.0 ms                                                                                                                                                                                                                                                                |
| Curva de respuesta       | —                                                                                                                                                                                                                                       | —                                                                                                                                                                                                                                                                              |
| Barra de reducción       | —                                                                                                                                                                                                                                       | 0 a 24 dB de GR                                                                                                                                                                                                                                                                |
| **Slope**                | 24 dB/oct (2 etapas). Cicla el recuento de cascadas de paso de banda de la cadena lateral. Cada etapa añade 12 dB/oct de pendiente fuera de la banda de sibilancia. Slope más alto = muesca efectiva más estrecha, menos daño colateral en la banda media en frases con muchas Ess. | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas). Presente como un botón pulsador etiquetado "N dB/oct" solo en el panel flotante StripDeEssPanel, anclado debajo del mando Thresh. Presente para ambas rutas TX y RX. Se persiste como ClientDeEssTxSlopeStages / ClientDeEssRxSlopeStages. |

## Introducción de valores mediante editor de texto en línea

Todos los mandos del Aetherial De-Esser admiten la entrada numérica directa a través de un editor de texto en línea:

1. **Active el editor**: Haga clic en el texto del valor actual de cualquier mando. El área de valor gana el foco y aparece un sutil recuadro oscuro con un borde cian, indicando el modo de edición.
2. **Introduzca un valor**: Escriba el valor numérico deseado. El editor acepta formatos decimales adaptados a la configuración regional (p. ej., "12,5" en configuraciones regionales que usan coma decimal) y tolera caracteres adicionales como etiquetas de unidad (p. ej., "2.00" o "2.00 ms").
3. **Confirme el valor**: Pulse **Enter** o haga clic en cualquier lugar fuera del editor. El valor se ajusta al rango válido del mando y se aplica inmediatamente.
4. **Cancele**: Pulse **Escape** para revertir al valor anterior sin confirmar.

Esta función proporciona un ajuste preciso en un solo paso sin girar el mando, especialmente útil para recuperar ajustes guardados o coincidir con un valor conocido.

## Atenuación por omisión

Cuando la etapa DESS se omite mediante un solo clic en el widget CHAIN, todo el mosaico del applet se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el comportamiento de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. Haga clic nuevamente en la etapa DESS en el widget CHAIN para reactivarla y restaurar la opacidad completa.

## Slope (inclinación del filtro de muesca)

El botón **Slope** controla cuántas etapas biquad de paso de banda en cascada utiliza la cadena lateral. Cada etapa añade 12 dB/oct de pendiente fuera de la banda de sibilancia. Haga clic en el botón para recorrer las opciones: 12 → 24 → 36 → 48 dB/oct (1 a 4 etapas). Una pendiente más alta estrecha la muesca efectiva, reduciendo la atenuación colateral en el contenido de banda media del habla durante frases con muchas Ess.

El botón Slope aparece solo en el panel flotante StripDeEssPanel, anclado en la parte inferior de la columna izquierda de mandos, debajo del mando Thresh. No está presente en el applet acoplado Aetherial De-Esser. Slope se persiste de forma independiente para TX y RX con las claves `ClientDeEssTxSlopeStages` y `ClientDeEssRxSlopeStages`.

## Consejos

- Comience con el valor predeterminado de 2.00 y aumente Q solo si la atenuación se está extendiendo a las vocales u otras consonantes adyacentes a la banda de sibilancia.
- Los valores de Q muy altos (por encima de 4.0) pueden hacer que el de-esser no detecte sibilancias ligeramente descentradas. Si GR deja de activarse de forma fiable, reduzca Q ligeramente o vuelva a barrer Freq.
- La curva de respuesta proporciona retroalimentación visual inmediata: úsela para juzgar si la campana es demasiado ancha o demasiado aguda antes de confirmar un ajuste.
- Los ajustes se guardan de forma independiente para las instancias TX y RX mediante claves de ajuste separadas: `ClientDeEssTxQ` para TX y `ClientDeEssRxQ` para RX.
- Use el editor de valores en línea (haga clic en el valor actual) para la entrada numérica precisa cuando sepa el Q exacto que necesita.
- Combine un Slope más alto (36 o 48 dB/oct) con un Q moderado para concentrar la acción del de-esser solo en frecuencias de sibilancia puras, dejando intactas las consonantes adyacentes.

## Relacionado

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
