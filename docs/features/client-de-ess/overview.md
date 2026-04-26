# Descripción general del De-Esser Aetherial

El De-Esser Aetherial es un procesador del lado del cliente exclusivo para TX que reduce la sibilancia áspera (sonidos "S" y "T") en el audio transmitido. Funciona monitoreando una banda de frecuencia estrecha y atenuándola cuando el nivel de señal en esa banda supera un umbral establecido.

## Antes de comenzar

- El De-Esser es una etapa exclusiva para TX. No tiene efecto sobre el audio recibido.
- El applet permanece oculto hasta que se habilite la etapa De-Ess. Habilítela desde el widget CHAIN dentro del contenedor padre Aetherial Audio (TXDSP), o desde el editor flotante.
- No se requiere conexión con la radio para configurar el de-esser.

## Cómo funciona

El de-esser utiliza un diseño de cadena lateral (sidechain). Un filtro pasabanda aísla la banda de sibilancia definida por **Freq** y **Q**. Cuando el nivel en esa banda supera el valor de **Thresh**, el de-esser atenúa la banda hasta el valor de **Amount**. El resto del audio pasa sin modificaciones.

El applet muestra dos indicadores en tiempo real mientras transmite:

- **Curva de respuesta de la cadena lateral** — muestra la forma del filtro pasabanda con un marcador de bola en la frecuencia central actual. Al ajustar **Freq** y **Q**, la curva y la bola se actualizan de inmediato.
- **Barra de reducción de ganancia** — una franja roja suave horizontal que se llena desde la derecha para mostrar cuánta atenuación se está aplicando en cada momento. La escala va de 0 a 24 dB; una marca indica el punto −6 dB. El medidor se actualiza aproximadamente 30 veces por segundo.

Para abrir el editor flotante completo, haga doble clic en la etapa DESS en el widget CHAIN. La ventana del editor se titula "Aetherial De-Esser — TX". Para poner en bypass el de-esser sin cambiar ninguna configuración, utilice el gesto de un solo clic sobre la etapa DESS en el widget CHAIN.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistida | Descripción |
|---|---|---|---|---|
| **Freq** | 6000 Hz | 1000 – 12000 Hz | `ClientDeEssTxFrequencyHz` | Frecuencia central de la banda de sibilancia. Usa escala logarítmica. Se muestra como "X.X kHz" a partir de 1000 Hz. |
| **Q** | 2.00 | 0.5 – 5.0 | `ClientDeEssTxQ` | Ancho de banda de la banda de sibilancia. Valores más altos producen una banda más estrecha. Usa escala lineal. |
| **Thresh** | −30.0 dB | −60.0 a 0.0 dB | `ClientDeEssTxThresholdDb` | Nivel a partir del cual el de-esser comienza a atenuar la banda. Ajústelo justo por debajo de sus picos sibilantes más fuertes. |
| **Amount** | −6.0 dB | −24.0 a 0.0 dB | `ClientDeEssTxAmountDb` | Atenuación máxima aplicada cuando la sibilancia está en su pico. Los valores negativos representan reducción; 0 dB significa sin atenuación. |
| **Curva de respuesta de la cadena lateral** | — | — | — | Visualización en tiempo real de la forma del filtro pasabanda. La bola marca la frecuencia central actual. |
| **Barra de reducción de ganancia** | — | 0 – 24 dB GR | — | Medidor en tiempo real que muestra la atenuación actual. Relleno rojo suave; marca en −6 dB. |

El estado habilitado se persiste como `ClientDeEssTxEnabled`.

## Consejos

- Comience con **Freq** en el valor predeterminado de 6.0 kHz y desplácelo lentamente mientras pronuncia palabras con sibilantes. Observe la barra de reducción de ganancia: la máxima deflexión indica que ha encontrado la frecuencia de sibilancia pico.
- Un **Q** de 2.00 es un buen punto de partida. Auméntelo para aislar una banda problemática estrecha; disminúyalo si la sibilancia se extiende en un rango más amplio.
- Ajuste **Thresh** de modo que la barra de reducción de ganancia solo se mueva ante sonidos genuinos de "S" y "T", no ante vocales o consonantes normales.
- La marca de −6 dB en la barra de reducción de ganancia indica el valor predeterminado de **Amount**. Mantener la reducción cerca de esa marca generalmente produce resultados transparentes. Se dispone de valores mayores, pero pueden hacer audible el efecto como bombeo o ceceo.

## Relacionados

- [Desplace Freq para localizar la sibilancia pico](sweep-freq-to-locate-peak-sibilance.md)
- [Estreche o amplíe la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajuste el umbral justo por debajo de los picos de "S" más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajuste Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observe la reducción de ganancia en tiempo real mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Ponga en bypass el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
