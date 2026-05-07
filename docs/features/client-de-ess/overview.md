# Descripción general del Aetherial De-Esser

El Aetherial De-Esser es un procesador del lado del cliente disponible en instancias tanto de TX como de RX. Reduce la sibilancia aguda (sonidos "S" y "T") monitorizando una banda estrecha de frecuencia y atenuándola cuando el nivel de señal en esa banda supera un umbral establecido.

## Antes de empezar

- El de-esser está disponible como un applet acoplado independiente (solo TX, etiquetado como "Aetherial De-Esser") y a través del Aetherial Audio Channel Strip (RX y TX).
- El applet acoplado permanece oculto hasta que la etapa De-Ess esté habilitada. Actívela mediante el widget CHAIN dentro del contenedor principal Aetherial Audio (TXDSP).
- Para abrir la instancia de RX, use el icono de **Aetherial Audio Channel Strip** para el canal de recepción, luego haga clic en la etapa De-Ess. El panel se abre con el título "Aetherial De-Esser — RX".
- No se requiere conexión de radio para configurar el de-esser.

## Cómo funciona

El de-esser utiliza un diseño de cadena lateral. Un filtro paso banda aísla la banda de sibilancia definida por **Freq** y **Q**. Cuando el nivel en esa banda supera el valor **Thresh**, el de-esser atenúa la banda hasta el valor **Amount**. El resto de su audio pasa sin verse afectado.

El panel muestra dos indicadores en vivo mientras el audio está activo:

- **Curva de respuesta de la cadena lateral** — muestra la forma del filtro paso banda con un marcador esférico en la frecuencia central actual. Al ajustar **Freq** y **Q**, la curva y el marcador se actualizan de inmediato.
- **Barra de reducción de ganancia** — una franja horizontal de color rojo suave que se llena desde la derecha para mostrar cuánta atenuación se está aplicando en cada momento. La escala va de 0 a 24 dB; una marca indica el punto de −6 dB. El medidor se actualiza aproximadamente 30 veces por segundo.

Cuando la etapa del de-esser está en bypass, todo el panel se renderiza con opacidad reducida (aproximadamente 55%) para dar una clara indicación visual de que la etapa está inactiva. Para poner en bypass o reactivar el de-esser, use el gesto de un solo clic en la etapa DESS del widget CHAIN.

## Instancias TX y RX

El de-esser tiene instancias separadas para transmisión y recepción:

| Instancia | Cómo acceder | Etiqueta de la barra de título |
|---|---|---|
| TX (applet acoplado) | Haga clic en el icono De-Esser en el Applet Panel | "Aetherial De-Esser" |
| TX (channel strip) | Abra el channel strip de TX, haga clic en la etapa De-Ess | "Aetherial De-Esser — TX" |
| RX (channel strip) | Abra el channel strip de RX, haga clic en la etapa De-Ess | "Aetherial De-Esser — RX" |

Cada instancia mantiene ajustes independientes para Freq, Q, Thresh, Amount, Attack y Release. El applet acoplado omite los mandos de Attack y Release.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **Freq** | 6000 Hz | 1000 – 12000 Hz | Mapeo logarítmico. Establece la frecuencia central de la banda de sibilancia. La etiqueta muestra "6.0 kHz" por encima de 1 kHz, "N Hz" por debajo. |
| **Q** | 2.00 | 0.5 – 5.0 | Mapeo lineal. Establece el ancho de banda — Q más alto = más estrecho. La etiqueta muestra "X.XX". |
| **Thresh** | −30.0 dB | −60.0 a 0.0 dB | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar. |
| **Amount** | −6.0 dB | −24.0 a 0.0 dB | Mapeo lineal. Atenuación máxima en el pico de sibilancia. Los valores negativos representan reducción. |
| **Attack** | 1.0 ms | 0.1 a 30.0 ms | Mapeo exponencial. Qué tan rápido responde el de-esser una vez que la sibilancia cruza el umbral. Solo en el panel del Channel Strip (RX y TX). |
| **Release** | 100 ms | 10.0 a 500.0 ms | Mapeo exponencial. Qué tan rápido regresa la ganancia después de que la sibilancia cae por debajo del umbral. Solo en el panel del Channel Strip (RX y TX). |

## Persistencia de los ajustes

Cada instancia guarda y restaura los valores de sus controles desde la base de datos de ajustes:

| Clave de ajuste | Propósito |
|---|---|
| `ClientDeEssTxFrequencyHz` | Frecuencia central de TX |
| `ClientDeEssTxQ` | Factor de ancho de banda de TX |
| `ClientDeEssTxThresholdDb` | Umbral de cadena lateral de TX |
| `ClientDeEssTxAmountDb` | Atenuación máxima de TX |
| `ClientDeEssTxAttackMs` | Tiempo de ataque de TX |
| `ClientDeEssTxReleaseMs` | Tiempo de liberación de TX |
| `ClientDeEssTxEnabled` | Estado habilitado de TX |

Los ajustes de RX utilizan un conjunto de claves paralelo (`ClientDeEssRx*`). Los ajustes se guardan cuando ajusta cualquier mando o cierra el panel.

## Consejos

- Comience con **Freq** en el valor predeterminado de 6.0 kHz y bárrala lentamente mientras pronuncia palabras sibilantes. Observe la barra de reducción de ganancia — la desviación máxima indica que ha encontrado la frecuencia de sibilancia pico.
- Un **Q** de 2.00 es un punto de partida razonable. Auméntelo para aislar una banda problemática estrecha; redúzcalo si la sibilancia está distribuida en un rango más amplio.
- Ajuste **Thresh** para que la barra de reducción de ganancia solo se mueva en sonidos genuinos de "S" y "T", no en vocales o consonantes normales.
- La marca de −6 dB en la barra de reducción de ganancia señala el valor predeterminado de **Amount**. Mantener la reducción cerca de esa marca suele producir resultados transparentes. Hay cantidades mayores disponibles, pero pueden hacer que el efecto sea audible como bombeo o ceceo.
- Use ajustes diferentes para TX y RX — puede necesitar un de-essing más agresivo en recepción que en transmisión, o viceversa.
- Cuando la etapa está en bypass, el panel se atenúa notablemente. Si el panel parece atenuado y no nota de-essing, verifique que la etapa DESS no esté en bypass en el widget CHAIN.

## Relacionado

- [Barrer Freq para localizar el pico de sibilancia](sweep-freq-to-locate-peak-sibilance.md)
- [Estrechar o ensanchar la banda de la cadena lateral con Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Ajustar el umbral justo por debajo de los picos de 'S' más fuertes](set-threshold-just-below-the-loudest-s-peaks.md)
- [Ajustar Amount para el de-essing más transparente](dial-amount-for-the-most-transparent-de-essing.md)
- [Observar la GR en vivo mientras lee una frase sibilante](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Poner en bypass el de-esser desde la cadena](bypass-the-de-esser-from-the-chain.md)
