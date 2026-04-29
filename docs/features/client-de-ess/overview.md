# Descripción general del De-Esser Aetherial

El De-Esser Aetherial es un procesador de lado cliente exclusivo para TX que reduce la sibilancia excesiva (sonidos "S" y "T") en el audio transmitido. Funciona monitoreando una banda de frecuencia estrecha y atenuándola cuando el nivel de señal en esa banda supera un umbral definido.

## Antes de comenzar

- El De-Esser es una etapa exclusiva para TX. No tiene ningún efecto sobre el audio recibido.
- El applet permanece oculto hasta que se habilita la etapa De-Ess. Habilítela desde el widget CHAIN dentro del contenedor principal Aetherial Audio (TXDSP), o desde el editor flotante.
- No se requiere conexión a un radio para configurar el de-esser.

## Cómo funciona

El de-esser utiliza un diseño de cadena lateral (sidechain). Un filtro pasabanda aísla la banda de sibilancia definida por **Freq** y **Q**. Cuando el nivel en esa banda supera el valor de **Thresh**, el de-esser atenúa la banda hasta el valor de **Amount**. El resto del audio pasa sin verse afectado.

El applet muestra dos indicadores en tiempo real mientras transmite:

- **Curva de respuesta de la cadena lateral** — muestra la forma del filtro pasabanda con un marcador circular en la frecuencia central actual. Al ajustar **Freq** y **Q**, la curva y el marcador se actualizan de inmediato.
- **Barra de reducción de ganancia** — una franja horizontal de color rojo suave que se rellena desde la derecha para indicar la atenuación que se aplica en cada momento. La escala va de 0 a 24 dB; una marca señala el punto de −6 dB. El medidor se refresca aproximadamente 30 veces por segundo.

Para abrir el editor flotante completo, haga doble clic en la etapa DESS en el widget CHAIN. La ventana del editor se titula "Aetherial De-Esser — TX". Para omitir el de-esser sin modificar ningún ajuste, utilice el gesto de clic simple sobre la etapa DESS en el widget CHAIN.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente | Descripción |
|---|---|---|---|---|
| **Freq** | 6000 Hz | 1000 – 12000 Hz | `ClientDeEssTxFrequencyHz` | Frecuencia central de la banda de sibilancia. Usa escala logarítmica. Se muestra como "X.X kHz" a partir de 1000 Hz. |
| **Q** | 2.00 | 0.5 – 5.0 | `ClientDeEssTxQ` | Ancho de banda de la banda de sibilancia. Valores más altos producen una banda más estrecha. Usa escala lineal. |
| **Thresh** | −30.0 dB | −60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel a partir del cual el de-esser comienza a atenuar la banda. Ajústelo justo por debajo de los picos sibilantes más fuertes. |
| **Amount** | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada cuando la sibilancia alcanza su pico. Los valores negativos representan reducción; 0 dB significa sin atenuación. |
| **Curva de respuesta de la cadena lateral** | — | — | — | Visualización en tiempo real de la forma del filtro pasabanda. El marcador circular indica la frecuencia central actual. |
| **Barra de reducción de ganancia** | — | 0 – 24 dB GR | — | Medidor en tiempo real que muestra la atenuación actual. Relleno rojo suave; marca en −6 dB. |

El estado habilitado se almacena de forma persistente como `ClientDeEssTxEnabled`.

## Consejos

- Comience con **Freq** en el valor predeterminado de 6.0 kHz y desplácelo lentamente mientras pronuncia palabras con sibilantes. Observe la barra de reducción de ganancia — la deflexión máxima indica que ha encontrado la frecuencia de mayor sibilancia.
- Un **Q** de 2.00 es un punto de partida razonable. Auméntelo para aislar una banda problemática estrecha; redúzcalo si la sibilancia se distribuye en un rango más amplio.
- Ajuste **Thresh** de modo que la barra de reducción de ganancia solo se mueva ante sonidos genuinos de "S" y "T", y no ante vocales o consonantes normales.
- La marca de −6 dB en la barra de reducción de ganancia señala el valor predeterminado de **Amount**. Mantener la reducción cerca de esa marca suele producir resultados transparentes. Se dispone de valores mayores, pero pueden hacer que el efecto sea audible como bombeo (pumping) o ceceo.

## Temas relacionados

- [Desplazar Freq para localizar la sibilancia máxima](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ampliar la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos de "S" más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Calibrar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la reducción de ganancia en tiempo real mientras se lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Omitir el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
