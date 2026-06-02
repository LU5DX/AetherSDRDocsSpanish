# Descripción general del De-Esser Aetherial

El De-Esser Aetherial es un procesador del lado del cliente disponible tanto en instancias de TX como de RX. Reduce la sibilancia áspera (sonidos "S" y "T") monitorizando una banda de frecuencia estrecha y atenuándola cuando el nivel de señal en esa banda supera un umbral establecido.

## Antes de empezar

- El de-esser está disponible como un applet acoplado independiente (solo TX, etiquetado como "Aetherial De-Esser") y a través del Aetherial Audio Channel Strip (RX y TX).
- El applet acoplado está oculto hasta que se habilita la etapa De-Ess. Actívela a través del widget CHAIN dentro del contenedor principal Aetherial Audio (TXDSP).
- Para abrir la instancia de RX, use el icono de **Aetherial Audio Channel Strip** para el canal de recepción, luego haga clic en la etapa De-Ess. El panel se abre con el título "Aetherial De-Esser — RX".
- No se requiere conexión de radio para configurar el de-esser.

## Cómo funciona

El de-esser utiliza un diseño de cadena lateral (sidechain). Un filtro paso banda aísla la banda de sibilancia definida por **Freq** y **Q**. Cuando el nivel en esa banda supera el valor **Thresh**, el de-esser atenúa la banda hasta el valor **Amount**. El resto de su audio pasa sin verse afectado.

El panel muestra dos indicadores en vivo mientras el audio está activo:

- **Curva de respuesta de la cadena lateral** — muestra la forma del filtro paso banda con un marcador de bola en la frecuencia central actual. Al ajustar **Freq** y **Q**, la curva y la bola se actualizan inmediatamente. Las etiquetas del eje de frecuencia (100, 500, 1k, 2k, 4k, 8k, 12k) se renderizan usando texto en caché para rendimiento.
- **Barra de reducción de ganancia** — una barra horizontal de color rojo suave que se llena desde la derecha para mostrar cuánta atenuación se aplica en cada momento. La escala va de 0 a 24 dB; una marca indica el punto de −6 dB. El medidor se actualiza aproximadamente 30 veces por segundo.

Cuando la etapa del de-esser está en bypass, todo el panel se renderiza con opacidad reducida (aproximadamente 55%) para dar una indicación visual clara de que la etapa está inactiva. Para poner en bypass o reactivar el de-esser, use el gesto de un solo clic en la etapa DESS en el widget CHAIN.

## Instancias de TX y RX

El de-esser tiene instancias separadas para transmisión y recepción:

| Instancia | Cómo acceder | Etiqueta de la barra de título |
|---|---|---|
| TX (applet acoplado) | Haga clic en el icono De-Esser en el Applet Panel | "Aetherial De-Esser" |
| TX (channel strip) | Abra el channel strip de TX, haga clic en la etapa De-Ess | "Aetherial De-Esser — TX" |
| RX (channel strip) | Abra el channel strip de RX, haga clic en la etapa De-Ess | "Aetherial De-Esser — RX" |

Cada instancia mantiene ajustes independientes para Freq, Q, Thresh, Amount, Attack, Release y Slope. El applet acoplado omite los controles de Attack y Release.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---|---|---|---|
| **Freq** | 6000 Hz | 1000 – 12000 Hz | Mapeo logarítmico. Establece la frecuencia central de la banda de sibilancia. La etiqueta muestra '6.0 kHz' por encima de 1 kHz, 'N Hz' por debajo. |
| **Q** | 2.00 | 0.5 – 5.0 | Mapeo lineal. Establece el ancho de banda de la sibilancia — Q más alta = más estrecha. La etiqueta muestra 'X.XX'. |
| **Thresh** | −30.0 dB | −60.0 a 0.0 dB | Mapeo lineal. Nivel por encima del cual el de-esser comienza a atenuar la banda. |
| **Amount** | −6.0 dB | −24.0 a 0.0 dB | Mapeo lineal. Atenuación máxima aplicada en el pico de sibilancia. Los valores son negativos (o cero) porque representan reducción. |
| **Attack** | 1.0 ms | 0.1 a 30.0 ms | Mapeo exponencial. Establece la rapidez con que el de-esser responde una vez que la sibilancia cruza el umbral. Presente en el StripDeEssPanel del Channel Strip. El ClientDeEssApplet acoplado omite este control. |
| **Release** | 100 ms | 10.0 a 500.0 ms | Mapeo exponencial. Establece la rapidez con que la ganancia regresa después de que la sibilancia cae por debajo del umbral. Presente en el StripDeEssPanel del Channel Strip. El ClientDeEssApplet acoplado omite este control. |
| **Slope** | 24 dB/oct (2 etapas) | 12 / 24 / 36 / 48 dB/oct (1 a 4 etapas) | Cicla el recuento de cascadas del paso banda de la cadena lateral. Cada etapa añade 12 dB/oct de atenuación fuera de la banda sibilante. Presente en el StripDeEssPanel flotante. La etiqueta muestra 'N dB/oct'. Presente tanto para rutas TX como RX. |

### Edición de valor en línea

