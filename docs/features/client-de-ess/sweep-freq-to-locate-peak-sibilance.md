# Frecuencia de barrido para localizar el pico de sibilancia

Utilice el mando Freq para barrer el rango de sibilancia mientras transmite o monitorea el audio, observando la barra de reducción de ganancia para identificar la frecuencia que provoca la mayor reducción. Esto identifica el centro de la banda problemática de sibilancia antes de ajustar los valores de Q, Thresh y Amount.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN en el contenedor Aetherial Audio (TXDSP). La applet permanece oculta hasta que la etapa DESS está activa.
- Necesita una fuente de audio en vivo — ya sea transmitiendo o enrutando audio a través de la cadena TX DSP — para que la barra de reducción de ganancia responda en tiempo real.
- Abra la applet del de-esser. El bypass y la habilitación se controlan con un solo clic en la etapa DESS en el widget CHAIN. La edición se realiza a través del Aetherial Audio Channel Strip.

## Pasos

1. Ajuste Thresh a un valor justo por debajo de sus picos típicos de sibilancia — un punto de partida de -30.0 dB (el valor predeterminado) funciona para la mayoría de las voces.
2. Ajuste Amount a un valor claramente audible, como -12.0 dB o inferior, para que la reducción de ganancia sea fácil de ver en la barra.
3. Hable o reproduzca audio que contenga sonidos sostenidos de "S" y "T" de forma continua en el micrófono.
4. Gire lentamente el mando Freq desde su valor predeterminado de 6.0 kHz hacia arriba o hacia abajo, en el rango de 1000 a 12000 Hz.
5. Observe la barra de reducción de ganancia. La barra se llena más hacia la derecha — indicando la máxima atenuación — cuando Freq está centrado en la banda de sibilancia dominante.
6. Deténgase en el valor de Freq que produce la lectura más alta de reducción de ganancia. Ese valor es su frecuencia central de sibilancia.
7. Una vez completado el barrido, regrese Amount a su valor operativo deseado (valor predeterminado -6.0 dB).

## Función de cada control

| Control                  | Valor predeterminado | Rango válido        |
|--------------------------|----------------------|---------------------|
| Freq                     | 6000 Hz              | 1000 a 12000 Hz     |
| Q                        | 2.00                 | 0.5 a 5.0           |
| Thresh                   | -30.0 dB             | -60.0 a 0.0 dB      |
| Amount                   | -6.0 dB              | -24.0 a 0.0 dB      |
| Attack                   | 1.0 ms               | 0.1 a 30.0 ms       |
| Release                  | 100 ms               | 10.0 a 500.0 ms     |
| Curva de respuesta de sidechain | —               | —                   |
| Barra de reducción de ganancia | —               | 0 a 24 dB GR        |
| Slope                    | 24 dB/oct            | 12/24/36/48 dB/oct  |

**Nota:** Los mandos Attack y Release aparecen solo en el StripDeEssPanel del Channel Strip (tanto RX como TX). La applet ClientDeEssApplet acoplada omite estos controles.

## Ingreso directo de valores

Haga clic en la visualización del valor de cualquier mando para revelar un editor de texto en línea. Escriba un valor numérico (incluyendo unidades o texto final) y presione Enter o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido del mando. Para cancelar, presione Escape — el mando vuelve a su valor anterior.

- El editor admite el análisis sensible a la configuración regional, por lo que "12,5" funciona en configuraciones regionales que usan coma decimal.
- El texto final como "ms" o "dB" se elimina automáticamente.
- Mientras el editor está activo, los eventos de la rueda del ratón aún ajustan el mando con normalidad.

## Etiquetas de los ejes de la curva de respuesta de sidechain

El widget de la curva dibuja las etiquetas del eje de frecuencia usando QStaticText para mejorar el rendimiento del renderizado. Las etiquetas se muestran como "100", "500", "1k", "2k", etc. El texto de la etiqueta se almacena en caché después del primer pintado y se reutiliza en redibujados posteriores. Las etiquetas de los ejes están ocultas cuando el widget de la curva está en modo compacto.

## Atenuación en bypass

Cuando la etapa DESS está en bypass a través del widget CHAIN, todo el mosaico de la applet del de-esser se renderiza con opacidad reducida (aproximadamente el 55 % del brillo total). Esto coincide con el efecto de atenuación utilizado en la curva EQ y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve al brillo total tan pronto como la etapa se vuelve a habilitar.

## Instancias RX y TX

El Aetherial De-Esser tiene ajustes separados para las rutas TX y RX. El panel Applet Panel acoplado muestra la copia TX etiquetada como "Aetherial De-Esser". La copia RX, etiquetada como "Aetherial De-Esser — RX", es accesible a través del StripDeEssPanel del Aetherial Audio Channel Strip.

