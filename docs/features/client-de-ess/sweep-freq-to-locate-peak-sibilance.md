# Barrer Frec para localizar el pico de sibilancia

Use el mando Freq para barrer el rango de sibilancia mientras transmite o monitoriza audio, observando la barra de reducción de ganancia para detectar la frecuencia que provoca la mayor reducción. Esto identifica el centro de la banda de sibilancia problemática antes de ajustar definitivamente sus valores de Q, Thresh y Amount.

## Antes de comenzar

- El Aetherial De-Esser debe estar habilitado mediante el widget CHAIN en el contenedor Aetherial Audio (TXDSP). El applet permanece oculto hasta que la etapa DESS esté activa.
- Necesita una fuente de audio en vivo — ya sea transmitiendo o enrutando audio a través de la cadena TX DSP — para que la barra de reducción de ganancia responda en tiempo real.
- Abra el applet del de-esser. El bypass y la habilitación se controlan con un solo clic en la etapa DESS del widget CHAIN. La edición se realiza a través del Aetherial Audio Channel Strip.

## Pasos

1. Ajuste Thresh a un valor justo por debajo de sus picos típicos de sibilancia — un punto de partida de -30.0 dB (el valor predeterminado) funciona para la mayoría de las voces.
2. Ajuste Amount a un valor claramente audible, como -12.0 dB o inferior, para que la reducción de ganancia sea fácil de ver en la barra.
3. Hable o reproduzca audio que contenga sonidos sostenidos de "S" y "T" de forma continua en el micrófono.
4. Gire lentamente el mando Freq desde su valor predeterminado de 6.0 kHz hacia arriba o hacia abajo dentro del rango de 1000 a 12000 Hz.
5. Observe la barra de reducción de ganancia. La barra se llena más hacia la derecha — indicando la máxima atenuación — cuando Freq está centrada en la banda de sibilancia dominante.
6. Deténgase en el valor de Freq que produzca la lectura de reducción de ganancia más alta. Ese valor es su frecuencia central de sibilancia.
7. Una vez completado el barrido, regrese Amount a su valor operativo previsto (por defecto -6.0 dB).

## Función de cada control

| Control                  | Valor predeterminado | Rango válido        |
|--------------------------|----------------------|---------------------|
| Freq                     | 6000 Hz              | 1000 a 12000 Hz     |
| Q                        | 2.00                 | 0.5 a 5.0           |
| Thresh                   | -30.0 dB             | -60.0 a 0.0 dB      |
| Amount                   | -6.0 dB              | -24.0 a 0.0 dB      |
| Attack                   | 1.0 ms               | 0.1 a 30.0 ms       |
| Release                  | 100 ms               | 10.0 a 500.0 ms     |
| Curva de respuesta del sidechain | —               | —                    |
| Barra de reducción de ganancia  | —               | 0 a 24 dB GR        |
| Slope                    | 24 dB/oct            | 12/24/36/48 dB/oct  |

**Nota:** Los mandos Attack y Release aparecen solo en el StripDeEssPanel del Channel Strip (tanto RX como TX). El ClientDeEssApplet acoplado omite estos controles.

## Introducción directa de valores

Haga clic en la visualización del valor de cualquier mando para revelar un editor de texto en línea. Escriba un valor numérico (incluyendo unidades o texto al final) y presione Enter o haga clic en otro lugar para confirmar. El valor se ajusta al rango válido del mando. Para cancelar, presione Escape — el mando vuelve a su valor anterior.

- El editor admite el análisis según la configuración regional, por lo que "12,5" funciona en zonas con separador decimal de coma.
- El texto final como "ms" o "dB" se elimina automáticamente.
- Mientras el editor está activo, los eventos de la rueda del ratón siguen ajustando el mando con normalidad.

## Etiquetas de los ejes de la curva de respuesta del sidechain

El widget de la curva dibuja las etiquetas del eje de frecuencia usando QStaticText para mejorar el rendimiento de renderizado. Las etiquetas se muestran como "100", "500", "1k", "2k", etc. El texto de la etiqueta se almacena en caché después del primer pintado y se reutiliza en posteriores redibujados. Las etiquetas de los ejes se ocultan cuando el widget de la curva está en modo compacto.

## Atenuación por bypass

Cuando la etapa DESS está en bypass a través del widget CHAIN, todo el mosaico del applet de-esser se renderiza con opacidad reducida (aproximadamente el 55% del brillo completo). Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona una indicación clara de un vistazo de que la etapa está inactiva. El mosaico vuelve al brillo completo tan pronto como se vuelve a habilitar la etapa.

## Suavizado de la animación del medidor

La barra de reducción de ganancia utiliza un temporizador de animación suavizado que se actualiza a aproximadamente 30 Hz. La animación aplica una facilitación cúbica a la visualización de la reducción de ganancia para una respuesta visual natural y sin vibraciones. El temporizador se detiene cuando el valor de reducción de ganancia se ha estabilizado para evitar repintados innecesarios. La animación activa un repintado en cada tic del temporizador para garantizar transiciones visuales suaves incluso cuando el valor de reducción de ganancia está cerca de un umbral donde el temporizador se detendría prematuramente.

## Instancias RX y TX

