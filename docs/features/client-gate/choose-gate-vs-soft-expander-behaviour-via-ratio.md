# Elegir comportamiento de gate o expansor suave mediante el ratio

El mando **Ratio** controla con qué agresividad el gate atenúa el audio por debajo del umbral. Un valor alto produce un corte brusco y casi total (comportamiento de gate clásico); un valor bajo produce una reducción más suave y gradual (expansor descendente suave). Elegir el valor adecuado evita conmutaciones abruptas de encendido/apagado sin dejar de eliminar el ruido de fondo.

## Antes de comenzar

- El gate debe estar habilitado en el lado que desea ajustar (TX o RX). Habilítelo mediante el widget CHAIN o haciendo doble clic en la etapa GATE del widget CHAIN para abrir el editor flotante.
- El subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" debe estar visible en el Applet Panel.

## Pasos

1. Localice el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-T** (lado RX) en el Applet Panel.
2. Busque el mando **Ratio** en la fila de cinco mandos situada en la parte inferior del applet. Su etiqueta muestra el formato `X.X:1`.
3. Gire **Ratio** hacia `1.0:1` para obtener un expansor descendente suave: el audio por debajo del umbral se atenúa de forma gradual en lugar de cortarse bruscamente.
4. Gire **Ratio** hacia `10.0:1` para obtener un corte más brusco, similar al de un gate: el audio por debajo del umbral se reduce de forma pronunciada, aproximándose al silencio en el valor de **Floor**.
5. Observe la barra de reducción de ganancia (la franja ámbar sobre la fila de mandos) mientras la entrada esté por debajo del umbral. Un relleno ámbar más profundo confirma que se está aplicando mayor atenuación.
6. Hable o reproduzca audio cruzando el umbral y observe la curva de transferencia. La bola de entrada en vivo se desplaza a lo largo de la curva; la pendiente de la curva por debajo del umbral se pronuncia a medida que aumenta el Ratio.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) | Comportamiento |
|---|---|---|---|---|
| **Ratio** | `2.0` | `1.0` a `10.0` | `ClientGateTxRatio` / `ClientGateRxRatio` | Pendiente de la curva de transferencia por debajo del umbral. `1.0:1` = sin atenuación (expansor desactivado). `10.0:1` = corte casi total. Mapeo de mando lineal. |
| **Thresh** | `-40.0 dB` | `-80.0` a `0.0 dB` | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` | Nivel por debajo del cual el gate comienza a atenuar. El Ratio solo tiene efecto por debajo de este punto. |
| **Floor** | `-15.0 dB` | `-80.0` a `0.0 dB` | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` | Atenuación máxima que el gate puede aplicar, independientemente del Ratio. Una marca en −15 dB en la barra de reducción de ganancia señala este valor predeterminado. |

## Consejos

- Un ratio de `2.0:1` (el valor predeterminado) funciona como expansor descendente suave: es un buen punto de partida para el gate de voz en TX cuando el silencio abrupto entre palabras suena antinatural.
- Aumentar el Ratio por encima de `5.0:1` se aproxima al comportamiento de gate real. Combine esto con un valor de **Floor** distinto de cero (por ejemplo, `-15.0 dB`) para evitar que el silencio total entre de forma brusca.
- Los cambios realizados en los mandos del applet y en el editor flotante (abierto haciendo doble clic en la etapa GATE del widget CHAIN) se mantienen sincronizados automáticamente.

## Solución de problemas

- **El Ratio está al máximo pero el ruido de fondo sigue siendo audible entre palabras** — El ajuste de **Floor** está limitando la atenuación antes de llegar al silencio. Baje **Floor** hacia `-80.0 dB`, o baje **Thresh** para que el gate se active al nivel de ruido real. Consulte [Establecer el umbral TX justo por encima del nivel de ruido de sala](set-tx-threshold-just-above-room-noise-floor.md) y [Ajustar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).
- **El audio se corta y reanuda de forma demasiado abrupta cuando el Ratio es alto** — Aumente **Release** para que el gate se cierre más lentamente, o baje **Ratio** hacia `2.0:1` para suavizar la transición. Consulte [Ajustar ataque/liberación para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md).

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Establecer el umbral TX justo por encima del nivel de ruido de sala](set-tx-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar el silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar ataque/liberación para una apertura/cierre natural](tune-attack-release-for-natural-open-close.md)
- [Ver la reducción de ganancia en vivo mientras no se transmite](watch-live-gr-while-not-speaking.md)
