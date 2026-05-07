# Use Envelope para añadir énfasis dinámico en los transientes

El control Envelope conecta un seguidor de envolvente a la excitación del tubo, de modo que la cantidad de saturación cambia en tiempo real con el nivel de la señal de entrada. Úselo en TX para agregar textura armónica a los transientes del micrófono, o en RX para hacer que el audio recibido se sienta más presente en los picos.

## Antes de comenzar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Si el applet no está visible, habilite la etapa a través del widget CHAIN primero.
- Ajuste Drive a un nivel donde la curva de transferencia ya muestre cierta curvatura. Envelope modula esa excitación; si Drive está en 0 dB, el efecto será sutil.
- Cuando una etapa Tube está desviada (bypassed), todo el mosaico del applet se atenúa a aproximadamente un 55 % de opacidad. Esta señal visual coincide con el efecto de atenuación utilizado en la curva EQ y confirma que la etapa DSP está inactiva.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor flotante titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice el control Envelope en la columna derecha del editor.
3. Gire Envelope en sentido horario (positivo) para aumentar la excitación en los transientes: el tubo se calienta a medida que aumentan los niveles de entrada. Gírelo en sentido antihorario (negativo) para reducir la excitación en los transientes, comprimiendo los armónicos dinámicamente. El valor predeterminado es 0 %.
4. Ajuste Attack para definir la rapidez con la que responde el seguidor de envolvente cuando los niveles aumentan. Los valores más bajos (hacia 0.1 ms) reaccionan más rápido; los valores más altos (hacia 30.0 ms) suavizan los picos cortos.
5. Ajuste Release para definir la rapidez con la que el seguidor se recupera después de que los niveles disminuyen. Los valores más bajos (hacia 10.0 ms) se recuperan más rápido; los valores más altos (hacia 500.0 ms) prolongan la duración del efecto.
6. Observe la bola de entrada en vivo en la curva de transferencia: con Envelope activo, la bola se moverá más a lo largo de la curva en los picos que en los pasajes silenciosos, lo que confirma que el seguidor está funcionando.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistente (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Envelope | 0 % | −1.0 a +1.0 | `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope` | Positivo: aumenta la excitación en picos fuertes. Negativo: reduce la excitación en picos fuertes. Cero: sin modulación dinámica. |
| Attack | 5.00 ms | 0.1 a 30.0 ms | `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs` | Qué tan rápido responde el seguidor a niveles crecientes. Usa escala exponencial. No tiene efecto cuando Envelope es 0. |
| Release | 35.00 ms | 10.0 a 500.0 ms | `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs` | Qué tan rápido se recupera el seguidor después de que los niveles caen. Usa escala exponencial. No tiene efecto cuando Envelope es 0. |

## Atenuación al desviar (Bypass dimming)

Cuando una etapa Tube está desviada, AetherSDR aplica un `QGraphicsOpacityEffect` al mosaico del applet y lo renderiza con un 55 % de opacidad. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa. Este comportamiento se aplica tanto a los mosaicos TX como RX y no requiere configuración.

## Consejos

- Después de establecer un valor positivo de Envelope, verifique el medidor de salida (OUT) en el editor. Los picos pueden ser más fuertes de lo que el ajuste estático de Drive produciría por sí solo; use el control Output para compensar.
- Para una textura de micrófono TX de sonido natural, comience con Envelope alrededor de +30 %, Attack a 5 ms y Release a 50–80 ms, luego ajuste al gusto.
- Los valores negativos de Envelope se comportan como un reductor de saturación dinámico, útil en RX para domar picos agresivos sin eliminar el carácter del tubo de los pasajes más silenciosos.
- El control Dry/Wet mezcla la señal completamente procesada (incluyendo la saturación modulada por envolvente) con la señal seca, por lo que puede usar valores altos de Envelope sin comprometerse completamente con el efecto.
- Si un mosaico aparece atenuado y los controles no responden, la etapa está desviada. Vuelva a habilitarla a través del widget CHAIN; el mosaico volverá al brillo completo.

## Solución de problemas

- **El control Envelope no tiene efecto audible** — Es probable que Drive esté en o cerca de 0 dB. Ajuste Drive a un valor donde la curva de transferencia se doble visiblemente y luego vuelva a probar Envelope.
- **El efecto suena errático o con bombeo** — Los valores de Attack o Release son demasiado cortos para el material de programa. Aumente Release hacia 100 ms o más; aumente Attack por encima de 10 ms para ignorar transientes cortos.
- **El nivel de salida se dispara en los transientes** — Envelope positivo agrega ganancia en los picos. Reduzca Output para compensar, o reduzca la profundidad de Envelope.
- **El mosaico del applet aparece atenuado** — La etapa Tube está desviada. Habilite la etapa a través del widget CHAIN para restaurar la opacidad completa y el procesamiento DSP.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Tune Attack and Release for natural-sounding envelope following](tune-attack-and-release-for-natural-sounding-envelope-following.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-dry-wet.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
