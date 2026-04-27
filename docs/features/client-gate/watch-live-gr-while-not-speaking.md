# Ver la reducción de ganancia en vivo sin hablar

El medidor de reducción de ganancia (GR) y la curva de transferencia se actualizan en tiempo real incluso cuando no está transmitiendo. Observarlos mientras el ambiente está en silencio le indica qué tan profundo está cortando el gate en cada momento, de modo que pueda evaluar si los ajustes de umbral y piso son apropiados antes de activar el transmisor.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el lado que desea observar. Consulte [Omitir el gate de la cadena](bypass-the-gate-from-the-chain.md) si el applet no es visible.
- El subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" debe estar abierto dentro del contenedor principal Aetherial Audio (TXDSP).

## Pasos

1. Abra el panel de applets si aún no está visible: `View > Applet Panel`.
2. Localice el subcontenedor "Aetherial TX Gate" (lado TX) o el subcontenedor "Aetherial AGC-T" (lado RX).
3. Permanezca en silencio — no hable ni active el radio.
4. Observe la barra de reducción de ganancia de color ámbar. Mientras la entrada permanezca por debajo del nivel Thresh, la barra se llena desde la derecha, mostrando la profundidad de atenuación que se está aplicando.
5. Observe la bola de entrada en la curva de transferencia. La bola se sitúa en la región inferior izquierda de la curva cuando el gate está cerrado (entrada por debajo del umbral) y se desplaza hacia arriba y a la derecha cuando el gate se abre.
6. Note hasta dónde se llena la barra. Si alcanza o supera la marca de -15 dB, el gate está aplicando al menos 15 dB de atenuación — el valor predeterminado de Floor.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|---|
| Transfer curve | Indicador | — | — | — |
| Input ball | Indicador | — | Por debajo / por encima del umbral | — |
| Gain-reduction bar | Medidor | — | 0 a 40 dB GR | — |
| Thresh | Mando | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |
| Ratio | Mando | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` |
| Attack | Mando | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` / `ClientGateRxAttackMs` |
| Release | Mando | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |
| Floor | Mando | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` |

**Gain-reduction bar:** Franja ámbar horizontal, rellena desde la derecha. La escala llega hasta 40 dB. Una marca en -15 dB señala el valor predeterminado de Floor. Vacía significa sin atenuación; relleno completo hacia la derecha significa que el gate está cortando a la profundidad máxima definida por Floor.

**Transfer curve / Input ball:** La curva estática muestra la relación entrada-salida del expansor. La bola en vivo rastrea el nivel de entrada actual, desplazándose por debajo o por encima del punto de quiebre del umbral en tiempo real.

## Consejos

- El medidor se actualiza aproximadamente cada 33 ms, por lo que la barra sigue la reducción de ganancia con suficiente detalle para detectar eventos de ruido breves.
- Los cambios realizados en los mandos del editor flotante de Gate se reflejan en el applet dentro del mismo ciclo de sondeo de 33 ms, de modo que puede dejar el applet visible como medidor en vivo mientras ajusta en el editor.
- Una barra que nunca se vacía por completo mientras está en silencio indica que el gate siempre está atenuando — la entrada nunca supera el nivel Thresh aunque deje de hablar. Este es el comportamiento normal y esperado de un noise gate en reposo.

## Relacionados

- [Ajustar el umbral TX justo por encima del piso de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar attack / release para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Omitir el gate de la cadena](bypass-the-gate-from-the-chain.md)
