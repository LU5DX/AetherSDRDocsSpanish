# Ajustar la banda de la cadena lateral con Q (estrechar o ensanchar)

El mando **Q** controla la amplitud del filtro de paso de banda de la cadena lateral en torno a la frecuencia central de sibilancia. Un valor de Q más alto concentra la atenuación en una porción más estrecha del espectro; un valor de Q más bajo afecta a una banda más amplia. Ajuste Q después de localizar el pico de sibilancia con Freq, para que el de-esser ataque exactamente el contenido correcto sin atenuar consonantes cercanas.

## Antes de comenzar

- La etapa Aetherial De-Esser (DESS) debe estar habilitada y visible. Aparece como un subcontenedor dentro del contenedor principal Aetherial Audio (TXDSP).
- Si el applet no es visible, abra el Aetherial Audio Channel Strip, que aloja los controles del de-esser directamente. El editor flotante independiente "Aetherial De-Esser — TX" ya no existe.
- Para omitir el de-esser, haga clic una vez en la etapa DESS dentro del widget CHAIN. Cuando está omitido, el mosaico completo del applet se atenúa aproximadamente al 55 % de opacidad como indicador visual.
- Ajuste la frecuencia central con Freq antes de afinar Q. Consulte [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md).
- El de-esser está disponible en dos instancias específicas por lado: TX (para audio transmitido) y RX (para audio recibido). La versión TX está etiquetada como "Aetherial De-Esser" y la versión RX como "Aetherial De-Esser — RX". Ambas comparten controles y comportamiento idénticos. La instancia RX es accesible a través del Aetherial Audio Channel Strip.

## Pasos

1. Abra el applet Aetherial De-Esser dentro del Aetherial Audio Channel Strip. Use **showForTx()** para acceder a la instancia TX o **showForRx()** para acceder a la instancia RX.
2. Localice el mando **Q** en la fila de cuatro mandos de sintonización.
3. Gire **Q** en el sentido de las agujas del reloj para aumentar el valor y estrechar la banda de la cadena lateral, o en sentido contrario para disminuir el valor y ensancharla.
4. Observe la curva de respuesta de la cadena lateral: el pico de paso de banda se ensancha o se afina a medida que cambia Q.
5. Mientras transmite o pronuncia una frase con sibilantes, observe la barra de reducción de ganancia para confirmar que el de-esser sigue activándose con el ancho de banda ajustado. Consulte [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md).

## Función de cada control

| Control                    | Valor por defecto | Rango válido    | Comportamiento                                                                                                                              |
|----------------------------|-------------------|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| **Q**                      | 2.00              | 0.5 a 5.0       | Mapeo lineal. Establece el ancho de banda de la sibilancia: Q más alto = banda más estrecha. Etiqueta 'X.XX'.                             |
| Curva de respuesta de la cadena lateral | —       | —               | Respuesta de paso de banda en modo compacto. Dibuja la respuesta del filtro de paso de banda con un punto móvil en la frecuencia central actual. Las etiquetas de los ejes (100, 500, 1k, etc.) se renderizan usando QStaticText para mejorar el rendimiento. |
| Barra de reducción de ganancia          | —       | 0 a 24 dB GR    | Barra horizontal de color rojo suave, rellena desde la derecha. La escala máxima es 24 dB; una marca indica la cantidad típica de -6 dB. Se actualiza a ~30 Hz. |
| Ataque                     | 1.0 ms             | 0.1 a 30.0 ms   | Mapeo exponencial (0.1 * 300^n). Define la rapidez con la que responde el de-esser una vez que la sibilancia supera el umbral. Presente en ambas instancias de TX y RX del Channel Strip. El applet ClientDeEssApplet acoplado omite este mando. |
| Liberación                 | 100 ms             | 10.0 a 500.0 ms | Mapeo exponencial (10 * 50^n). Define la rapidez con la que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Presente en ambas instancias de TX y RX del Channel Strip. El applet ClientDeEssApplet acoplado omite este mando. |

## Ingreso de valores mediante editor de texto en línea

A partir de la versión 26.5.2.1, todos los mandos del Aetherial De-Esser admiten el ingreso numérico directo a través de un editor de texto en línea:

1. **Active el editor**: Haga clic en el texto del valor actual de cualquier mando. El área del valor gana el foco y aparece un sutil oscurecimiento interior con un borde cian, indicando el modo de edición.
2. **Ingrese un valor**: Escriba el valor numérico deseado. El editor acepta formatos decimales adaptados a la configuración regional (por ejemplo, "12,5" en configuraciones regionales con coma decimal) y tolera caracteres adicionales como etiquetas de unidad (por ejemplo, "2.00" o "2.00 ms").
3. **Confirme el valor**: Presione **Enter** o haga clic fuera del editor. El valor se ajusta al rango válido del mando y se aplica inmediatamente.
4. **Cancele**: Presione **Escape** para revertir al valor anterior sin confirmar.

Esta función permite un ajuste preciso en un solo paso sin necesidad de girar el mando, especialmente útil para recuperar configuraciones guardadas o coincidir con un valor conocido.

## Atenuación por omisión

Cuando la etapa DESS se omite mediante un solo clic en el widget CHAIN, el mosaico completo del applet se renderiza con opacidad reducida (aproximadamente 55 %). Esto coincide con el comportamiento de atenuación utilizado en la curva de EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. Haga clic nuevamente en la etapa DESS dentro del widget CHAIN para reactivarla y restaurar la opacidad completa.

## Consejos

- Comience con el valor predeterminado de 2.00 y aumente Q solo si la atenuación se está extendiendo a las vocales u otras consonantes adyacentes a la banda de sibilancia.
- Valores de Q muy altos (superiores a 4.0) pueden hacer que el de-esser pase por alto sibilantes ligeramente descentrados. Si la reducción de ganancia deja de activarse de manera fiable, reduzca Q ligeramente o vuelva a barrer Freq.
- La curva de respuesta proporciona retroalimentación visual inmediata; úsela para juzgar si la campana es demasiado ancha o demasiado estrecha antes de confirmar un ajuste.
- Los ajustes se guardan de forma independiente para las instancias TX y RX mediante claves de configuración separadas: `ClientDeEssTxQ` para TX y `ClientDeEssRxQ` para RX.
- Use el editor de valor en línea (haga clic en el valor actual) para el ingreso numérico preciso cuando conozca el valor Q exacto que necesita.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
