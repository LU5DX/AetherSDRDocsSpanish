# Usar AGC-T en RX para suprimir el ruido de banda por debajo de un umbral elegido

El applet Aetherial AGC-T (RX) aplica un expansor descendente del lado del cliente al audio recibido. Úselo para reducir el ruido de banda persistente, QRM o silbidos entre señales, atenuando el audio que cae por debajo de un nivel que usted defina.

## Antes de comenzar

- El applet Aetherial AGC-T (RX) permanece oculto hasta que la etapa Gate esté habilitada en el lado RX. Habilítela primero mediante el widget CHAIN o el editor flotante Gate para el lado RX.
- El applet se encuentra dentro del contenedor padre Aetherial Audio (TXDSP) en el Panel de Applets. Abra el Panel de Applets si no está visible: `View > Applet Panel`.

## Pasos

1. En el Panel de Applets, localice el subcontenedor **Aetherial AGC-T** dentro del contenedor padre Aetherial Audio (TXDSP).
2. Habilite la etapa Gate para el lado RX usando el widget CHAIN (haga clic una vez en la etapa Gate) o haga doble clic en la etapa Gate del widget CHAIN para abrir el editor flotante **Aetherial Gate — RX**.
3. Observe la **curva de transferencia** (Transfer curve): la bola en movimiento indica el nivel de audio entrante en tiempo real. Note dónde se ubica la bola durante el ruido de banda y durante una señal.
4. Gire el control **Thresh** para establecer el nivel por debajo del cual la puerta comienza a atenuar. Ajústelo justo por encima del piso de ruido y por debajo de la señal más débil que desee escuchar. Valor predeterminado: -40.0 dB; rango: -80.0 a 0.0 dB. Este valor se guarda como `ClientGateRxThresholdDb`.
5. Gire el control **Ratio** para controlar con qué agresividad se corta el audio por debajo del umbral. En 2.0:1 (predeterminado), la puerta actúa como un expansor suave; en 10.0:1, el corte es muy pronunciado. Rango: 1.0 a 10.0. Se guarda como `ClientGateRxRatio`.
6. Gire el control **Floor** para establecer la atenuación máxima que puede aplicar la puerta. El valor predeterminado de -15.0 dB deja un ruido residual tenue en lugar de cortar hasta el silencio. Rango: -80.0 a 0.0 dB. Se guarda como `ClientGateRxFloorDb`.
7. Gire el control **Release** para controlar con qué rapidez se cierra la puerta después de que una señal cae por debajo del umbral. Valor predeterminado: 100 ms; rango: 5 a 2000 ms. Se guarda como `ClientGateRxReleaseMs`. Un Release más largo suena más natural; uno más corto cierra con mayor precisión entre señales.
8. Observe la **barra de reducción de ganancia** (Gain-reduction bar) mientras haya ruido de banda sin señal presente. La franja ámbar se llena desde la derecha cuando se aplica reducción de ganancia. La marca en -15 dB indica la posición predeterminada de Floor. Ajuste Thresh y Floor hasta que la barra permanezca llena durante el ruido y se vacíe con rapidez cuando aparezca una señal.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateRxThresholdDb` | Nivel por debajo del cual comienza la atenuación. Valores más bajos permiten que pase más señal antes de que actúe la puerta. |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateRxRatio` | Relación de expansión por debajo del umbral. Valores más altos producen un corte más pronunciado tipo puerta; valores más bajos generan una pendiente más suave. Se muestra como X.X:1. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateRxReleaseMs` | Velocidad con la que se cierra la puerta después de que la entrada cae por debajo del umbral. Usa mapeo exponencial. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateRxFloorDb` | Atenuación máxima que puede aplicar la puerta. Evita el silencio completo durante el ruido. |
| Transfer curve | — | — | — | Representa la curva estática del expansor. Una bola en tiempo real muestra el nivel de entrada actual en relación con el umbral. |
| Gain-reduction bar | — | 0 a 40 dB GR | — | La franja ámbar que se llena desde la derecha indica la profundidad de atenuación actual. La marca en -15 dB señala el Floor predeterminado. |

> **Nota:** La fuente confirma que el applet también cuenta con un control **Return** (predeterminado 2.0 dB, rango 0.0 a 20.0 dB) y un control **Release** en la interfaz construida. El catálogo incluye Attack (`ClientGateRxAttackMs`, predeterminado 0.5 ms, rango 0.1 a 100.0 ms) como un valor persistido independiente; es ajustable en el editor flotante **Aetherial Gate — RX** si no está presente en el mosaico del applet.

## Consejos

- Comience con Thresh en -40.0 dB y auméntelo lentamente hasta que la barra de reducción de ganancia se llene de forma sólida durante el ruido de banda, pero se abra con claridad cuando aparezca una señal.
- Ajuste Floor en -15.0 dB inicialmente. Redúzcalo (más negativo) solo si el ruido residual sigue siendo molesto. Evite valores de Floor muy bajos, ya que pueden hacer que el audio suene antinatural entre señales.
- Los cambios realizados en el editor flotante **Aetherial Gate — RX** y en el mosaico del applet permanecen sincronizados: el mosaico consulta el motor aproximadamente cada 33 ms y actualiza sus controles en consecuencia.
- El AGC-T opera completamente del lado del cliente y no requiere conexión con la radio para configurarse.

## Solución de problemas

- **El applet Aetherial AGC-T no es visible en el Panel de Applets** — La etapa Gate en el lado RX no ha sido habilitada. Habilítela mediante el widget CHAIN para el lado RX. El applet permanece oculto hasta que la etapa esté activa.
- **La barra de reducción de ganancia no muestra actividad incluso durante el ruido de banda** — Thresh está ajustado demasiado bajo. El piso de ruido no está alcanzando el umbral. Suba Thresh hacia 0 dB hasta que la barra muestre relleno ámbar durante el ruido.
- **Las señales están siendo cortadas junto con el ruido** — Thresh está ajustado demasiado alto. Baje Thresh para que solo el piso de ruido active la atenuación y las señales deseadas abran la puerta.
- **La puerta suena abrupta o entrecortada entre señales** — Aumente el valor de Release para permitir que la puerta se cierre de forma más gradual después de cada señal.

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Elegir comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar attack/release para apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Observar la reducción de ganancia en tiempo real sin transmitir](watch-live-gr-while-not-speaking.md)
