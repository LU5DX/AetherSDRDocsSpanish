# Ver la reducción de ganancia (GR) en tiempo real sin hablar

Use esta página para leer el indicador de reducción de ganancia (GR) del ClientGateApplet mientras la puerta está inactiva, es decir, cuando ningún audio supera el umbral. Esto permite confirmar que la puerta se cierra correctamente y evaluar cuánta atenuación aplica entre palabras o durante el ruido de banda.

## Antes de comenzar

- La etapa Gate debe estar habilitada al menos en un lado (TX o RX). El applet permanece oculto hasta que la etapa Gate se habilite mediante el widget CHAIN o el editor flotante. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md) si el applet no es visible.
- AetherSDR debe estar conectado a audio (no se requiere conexión a una radio para que el indicador se anime, pero el audio debe estar fluyendo para que el medidor de GR muestre lecturas con sentido).

## Pasos

1. Localice el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-T** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el panel de applets.
2. Deje de hablar o espere un momento de silencio en la banda.
3. Observe la **barra de reducción de ganancia** — la franja horizontal de color ámbar en la parte superior del applet, justo debajo de la curva de transferencia. Cuando la puerta está cerrada, la franja se llena de derecha a izquierda en color ámbar.
4. Observe la **bola de entrada** en la curva de transferencia. Cuando la bola se encuentra por debajo del punto de umbral en la curva, la puerta está cerrada y el relleno ámbar en la **barra de reducción de ganancia** muestra la profundidad de atenuación que se está aplicando.
5. Observe la marca en la **barra de reducción de ganancia**. La marca en −15 dB señala el nivel de piso predeterminado del expansor suave. Si el relleno ámbar alcanza o supera esa marca, la puerta está atenuando en el valor de Floor predeterminado o más allá de él.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|---|
| Curva de transferencia | Indicador | — | — | — |
| Barra de reducción de ganancia | Medidor | — | 0 a 40 dB GR | — |
| Bola de entrada | Indicador | — | Por debajo / por encima del umbral | — |
| Thresh | Perilla | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |
| Ratio | Perilla | 2.0:1 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` |
| Attack | Perilla | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` / `ClientGateRxAttackMs` |
| Release | Perilla | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |
| Floor | Perilla | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` |

La escala de la **barra de reducción de ganancia** llega hasta 40 dB. La marca en −15 dB corresponde al valor predeterminado de Floor.

## Consejos

- El medidor se actualiza aproximadamente cada 33 ms. Es posible que los transitorios rápidos no sean completamente visibles, pero la atenuación en estado estable durante el silencio se lee con precisión.
- Si tiene el editor flotante abierto al mismo tiempo, los valores de las perillas en ambas vistas se sincronizan automáticamente. Puede ajustar Thresh o Floor en el editor y observar cómo responde la **barra de reducción de ganancia** en el applet sin cambiar de ventana.
- Para ver con qué profundidad corta la puerta, baje temporalmente Thresh muy por debajo de su nivel de ruido — el relleno ámbar debería acercarse a la escala completa. Restaure Thresh cuando termine.

## Solución de problemas

- **La barra de reducción de ganancia permanece vacía incluso cuando no se habla** — Es posible que la puerta no esté habilitada, o que la perilla Thresh esté configurada por debajo de su nivel de ruido, por lo que la puerta nunca se cierra. Suba Thresh hasta que quede justo por encima del nivel de ruido. Consulte [Ajustar el umbral de TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md).
- **El relleno ámbar alcanza la escala completa y el audio suena cortado** — La perilla Floor está configurada demasiado baja (valor negativo grande), aplicando más atenuación de la prevista. Suba Floor hacia −15.0 dB. Consulte [Ajustar Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).
- **El applet no es visible** — La etapa Gate no está habilitada. Habilítela mediante el widget CHAIN en el lado TX o RX correspondiente. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md).

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Ajustar el umbral de TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar silencios antinaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar attack / release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Elegir entre comportamiento de puerta o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