Cada control admite edición de valor en línea. Haga clic en el texto del valor mostrado para abrir un pequeño campo de entrada de texto. Escriba un nuevo valor y presione **Enter** o haga clic fuera del campo para confirmar. El valor se limita automáticamente al rango válido del control. Presione **Escape** para cancelar la edición y volver al valor anterior. Esta función funciona de la misma manera en el applet acoplado y en los paneles del channel strip.

## Botón Slope

El botón **Slope** en el panel del Channel Strip le permite ajustar la pendiente del filtro de la cadena lateral:

- Haga clic en el botón para ciclar a través de 12 → 24 → 36 → 48 dB/oct (1 a 4 biquads paso banda en cascada).
- Cada clic aumenta la atenuación en 12 dB/oct fuera de la banda sibilante.
- Los valores de pendiente más altos crean una muesca más estrecha alrededor de la frecuencia central, reduciendo la atenuación colateral del habla en el rango medio.
- La etiqueta del botón se actualiza para mostrar el ajuste actual (por ejemplo, "24 dB/oct").
- La curva de respuesta de la cadena lateral se actualiza para reflejar la nueva pendiente.
- La configuración de pendiente persiste de forma independiente para las rutas TX y RX.

## Persistencia de la configuración

Cada instancia guarda y restaura sus valores de control desde la base de datos de configuración:

| Clave de configuración | Propósito |
|---|---|
| `ClientDeEssTxFrequencyHz` | Frecuencia central de TX |
| `ClientDeEssTxQ` | Factor de ancho de banda de TX |
| `ClientDeEssTxThresholdDb` | Umbral de la cadena lateral de TX |
| `ClientDeEssTxAmountDb` | Atenuación máxima de TX |
| `ClientDeEssTxAttackMs` | Tiempo de ataque de TX |
| `ClientDeEssTxReleaseMs` | Tiempo de liberación de TX |
| `ClientDeEssTxSlopeStages` | Número de etapas de pendiente de TX |
| `ClientDeEssTxEnabled` | Estado habilitado de TX |

Los ajustes de RX utilizan un conjunto de claves paralelo (`ClientDeEssRx*`). La configuración se guarda cuando ajusta cualquier control o cierra el panel.

## Temas

El panel del de-esser y sus controles utilizan el sistema de temas de la aplicación. Los colores de los controles (anillo de fondo, arco de primer plano, manejador del puntero, texto de etiqueta, texto de valor) se obtienen de las claves de color del tema:

- `color.knob.background` — anillo de fondo del control
- `color.knob.foreground` — arco de valor del control
- `color.knob.handle` — línea del puntero del control
- `color.text.secondary` — texto de la etiqueta del control
- `color.text.primary` — texto del valor del control

La curva de respuesta de la cadena lateral también utiliza colores del tema:

- `color.background.0` — fondo del widget de la curva
- `color.background.1` — líneas de cuadrícula y líneas de cuadrícula principales
- `color.text.label` — etiquetas de los ejes
- `color.accent.danger` — curva de la banda sibilante (rojo suave)
- `color.accent.dim` — líneas de umbral/marcador
- `color.accent.warning` — resplandor de la bola de frecuencia central
- `color.text.primary` — núcleo de la bola de frecuencia central

El contenedor del applet acoplado está registrado con el tema como `applet/deess`, lo que permite anulaciones de color por applet cuando el tema activo las define.

## Consejos

- Comience con **Freq** en el valor predeterminado de 6.0 kHz y varíelo lentamente mientras pronuncia palabras sibilantes. Observe la barra de reducción de ganancia — la desviación máxima indica que ha encontrado la frecuencia de sibilancia máxima.
- Un **Q** de 2.00 es un punto de partida razonable. Auméntelo para aislar una banda problemática estrecha; redúzcalo si la sibilancia se extiende en un rango más amplio.
- Ajuste **Thresh** para que la barra de reducción de ganancia solo se mueva con sonidos "S" y "T" genuinos, no con vocales o consonantes normales.
- La marca de −6 dB en la barra de reducción de ganancia marca el valor predeterminado de **Amount**. Mantener la reducción cerca de esa marca generalmente produce resultados transparentes. Hay cantidades mayores disponibles, pero pueden hacer que el efecto se vuelva audible como bombeo o ceceo.
- Use el botón **Slope** para ajustar la pendiente del filtro con precisión. Comience con 24 dB/oct y auméntelo si escucha demasiada atenuación de rango medio en frases con mucha sibilancia.
- Use configuraciones diferentes para TX y RX — puede necesitar un de-essing más agresivo en recepción que en transmisión, o viceversa.
- Cuando la etapa está en bypass, el panel se atenúa notablemente. Si el panel parece atenuado y no escucha el de-essing, verifique que la etapa DESS no esté en bypass en el widget CHAIN.

## Relacionados

- [Sweep Freq to locate peak sibilance](sweep-freq-to-locate-peak-sibilance.md)
- [Narrow or widen the sidechain band with Q](narrow-or-widen-the-sidechain-band-with-q.md)
- [Set threshold just below the loudest 'S' peaks](set-threshold-just-below-the-loudest-s-peaks.md)
- [Dial Amount for the most transparent de-essing](dial-amount-for-the-most-transparent-de-essing.md)
- [Watch live GR while reading a sibilant phrase](watch-live-gr-while-reading-a-sibilant-phrase.md)
- [Bypass the de-esser from the chain](bypass-the-de-esser-from-the-chain.md)