El StripDeEssPanel en el Channel Strip se puede abrir para TX o RX. Cuando se abre para TX, el título de la ventana muestra "Aetherial De-Esser — TX". Cuando se abre para RX, el título de la ventana muestra "Aetherial De-Esser — RX". Cada instancia guarda y restaura sus propios ajustes de mando de forma independiente usando claves de configuración separadas:
- TX: `ClientDeEssTxFrequencyHz`, `ClientDeEssTxQ`, `ClientDeEssTxThresholdDb`, `ClientDeEssTxAmountDb`, `ClientDeEssTxAttackMs`, `ClientDeEssTxReleaseMs`, `ClientDeEssTxSlopeStages`
- RX: `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, `ClientDeEssRxThresholdDb`, `ClientDeEssRxAmountDb`, `ClientDeEssRxAttackMs`, `ClientDeEssRxReleaseMs`, `ClientDeEssRxSlopeStages`

## Estilo del contenedor de la applet

El mosaico de la applet Aetherial De-Esser acoplada utiliza el espacio de nombres de contenedor `applet/deess` para la resolución de colores del tema. Los colores de los mandos — anillo de fondo, arco de primer plano, puntero, texto de etiqueta y texto de valor — se obtienen del espacio de nombres `color.knob.*` del tema:
- `color.knob.background` — fondo del anillo
- `color.knob.foreground` — arco del anillo
- `color.knob.handle` — puntero
- `color.text.secondary` — etiqueta del mando
- `color.text.primary` — valor del mando

El widget de la curva de respuesta de sidechain utiliza las siguientes claves de color del tema:
- `color.background.0` — fondo de la curva
- `color.background.1` — líneas de cuadrícula y líneas de cuadrícula principales
- `color.text.label` — etiquetas de los ejes
- `color.accent.danger` — curva de la banda de sibilancia (rojo suave)
- `color.accent.dim` — línea indicadora de umbral
- `color.accent.danger` combinado con `color.background.0` — brillo y núcleo del punto de frecuencia central

Esto permite anulaciones de color consistentes por applet sin modificar el código del widget.

## Consejos

- Mantenga Q en su valor predeterminado de 2.00 durante el barrido inicial. Un Q muy estrecho puede hacer que pase por alto el pico real sin activar la barra. Reduzca el ancho de banda con Q solo después de haber localizado el pico.
- Si la barra de reducción de ganancia nunca se mueve, Thresh está ajustado demasiado alto. Redúzcalo hasta que la barra responda a los sonidos "S".
- El punto de frecuencia central en la curva de respuesta de sidechain se mueve a medida que gira Freq, proporcionando una referencia visual incluso antes de que haya audio presente.
- Ajuste Slope después de encontrar la frecuencia central de sibilancia. Comience con 24 dB/oct (el valor predeterminado). Si el de-esser afecta el habla de banda media, pruebe con 36 o 48 dB/oct para una muesca más estrecha. Si las sibilancias siguen siendo ásperas, pruebe con 12 dB/oct para una muesca más ancha.

## Operación del botón Slope

En el StripDeEssPanel del Channel Strip, un botón pulsador Slope se encuentra en la parte inferior de la columna izquierda de mandos. Haga clic en él para recorrer los valores 12, 24, 36 y 48 dB/oct (de 1 a 4 etapas biquad de paso de banda en cascada). La etiqueta del botón se actualiza para mostrar el valor actual (por ejemplo, "24 dB/oct").

La configuración de Slope se conserva por ruta: `ClientDeEssTxSlopeStages` para TX y `ClientDeEssRxSlopeStages` para RX. Los cambios surten efecto de inmediato y la curva de respuesta de sidechain se redibuja para reflejar la nueva pendiente.

## Solución de problemas

- **La barra de reducción de ganancia no se mueve durante el barrido** — Thresh está por encima del nivel de sus picos de sibilancia. Reduzca Thresh hasta que la barra comience a responder, luego realice un nuevo barrido.
- **La barra permanece cerca del máximo en un rango amplio de Freq** — Amount está configurado en un valor negativo muy grande y Thresh está muy bajo. Suba Thresh ligeramente para que la barra discrimine entre frecuencias en lugar de saturarse al máximo en todas partes.
- **La applet no es visible** — La etapa DESS no se ha habilitado en el widget CHAIN. Habilítela allí primero; la applet permanece oculta hasta que la etapa esté activa.
- **El mosaico de la applet aparece atenuado** — La etapa DESS está actualmente en bypass. Haga un solo clic en la etapa DESS en el widget CHAIN para volver a habilitarla.
- **El editor en línea no aparece al hacer clic en un mando** — El modo de edición en línea del mando puede estar deshabilitado en su configuración. Verifique que el indicador `m_inlineEdit` esté habilitado (está activado de forma predeterminada).

## Relacionados

- [Aetherial De-Esser overview](overview.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