El Aetherial De-Esser tiene ajustes separados para las rutas TX y RX. El Applet Panel acoplado muestra la copia TX etiquetada como "Aetherial De-Esser". La copia RX, etiquetada como "Aetherial De-Esser — RX", es accesible a través del StripDeEssPanel del Aetherial Audio Channel Strip.

El StripDeEssPanel en el Channel Strip se puede abrir tanto para TX como para RX. Cuando se abre para TX, el título de la ventana muestra "Aetherial De-Esser — TX". Cuando se abre para RX, el título de la ventana muestra "Aetherial De-Esser — RX". Cada instancia guarda y restaura independientemente sus propios ajustes de los mandos utilizando claves de ajuste separadas:
- TX: `ClientDeEssTxFrequencyHz`, `ClientDeEssTxQ`, `ClientDeEssTxThresholdDb`, `ClientDeEssTxAmountDb`, `ClientDeEssTxAttackMs`, `ClientDeEssTxReleaseMs`, `ClientDeEssTxSlopeStages`
- RX: `ClientDeEssRxFrequencyHz`, `ClientDeEssRxQ`, `ClientDeEssRxThresholdDb`, `ClientDeEssRxAmountDb`, `ClientDeEssRxAttackMs`, `ClientDeEssRxReleaseMs`, `ClientDeEssRxSlopeStages`

## Estilo del contenedor del applet

El mosaico del applet Aetherial De-Esser acoplado utiliza el espacio de nombres de contenedor `applet/deess` para la resolución de colores del tema. Los colores de los mandos — anillo de fondo, arco de primer plano, puntero, texto de etiqueta y texto de valor — se toman del espacio de nombres `color.knob.*` del tema:
- `color.knob.background` — fondo del anillo
- `color.knob.foreground` — arco del anillo
- `color.knob.handle` — puntero
- `color.text.secondary` — etiqueta del mando
- `color.text.primary` — valor del mando

El widget de la curva de respuesta del sidechain utiliza las siguientes claves de color del tema:
- `color.background.0` — fondo de la curva
- `color.background.1` — líneas de cuadrícula y líneas de cuadrícula principales
- `color.text.label` — etiquetas de los ejes
- `color.accent.danger` — curva de la banda de sibilancia (rojo suave)
- `color.accent.dim` — línea indicadora de umbral
- `color.accent.danger` combinado con `color.background.0` — brillo y centro de la bola de frecuencia central

Esto permite anulaciones de color consistentes por applet sin modificar el código del widget.

## Consejos

- Mantenga Q en su valor predeterminado de 2.00 durante el barrido inicial. Un Q muy estrecho puede hacer que pase por alto el pico real sin activar la barra. Reduzca el ancho de banda con Q solo después de haber localizado el pico.
- Si la barra de reducción de ganancia nunca se mueve, Thresh está configurado demasiado alto. Redúzcalo hasta que la barra responda a los sonidos de "S".
- La bola de frecuencia central en la curva de respuesta del sidechain se mueve a medida que gira Freq, proporcionando una referencia visual incluso antes de que haya audio presente.
- Ajuste Slope después de encontrar la frecuencia central de sibilancia. Comience con 24 dB/oct (el valor predeterminado). Si el de-esser afecta el habla de banda media, pruebe con 36 o 48 dB/oct para una muesca más estrecha. Si las sibilancias siguen siendo ásperas, pruebe con 12 dB/oct para una muesca más ancha.

## Funcionamiento del botón Slope

En el StripDeEssPanel del Channel Strip, un botón pulsador Slope se encuentra en la parte inferior de la columna izquierda de mandos. Haga clic en él para recorrer las opciones 12, 24, 36 y 48 dB/oct (de 1 a 4 etapas biquad de paso de banda en cascada). La etiqueta del botón se actualiza para mostrar el valor actual (por ejemplo, "24 dB/oct").

El ajuste Slope se conserva por ruta: `ClientDeEssTxSlopeStages` para TX y `ClientDeEssRxSlopeStages` para RX. Los cambios surten efecto inmediatamente y la curva de respuesta del sidechain se redibuja para reflejar la nueva pendiente.

## Solución de problemas

- **La barra de reducción de ganancia no se mueve durante el barrido** — Thresh está por encima del nivel de sus picos de sibilancia. Reduzca Thresh hasta que la barra comience a responder, luego repita el barrido.
- **La barra permanece cerca del máximo en un rango amplio de Freq** — Amount está configurado con un valor negativo muy grande y Thresh está muy bajo. Eleve Thresh ligeramente para que la barra discrimine entre frecuencias en lugar de saturarse al máximo en todas partes.
- **El applet no es visible** — La etapa DESS no se ha habilitado en el widget CHAIN. Habilítela allí primero; el applet permanece oculto hasta que la etapa esté activa.
- **El mosaico del applet aparece atenuado** — La etapa DESS está actualmente en bypass. Haga un solo clic en la etapa DESS del widget CHAIN para volver a habilitarla.
- **El editor en línea no aparece al hacer clic en un mando** — El modo de edición en línea del mando puede estar deshabilitado en su configuración. Verifique que el indicador `m_inlineEdit` esté habilitado (está activado por defecto).

## Relacionados

- [Descripción general del Aetherial De-Esser](overview.md)
- [Estrechar o ensanchar la banda del sidechain con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
