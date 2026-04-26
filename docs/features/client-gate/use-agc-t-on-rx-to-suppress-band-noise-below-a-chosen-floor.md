# Usar AGC-T en RX para suprimir el ruido de banda por debajo de un umbral elegido

El applet Aetherial AGC-T aplica un expansor descendente del lado del cliente al audio recibido, atenuando las señales que caen por debajo de un umbral establecido. Úselo para reducir el ruido de banda persistente o el siseo que se encuentra por debajo del audio que desea escuchar.

## Antes de comenzar

- AetherSDR debe estar en ejecución. No se requiere una conexión de radio para configurar los controles, pero es necesario que haya audio fluyendo para ver cómo responden los medidores en tiempo real.
- El subcontenedor "Aetherial AGC-T" debe ser visible en el Panel de Applets. Permanece oculto hasta que la etapa Gate se habilita en el lado RX mediante el widget CHAIN o el editor flotante.

## Pasos

1. Habilite la etapa Gate en el lado RX: haga un solo clic en la etapa Gate del widget CHAIN en el lado RX, o abra el editor flotante titulado "Aetherial Gate — RX" haciendo doble clic en la etapa Gate del widget CHAIN.
2. Localice el subcontenedor "Aetherial AGC-T" dentro del contenedor principal Aetherial Audio (TXDSP) en el Panel de Applets.
3. Observe la curva de transferencia y el indicador de entrada (ball) mientras recibe. Cuando el indicador se encuentra por debajo del punto de inflexión (knee), la puerta está atenuando.
4. Gire el control Thresh para establecer el nivel por debajo del cual comienza la atenuación. Comience cerca del nivel de ruido de banda — un punto de partida típico es alrededor de −40.0 dB — y auméntelo hasta que el ruido de banda se reduzca pero las señales deseadas abran la puerta con limpieza.
5. Gire el control Ratio para controlar con qué agresividad se cortan las señales por debajo del umbral. Los valores más bajos (cercanos a 1.0) producen una expansión descendente suave; los valores más altos producen un corte más abrupto.
6. Gire el control Floor para establecer qué tan profunda puede llegar la atenuación. El valor predeterminado de −15.0 dB evita el silencio completo y al mismo tiempo reduce el ruido de manera útil.
7. Gire el control Attack para establecer con qué rapidez se abre la puerta cuando una señal supera el umbral. Los valores más rápidos permiten que los flancos de subida pasen con limpieza.
8. Gire el control Release para establecer con qué rapidez se cierra la puerta después de que una señal cae. Los valores más lentos evitan un corte brusco en las colas de la señal.
9. Observe la barra Gain-reduction. El relleno ámbar muestra la profundidad de atenuación actual. Procure que el relleno sea estable durante el ruido de banda y que descienda casi a vacío cuando llega una señal.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente |
|---|---|---|---|
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateRxThresholdDb` |
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateRxRatio` |
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateRxAttackMs` |
| Release | 100 ms | 5 a 2000 ms | `ClientGateRxReleaseMs` |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateRxFloorDb` |
| Curva de transferencia | — | — | — |
| Barra Gain-reduction | — | 0 a 40 dB GR | — |

**Curva de transferencia** — representa la relación estática entrada-salida del expansor. Un indicador de entrada en tiempo real se mueve a lo largo de la curva para mostrar si la puerta está actualmente abierta o cerrada.

**Barra Gain-reduction** — franja ámbar horizontal, rellena desde la derecha. La escala llega hasta 40 dB. Una marca en −15 dB indica la posición predeterminada de Floor.

## Consejos

- Los controles del mosaico del applet y el editor flotante "Aetherial Gate — RX" permanecen sincronizados. Los cambios realizados en cualquiera de las dos ubicaciones surten efecto de inmediato y se guardan automáticamente.
- Si las señales deseadas están siendo cortadas, disminuya Thresh o acorte Attack para que la puerta responda más rápidamente al audio ascendente.
- Si el ruido de banda se filtra entre señales, aumente Thresh o reduzca Floor para permitir una atenuación más profunda.
- La marca de −15 dB en la barra Gain-reduction es una referencia útil: si el relleno ámbar supera regularmente esa marca, el ruido de banda puede ser más fuerte de lo que el ajuste de Floor puede suprimir por completo.

## Solución de problemas

- **El subcontenedor "Aetherial AGC-T" no es visible** — la etapa Gate en el lado RX no ha sido habilitada. Habilítela mediante el widget CHAIN o el editor flotante "Aetherial Gate — RX".
- **La barra Gain-reduction no muestra movimiento durante el ruido de banda** — Thresh está ajustado por debajo del nivel de ruido. Aumente Thresh hasta que el relleno ámbar aparezca durante los períodos de solo ruido.
- **Las señales se cortan o se interrumpen prematuramente** — Attack es demasiado lento o Thresh es demasiado alto. Reduzca Thresh ligeramente, o disminuya Attack para abrir la puerta más rápido cuando llega una señal.
- **El audio suena entrecortado entre palabras** — Release es demasiado corto. Aumente Release para que la puerta se cierre de forma más gradual después de que una señal cae.

## Temas relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md)
- [Elegir el comportamiento de puerta vs. expansor suave mediante Ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar Attack y Release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Observar la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
