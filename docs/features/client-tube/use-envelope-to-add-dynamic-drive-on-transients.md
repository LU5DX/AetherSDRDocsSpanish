# Use Envelope para añadir drive dinámico en transitorios

El control Envelope conecta un seguidor de envolvente al drive del tubo, de modo que la cantidad de saturación cambia en tiempo real según el nivel de la señal de entrada. Úselo en TX para añadir distorsión armónica en los transitorios del micrófono, o en RX para que el audio recibido se sienta más presente en los picos.

## Antes de comenzar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Si el applet no es visible, habilite la etapa primero desde el widget CHAIN.
- Ajuste Drive a un nivel donde la curva de transferencia ya muestre algo de curvatura. Envelope modula ese drive; si Drive está en 0 dB, el efecto será sutil.

## Pasos

1. Haga doble clic en la etapa TUBE del widget CHAIN en el lado TX o RX para abrir el editor flotante titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice el control Envelope en la columna derecha del editor.
3. Gire Envelope hacia la derecha (positivo) para aumentar el drive en los transitorios — el tubo se calienta más a medida que suben los niveles de entrada. Gírelo hacia la izquierda (negativo) para reducir el drive en los transitorios, comprimiendo los armónicos de forma dinámica. El valor predeterminado es 0 %.
4. Ajuste Attack para definir con qué rapidez responde el seguidor de envolvente cuando los niveles suben. Valores más bajos (hacia 0.1 ms) reaccionan más rápido; valores más altos (hacia 30.0 ms) suavizan los picos cortos.
5. Ajuste Release para definir con qué rapidez se recupera el seguidor después de que los niveles bajen. Valores más bajos (hacia 10.0 ms) se recuperan más rápido; valores más altos (hacia 500.0 ms) dejan que el efecto se prolongue.
6. Observe la bola de entrada en vivo sobre la curva de transferencia — con Envelope activo, la bola se desplazará más a lo largo de la curva en los picos que en los pasajes silenciosos, lo que confirma que el seguidor está funcionando.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Ajuste persistido (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Envelope | 0 % | −1.0 a +1.0 | `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope` | Positivo: aumenta el drive en picos altos. Negativo: reduce el drive en picos altos. Cero: sin modulación dinámica. |
| Attack | 5.00 ms | 0.1 a 30.0 ms | `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs` | Rapidez con la que el seguidor responde a niveles en ascenso. Usa escala exponencial. No tiene efecto cuando Envelope es 0. |
| Release | 35.00 ms | 10.0 a 500.0 ms | `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs` | Rapidez con la que el seguidor se recupera tras la caída de niveles. Usa escala exponencial. No tiene efecto cuando Envelope es 0. |

## Consejos

- Después de establecer un valor positivo de Envelope, verifique el medidor OUT en el editor. Los picos pueden ser más altos de lo que produciría el ajuste estático de Drive por sí solo; use el control Output para compensarlo.
- Para lograr un grit de micrófono TX de sonido natural, comience con Envelope alrededor de +30 %, Attack en 5 ms y Release entre 50 y 80 ms; luego ajuste a gusto.
- Los valores negativos de Envelope actúan como un reductor dinámico de saturación — útil en RX para controlar picos duros sin eliminar el carácter del tubo en los pasajes más silenciosos.
- El control Dry/Wet mezcla la señal totalmente procesada (incluida la saturación modulada por envolvente) con la señal seca, por lo que puede usar valores altos de Envelope sin comprometerse completamente con el efecto.

## Solución de problemas

- **El control Envelope no produce efecto audible** — Es probable que Drive esté en 0 dB o cerca de ese valor. Ajuste Drive a un valor donde la curva de transferencia se curve visiblemente y vuelva a probar Envelope.
- **El efecto suena errático o con bombeo** — Los valores de Attack o Release son demasiado cortos para el material de programa. Aumente Release hacia 100 ms o más; aumente Attack por encima de 10 ms para ignorar transitorios cortos.
- **El nivel de salida presenta picos en los transitorios** — Un Envelope positivo añade ganancia en los picos. Reduzca Output para compensarlo, o disminuya la profundidad de Envelope.

## Relacionados

- [Ajuste Drive hasta que la curva comience a curvarse (calidez en TX o modelado de tono en RX)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Ajuste Attack y Release para un seguimiento de envolvente de sonido natural](tune-attack-and-release-for-natural-sounding-envelope-following.md)
- [Compense los cambios de nivel con Output](compensate-level-changes-with-output.md)
- [Mezcle saturación en paralelo con Dry/Wet](parallel-blend-saturation-with-dry-wet.md)
- [Monitoree el recorte de salida con el medidor de nivel en el editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
