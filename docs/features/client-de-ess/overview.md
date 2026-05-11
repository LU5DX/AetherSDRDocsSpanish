# Descripción general del De-Esser Aetherial

El De-Esser Aetherial es un procesador del lado del cliente disponible en instancias de TX y RX. Reduce la sibilancia excesiva (sonidos "S" y "T") monitorizando una banda de frecuencia estrecha y atenuándola cuando el nivel de señal en esa banda supera un umbral establecido.

## Antes de comenzar

- El de-esser está disponible como un applet acoplado independiente (solo TX, etiquetado "Aetherial De-Esser") y a través de la Aetherial Audio Channel Strip (RX y TX).
- El applet acoplado permanece oculto hasta que se habilita la etapa De-Ess. Actívela mediante el widget CHAIN dentro del contenedor principal Aetherial Audio (TXDSP).
- Para abrir la instancia de RX, use el icono de la **Aetherial Audio Channel Strip** para el canal de recepción y luego haga clic en la etapa De-Ess. El panel se abre con el título "Aetherial De-Esser — RX".
- No se requiere conexión de radio para configurar el de-esser.

## Cómo funciona

El de-esser utiliza un diseño de cadena lateral. Un filtro pasabanda aísla la banda de sibilancia definida por **Freq** y **Q**. Cuando el nivel en esa banda supera el valor de **Thresh**, el de-esser atenúa la banda hasta el valor de **Amount**. El resto de su audio pasa sin verse afectado.

El panel muestra dos indicadores en vivo mientras el audio está activo:

- **Curva de respuesta de la cadena lateral** — muestra la forma del filtro pasabanda con un marcador esférico en la frecuencia central actual. Al ajustar **Freq** y **Q**, la curva y la esfera se actualizan inmediatamente. Las etiquetas del eje de frecuencia (100, 500, 1k, 2k, 4k, 8k, 12k) se representan utilizando texto en caché para optimizar el rendimiento.
- **Barra de reducción de ganancia** — una barra horizontal de color rojo suave que se llena desde la derecha para mostrar cuánta atenuación se está aplicando en cada momento. La escala va de 0 a 24 dB; una marca indica el punto de −6 dB. El medidor se actualiza aproximadamente 30 veces por segundo.

Cuando la etapa del de-esser está en bypass, todo el panel se renderiza con opacidad reducida (aproximadamente 55 %) para indicar visualmente que la etapa está inactiva. Para poner en bypass o reactivar el de-esser, use un solo clic en la etapa DESS del widget CHAIN.

## Instancias de TX y RX

El de-esser tiene instancias separadas para transmisión y recepción:

| Instancia | Cómo acceder | Etiqueta de la barra de título |
|---|---|---|
| TX (applet acoplado) | Haga clic en el icono De-Esser en el Applet Panel | "Aetherial De-Esser" |
| TX (channel strip) | Abra la channel strip de TX, haga clic en la etapa De-Ess | "Aetherial De-Esser — TX" |
| RX (channel strip) | Abra la channel strip de RX, haga clic en la etapa De-Ess | "Aetherial De-Esser — RX" |

Cada instancia mantiene ajustes independientes para Freq, Q, Thresh, Amount, Attack y Release. El applet acoplado omite los controles Attack y Release.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **Freq** | 6000 Hz | 1000 – 12000 Hz | Mapeo logarítmico. Establece la frecuencia central de la banda de sibilancia. La etiqueta muestra "6.0 kHz" por encima de 1 kHz, "N Hz" por debajo. |
| **Q** | 2.00 | 0.5 – 5.0 | Mapeo lineal. Establece el ancho de banda: Q más alto = banda más estrecha. La etiqueta muestra "X.XX". |
| **Thresh** | −30.0 dB | −60.0 a 0.0 dB | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar. |
| **Amount** | −6.0 dB | −24.0 a 0.0 dB | Mapeo lineal. Atenuación máxima en el pico de sibilancia. Los valores negativos representan reducción. |
| **Attack** | 1.0 ms | 0.1 a 30.0 ms | Mapeo exponencial. Rapidez con la que el de-esser responde una vez que la sibilancia supera el umbral. Solo en el panel de la Channel Strip (RX y TX). |
| **Release** | 100 ms | 10.0 a 500.0 ms | Mapeo exponencial. Rapidez con la que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Solo en el panel de la Channel Strip (RX y TX). |

## Persistencia de ajustes

Cada instancia guarda y restaura sus valores de control desde la base de datos de configuración:

| Clave de ajuste | Propósito |
|---|---|
| `ClientDeEssTxFrequencyHz` | Frecuencia central de TX |
| `ClientDeEssTxQ` | Factor de ancho de banda de TX |
| `ClientDeEssTxThresholdDb` | Umbral de cadena lateral de TX |
| `ClientDeEssTxAmountDb` | Atenuación máxima de TX |
| `ClientDeEssTxAttackMs` | Tiempo de ataque de TX |
| `ClientDeEssTxReleaseMs` | Tiempo de liberación de TX |
| `ClientDeEssTxEnabled` | Estado habilitado de TX |

Los ajustes de RX utilizan un conjunto de claves paralelo (`ClientDeEssRx*`). Los ajustes se guardan al ajustar cualquier control o al cerrar el panel.

## Consejos

- Comience con **Freq** en el valor predeterminado de 6.0 kHz y barra lentamente mientras dice palabras con sibilancia. Observe la barra de reducción de ganancia: la desviación máxima indica que ha encontrado la frecuencia de sibilancia pico.
- Un **Q** de 2.00 es un punto de partida razonable. Auméntelo para aislar una banda problemática estrecha; redúzcalo si la sibilancia se extiende en un rango más amplio.
- Ajuste **Thresh** para que la barra de reducción de ganancia se mueva solo con sonidos "S" y "T" genuinos, no con vocales o consonantes normales.
- La marca de −6 dB en la barra de reducción de ganancia señala el valor predeterminado de **Amount**. Mantener la reducción cerca de esa marca generalmente produce resultados transparentes. Hay cantidades mayores disponibles, pero pueden hacer que el efecto sea audible como bombeo o ceceo.
- Use ajustes diferentes para TX y RX: es posible que necesite un de-essing más agresivo en recepción que en transmisión, o viceversa.
- Cuando la etapa está en bypass, el panel se oscurece notablemente. Si el panel aparece oscuro y no escucha el de-essing, verifique que la etapa DESS no esté en bypass en el widget CHAIN.

## Relacionado

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
