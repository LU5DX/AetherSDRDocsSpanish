# Ajustar la banda de cadena lateral con Q

El mando Q controla la anchura o estrechez del filtro de paso de banda de la cadena lateral alrededor de la frecuencia central de sibilancia. Una Q más alta enfoca la atenuación en una porción más estrecha del espectro; una Q más baja afecta a una banda más amplia. Ajuste Q después de localizar el pico de sibilancia con Freq para que el de-esser ataque exactamente el contenido correcto sin apagar las consonantes cercanas.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada y visible. Aparece como un subcontenedor dentro del contenedor principal Aetherial Audio (TXDSP).
- Si el applet no es visible, abra el Aetherial Audio Channel Strip, que aloja los controles del de-esser directamente. El editor flotante independiente "Aetherial De-Esser — TX" ya no existe.
- Para omitir el de-esser, haga clic una vez en la etapa DESS en el widget CHAIN. Cuando está omitido, el mosaico completo del applet se atenúa a aproximadamente un 55 % de opacidad como indicador visual.
- Ajuste la frecuencia central con Freq antes de afinar Q. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- El de-esser está disponible en dos instancias específicas por lateral: TX (para audio transmitido) y RX (para audio recibido). La versión TX está etiquetada como "Aetherial De-Esser" y la versión RX como "Aetherial De-Esser — RX". Ambas comparten controles y comportamiento idénticos. La instancia RX es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Abra el applet Aetherial De-Esser dentro del Aetherial Audio Channel Strip. Use **showForTx()** para acceder a la instancia TX o **showForRx()** para acceder a la instancia RX.
2. Localice el mando **Q** en la fila de cuatro mandos de sintonía.
3. Gire **Q** en el sentido de las agujas del reloj para aumentar el valor y estrechar la banda de la cadena lateral, o en sentido contrario para disminuir el valor y ensancharla.
4. Observe la curva de respuesta de la cadena lateral: el pico de paso de banda se ensancha o se vuelve más nítido a medida que cambia Q.
5. Mientras transmite o dice una frase con sibilantes, observe la barra de reducción de ganancia para confirmar que el de-esser sigue disparándose con el ancho de banda ajustado. Consulte [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Función de cada control

| Control                  | Valor predeterminado                                                                                                                                                                                                                               | Rango válido                                                                                                                                                                                                                                          |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Q**                    | 2.00                                                                                                                                                                                                                                               | 0.5 a 5.0                                                                                                                                                                                                                                             |
| Curva de respuesta de la cadena lateral | —                                                                                                                                                                                                                                                  | —                                                                                                                                                                                                                                                     |
| Barra de reducción de ganancia       | —                                                                                                                                                                                                                                                  | 0 a 24 dB GR                                                                                                                                                                                                                                         |
| Attack                   | 1.0 ms                                                                                                                                                                                                                                             | 0.1 a 30.0 ms                                                                                                                                                                                                                                        |
| Release                  | 100 ms                                                                                                                                                                                                                                             | 10.0 a 500.0 ms                                                                                                                                                                                                                                      |
| Slope                    | 24 dB/oct (2 etapas). Cicla el conteo de cascada de paso de banda de la cadena lateral. Cada etapa agrega 12 dB/oct de pendiente fuera de la banda sibilante. Mayor pendiente = muesca efectiva más estrecha, menos daño colateral en la banda media en frases con muchas "S". | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas). Se presenta como un botón pulsador etiquetado "N dB/oct" en la columna izquierda del StripDeEssPanel flotante, anclado debajo del mando Thresh. Presente tanto para rutas TX como RX. Persistido como ClientDeEssTxSlopeStages / ClientDeEssRxSlopeStages. |

## Entrada de valor mediante editor de texto en línea

Todos los mandos del Aetherial De-Esser admiten la entrada numérica directa a través de un editor de texto en línea:

1. **Active el editor**: Haga clic en el texto del valor actual de cualquier mando. El área de valor gana el foco y aparece un sutil recuadro oscuro con un borde cian, indicando el modo de edición.
2. **Introduzca un valor**: Escriba el valor numérico deseado. El editor acepta formatos decimales adaptados a la configuración regional (p. ej., "12,5" en configuraciones de coma decimal) y tolera caracteres adicionales como etiquetas de unidad (p. ej., "2.00" o "2.00 ms").
3. **Confirme el valor**: Presione **Enter** o haga clic en cualquier lugar fuera del editor. El valor se ajusta al rango válido del mando y se aplica inmediatamente.
4. **Cancele**: Presione **Escape** para revertir al valor anterior sin confirmar.

Esta función proporciona un ajuste preciso en un solo paso sin girar el mando, especialmente útil para recuperar configuraciones guardadas o ajustar un valor conocido.

## Atenuación por omisión

Cuando la etapa DESS se omite mediante un solo clic en el widget CHAIN, el mosaico completo del applet se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el comportamiento de atenuación utilizado en la curva de ecualización y proporciona una indicación clara de un vistazo de que la etapa está inactiva. Haga clic nuevamente en la etapa DESS en el widget CHAIN para reactivarla y restaurar la opacidad completa.

## Slope (inclinación del filtro de muesca)

El botón **Slope** controla cuántas etapas biquad de paso de banda en cascada utiliza la cadena lateral. Cada etapa agrega 12 dB/oct de pendiente fuera de la banda sibilante. Haga clic en el botón para recorrer las opciones: 12 → 24 → 36 → 48 dB/oct (1 a 4 etapas). Una pendiente más alta estrecha la muesca efectiva, reduciendo la atenuación colateral en el contenido de la banda media del habla durante frases con muchas "S".

El botón Slope aparece únicamente en el StripDeEssPanel flotante, anclado en la parte inferior de la columna izquierda de mandos debajo del mando Thresh. No está presente en el applet Aetherial De-Esser acoplado. Slope se persiste de forma independiente para TX y RX con las claves `ClientDeEssTxSlopeStages` y `ClientDeEssRxSlopeStages`.

## Consejos

- Comience con el valor predeterminado de 2.00 y aumente Q solo si la atenuación se está extendiendo a vocales u otras consonantes adyacentes a la banda de sibilancia.
- Los valores de Q muy altos (por encima de 4.0) pueden hacer que el de-esser no detecte sibilantes ligeramente descentradas. Si la GR deja de dispararse de manera fiable, reduzca Q ligeramente o vuelva a barrer Freq.
- La curva de respuesta proporciona retroalimentación visual inmediata: úsela para juzgar si la campana es demasiado ancha o demasiado aguda antes de confirmar una configuración.
- Los ajustes se guardan de forma independiente para las instancias TX y RX mediante claves de configuración separadas: `ClientDeEssTxQ` para TX y `ClientDeEssRxQ` para RX.
- Use el editor de valor en línea (haga clic en el valor actual) para una entrada numérica precisa cuando sepa exactamente la Q que necesita.
- Combine un Slope más alto (36 o 48 dB/oct) con una Q moderada para concentrar la acción del de-esser solo en frecuencias sibilantes puras, dejando intactas las consonantes adyacentes.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
