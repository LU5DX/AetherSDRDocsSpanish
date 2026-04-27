# Elegir el comportamiento de puerta o expansor suave mediante el ratio

El control **Ratio** determina con qué agresividad la puerta atenúa el audio por debajo del umbral. Un valor de ratio bajo produce un expansor descendente suave que reduce gradualmente el audio de bajo nivel; un valor alto produce una puerta dura que lo corta bruscamente. Elegir el ratio adecuado permite adaptar el carácter de la puerta a su situación de ruido y estilo de operación.

## Antes de comenzar

- La etapa de puerta debe estar habilitada en el lado que desea ajustar (TX o RX). Si el applet no es visible, habilite la puerta mediante el widget CHAIN o haga doble clic en la etapa GATE para abrir el editor flotante.
- Abra el subcontenedor **Aetherial TX Gate** (TX) o el subcontenedor **Aetherial AGC-T** (RX) dentro del contenedor padre Aetherial Audio (TXDSP) en el panel de applets.

## Pasos

1. Localice el control **Ratio** en la fila de cinco controles en la parte inferior del applet.
2. Para establecer el comportamiento de expansor suave, gire **Ratio** hacia un valor bajo (por ejemplo, 2.0:1). El audio por debajo del umbral se reduce gradualmente.
3. Para establecer el comportamiento de puerta dura, gire **Ratio** hacia un valor alto (por ejemplo, 8.0:1 o superior). El audio por debajo del umbral se corta bruscamente.
4. Observe la barra de reducción de ganancia mientras el audio pasa. Un ajuste de expansor suave produce un relleno ámbar más somero y gradual; un ajuste de puerta dura produce un relleno profundo y abrupto cuando la puerta se cierra.
5. Si el corte de la puerta dura es demasiado severo entre palabras, ajuste **Floor** para limitar la atenuación máxima. Consulte [Establecer Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) | Comportamiento |
|---|---|---|---|---|
| **Ratio** | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` | Se muestra como X.X:1. Valores bajos expanden suavemente; valores altos aplican puerta dura. |
| **Thresh** | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` | Nivel por debajo del cual comienza la atenuación. |
| **Floor** | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` | Atenuación máxima que la puerta puede aplicar, independientemente del ratio. |
| **Barra de reducción de ganancia** | — | 0 a 40 dB GR | — | Franja ámbar, rellena desde la derecha. La marca en -15 dB indica el valor predeterminado de Floor. |
| Curva de transferencia | — | — | — | Muestra la curva de transferencia estática con una bola en vivo en el nivel de entrada actual. |

## Consejos

- Un ratio de 2.0:1 (el predeterminado) es un punto de partida conservador adecuado para la mayoría de los usos en TX. Auméntelo solo si el ruido de bajo nivel sigue siendo audible cuando no está hablando.
- Con valores de ratio superiores a aproximadamente 8.0:1, la puerta se comporta casi como un interruptor de encendido/apagado. Combínelo con un **Thresh** cuidadosamente ajustado para evitar recortar el flanco inicial de las palabras.
- La curva de transferencia se actualiza en tiempo real al mover **Ratio**. Use la bola de entrada en vivo para confirmar que la forma de la curva coincide con su intención antes de transmitir.
- Los cambios en **Ratio** surten efecto de inmediato y se guardan automáticamente. No se requiere ningún botón Apply ni Save.

## Solución de problemas

- **El control Ratio no tiene efecto en el sonido** — Confirme que la etapa de puerta está habilitada. Una puerta en bypass pasa el audio sin modificaciones, independientemente de los ajustes de los controles. Consulte [Poner la puerta en bypass desde la cadena](bypass-the-gate-from-the-chain.md).
- **El ratio de puerta dura corta demasiado y genera silencios artificiales** — Reduzca **Floor** hacia 0 dB para disminuir la atenuación máxima, o reduzca **Ratio** hacia el rango de expansor suave.
- **El ratio de expansor suave no suprime suficientemente el ruido** — Aumente **Ratio** o reduzca **Thresh** para que la atenuación comience con un nivel de entrada más alto.

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Establecer el umbral TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Establecer Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar ataque y caída para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Observar la reducción de ganancia en vivo mientras no se transmite](watch-live-gr-while-not-speaking.md)
