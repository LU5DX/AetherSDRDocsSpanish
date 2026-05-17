# Barrer frecuencia para localizar el pico de sibilancia

Use el mando Freq para recorrer el rango de sibilancia mientras transmite o monitorea audio, observando la barra de reducción de ganancia para identificar la frecuencia que provoca la mayor reducción. Esto localiza el centro de la banda problemática de sibilancia antes de ajustar los valores finales de Q, Thresh y Amount.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado a través del widget CHAIN en el contenedor Aetherial Audio (TXDSP). El applet permanece oculto hasta que la etapa DESS esté activa.
- Necesita una fuente de audio en vivo — ya sea transmitiendo o enrutando audio a través de la cadena TX DSP — para que la barra de reducción de ganancia responda en tiempo real.
- Abra el applet del de-esser. El bypass y la habilitación se controlan con un solo clic en la etapa DESS en el widget CHAIN. La edición se realiza a través del Aetherial Audio Channel Strip.

## Pasos

1. Ajuste Thresh a un valor justo por debajo de sus picos típicos de sibilancia — un punto de partida de -30.0 dB (el predeterminado) funciona para la mayoría de las voces.
2. Ajuste Amount a un valor claramente audible, como -12.0 dB o inferior, para que la reducción de ganancia sea fácil de ver en la barra.
3. Hable o reproduzca audio que contenga sonidos sostenidos de "S" y "T" de forma continua en el micrófono.
4. Gire lentamente el mando Freq desde su valor predeterminado de 6.0 kHz hacia arriba o hacia abajo en el rango de 1000 a 12000 Hz.
5. Observe la barra de reducción de ganancia. La barra se llena más hacia la derecha — indicando la atenuación máxima — cuando Freq está centrado en la banda de sibilancia dominante.
6. Deténgase en el valor de Freq que produzca la lectura más alta de reducción de ganancia. Ese valor es su frecuencia central de sibilancia.
7. Una vez completado el barrido, regrese Amount a su valor operativo previsto (predeterminado -6.0 dB).

## Función de cada control

| Control                  | Predeterminado | Rango válido    |
|--------------------------|----------------|-----------------|
| Freq                     | 6000 Hz        | 1000 a 12000 Hz |
| Q                        | 2.00           | 0.5 a 5.0       |
| Thresh                   | -30.0 dB       | -60.0 a 0.0 dB  |
| Amount                   | -6.0 dB        | -24.0 a 0.0 dB  |
| Attack                   | 1.0 ms         | 0.1 a 30.0 ms   |
| Release                  | 100 ms         | 10.0 a 500.0 ms |
| Curva de respuesta de sidechain | —       | —               |
| Barra de reducción de ganancia | —       | 0 a 24 dB GR    |

**Nota:** Los mandos Attack y Release aparecen solo en el StripDeEssPanel del Channel Strip (tanto RX como TX). El ClientDeEssApplet acoplado omite estos controles.

## Ingreso directo de valores

Haga clic en la pantalla de valor de cualquier mando para revelar un editor de texto en línea. Escriba un valor numérico (incluyendo unidades o texto final) y presione Enter o haga clic en otra parte para confirmar. El valor se ajusta al rango válido del mando. Para cancelar, presione Escape — el mando vuelve a su valor anterior.

- El editor admite el análisis según la configuración regional, por lo que "12,5" funciona en configuraciones regionales con coma decimal.
- El texto final como "ms" o "dB" se elimina automáticamente.
- Mientras el editor está activo, los eventos de la rueda del ratón aún ajustan el mando normalmente.

## Etiquetas de ejes de la curva de respuesta de sidechain

El widget de curva dibuja las etiquetas del eje de frecuencia usando QStaticText para mejorar el rendimiento de renderizado. Las etiquetas se muestran como "100", "500", "1k", "2k", etc. El texto de la etiqueta se almacena en caché después de la primera pintura y se reutiliza en redibujos posteriores. Las etiquetas de los ejes se ocultan cuando el widget de curva está en modo compacto.

## Atenuación en bypass

Cuando la etapa DESS está en bypass a través del widget CHAIN, todo el mosaico del applet de de-esser se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve al brillo completo tan pronto como la etapa se vuelve a habilitar.

## Instancias RX y TX

El Aetherial De-Esser tiene configuraciones separadas para las rutas TX y RX. El Applet Panel acoplado muestra la copia TX etiquetada como "Aetherial De-Esser". La copia RX, etiquetada como "Aetherial De-Esser — RX", es accesible a través del StripDeEssPanel del Aetherial Audio Channel Strip.

El StripDeEssPanel en el Channel Strip se puede abrir para TX o RX. Cuando se abre para TX, el título de la ventana muestra "Aetherial De-Esser — TX". Cuando se abre para RX, el título de la ventana muestra "Aetherial De-Esser — RX". Cada instancia guarda y restaura de forma independiente sus propias configuraciones de mandos utilizando claves de configuración separadas:
- TX: `ClientDeEssTxFrequencyHz`, `ClientDeEssTxQ`, `ClientDeEssTxThresholdDb`, `ClientDeEssTxAmountDb`, `ClientDeEssTxAttackMs`, `ClientDeEssTxReleaseMs`
- RX: `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, `ClientDeEssRxThresholdDb`, `ClientDeEssRxAmountDb`, `ClientDeEssRxAttackMs`, `ClientDeEssRxReleaseMs`

## Consejos

- Mantenga Q en su valor predeterminado de 2.00 durante el barrido inicial. Un Q muy estrecho puede hacer que pase por alto el pico real sin activar la barra. Reduzca la banda con Q solo después de haber localizado el pico.
- Si la barra de reducción de ganancia nunca se mueve, Thresh está configurado demasiado alto. Bajélo hasta que la barra responda a los sonidos "S".
- La bola de frecuencia central en la curva de respuesta de sidechain se mueve a medida que gira Freq, proporcionando una referencia visual incluso antes de que haya audio presente.

## Solución de problemas

- **La barra de reducción de ganancia no se mueve durante el barrido** — Thresh está por encima del nivel de sus picos de sibilancia. Baje Thresh hasta que la barra comience a responder, luego vuelva a barrer.
- **La barra se mantiene cerca del máximo en un amplio rango de Freq** — Amount está configurado a un valor negativo muy grande y Thresh está muy bajo. Suba Thresh ligeramente para que la barra discrimine entre frecuencias en lugar de fijarse al máximo en todas partes.
- **El applet no es visible** — La etapa DESS no se ha habilitado en el widget CHAIN. Habilítela primero allí; el applet permanece oculto hasta que la etapa esté activa.
- **El mosaico del applet aparece atenuado** — La etapa DESS está actualmente en bypass. Haga un solo clic en la etapa DESS en el widget CHAIN para volver a habilitarla.
- **El editor en línea no aparece al hacer clic en un mando** — El modo de edición en línea del mando puede estar deshabilitado en su configuración. Verifique que la bandera `m_inlineEdit` esté habilitada (está habilitada de forma predeterminada).

## Relacionado

- [Descripción general de Aetherial De-Esser](overview.md)
- [Estrechar o ensanchar la banda de sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos "S" más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Ver GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
