# Descripción general del De-Esser

El De-Esser reduce la sibilancia áspera (sonidos "S" y "T") en el audio TX, atenuando una banda de frecuencia estrecha cada vez que su nivel supera un umbral definido. Úselo para suavizar el brillo de un micrófono agudo o de una sala con reflexiones pronunciadas en las frecuencias altas, sin alterar el resto de su voz.

## Antes de comenzar

- El De-Esser opera únicamente en la cadena de audio TX. No tiene efecto sobre el audio recibido.
- La etapa De-Ess debe estar habilitada en el widget CHAIN antes de que aparezca el applet. Consulte [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md) para saber cómo habilitarla y deshabilitarla.
- No se requiere conexión a la radio para ver o ajustar los controles del De-Esser.

## Cómo funciona

El De-Esser utiliza una arquitectura de cadena lateral (sidechain). Un filtro pasabanda aísla el rango de frecuencia que usted define con Freq y Q. Cuando el nivel en esa banda supera el nivel de Thresh, el De-Esser atenúa dicha banda hasta el valor máximo definido en Amount. El audio fuera de la banda de la cadena lateral no se ve afectado.

El applet se encuentra en el subcontenedor DESS, dentro del contenedor principal PooDoo Audio (TXDSP). Permanece oculto hasta que la etapa De-Ess se habilita mediante el widget CHAIN o el editor flotante. Para abrir el editor flotante, haga doble clic en la etapa DeEss del widget CHAIN. Para flotar, extraer o ocultar el applet acoplado, haga clic derecho en la barra de título del subcontenedor DESS.

El applet muestra dos indicadores visuales y cuatro perillas de ajuste:

- **Curva de respuesta de la cadena lateral** — dibuja la forma del filtro pasabanda. Una bola en tiempo real marca la frecuencia central actual en el pico de la curva.
- **Barra de reducción de ganancia** — una franja horizontal de color rojo suave que se rellena desde la derecha para mostrar la atenuación actual. La escala va de 0 a 24 dB; una marca indica el punto de −6 dB. La barra se actualiza aproximadamente 30 veces por segundo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistida | Descripción |
|---|---|---|---|---|
| Freq | 6000 Hz | 1000 – 12000 Hz | `ClientDeEssTxFrequencyHz` | Frecuencia central de la banda de sibilancia. Usa escala logarítmica. Se muestra como "X.X kHz" a partir de 1000 Hz. |
| Q | 2.00 | 0.5 – 5.0 | `ClientDeEssTxQ` | Ancho de banda de la banda de sibilancia. Valores más altos producen una banda más estrecha. |
| Thresh | −30.0 dB | −60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel a partir del cual comienza la atenuación. Ajústelo justo por debajo de los picos de sibilancia más intensos. |
| Amount | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada en el pico de sibilancia. Los valores son cero o negativos porque representan una reducción. |

El estado habilitado/deshabilitado de la etapa De-Ess se persiste como `ClientDeEssTxEnabled` y se controla desde el widget CHAIN, no desde el propio applet.

## Consejos

- Comience con Freq en el valor predeterminado de 6.0 kHz y desplácelo mientras pronuncia frases con sibilantes. Observe la barra de reducción de ganancia: la mayor actividad indica que ha encontrado la frecuencia central de la sibilancia.
- Un Q de 2.00 es un buen punto de partida. Estreche la banda (aumente Q hacia 5.0) si el de-esser afecta consonantes distintas a las sibilantes. Amplíela (reduzca Q hacia 0.5) si la sibilancia sigue escapando.
- Ajuste Thresh de modo que la barra de reducción de ganancia apenas se mueva con el habla normal y reaccione claramente ante sonidos "S" fuertes. Un umbral demasiado bajo provoca una reducción de ganancia constante que opaca la voz.
- Mantenga Amount en −6.0 dB o un valor menos profundo para obtener resultados transparentes. Valores más profundos pueden producir un efecto audible de "ceceo" si se aplican en exceso.

## Relacionados

- [Desplazar Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ampliar la banda de cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos de "S" más intensos](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la reducción de ganancia en tiempo real mientras se lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
