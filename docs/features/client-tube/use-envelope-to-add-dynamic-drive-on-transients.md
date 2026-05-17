# Usar Envelope para agregar drive dinámico en los transitorios

El control Envelope conecta un seguidor de envolvente al drive del tubo, por lo que la cantidad de saturación cambia en tiempo real con el nivel de la señal de entrada. Úselo en TX para agregar armónicos dinámicos a los transitorios del micrófono, o en RX para que el audio recibido se sienta más presente en los picos.

## Antes de comenzar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Si el applet no es visible, primero habilite la etapa a través del widget CHAIN.
- Ajuste Drive a un nivel donde la curva de transferencia ya muestre cierta curvatura. Envelope modula ese drive; si Drive está en 0 dB, el efecto será sutil.
- Cuando una etapa Tube está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esta señal visual coincide con el efecto de atenuación utilizado en la curva de EQ y confirma que la etapa DSP está inactiva.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor flotante titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice el control Envelope en la columna derecha del editor.
3. Gire Envelope en el sentido de las agujas del reloj (positivo) para aumentar el drive en los transitorios: el tubo se calienta a medida que los niveles de entrada aumentan. Gírelo en sentido contrario (negativo) para reducir el drive en los transitorios, comprimiendo los armónicos dinámicamente. El valor predeterminado es 0 %.
4. Ajuste Attack para definir qué tan rápido responde el seguidor de envolvente cuando los niveles aumentan. Los valores más bajos (hacia 0.1 ms) reaccionan más rápido; los valores más altos (hacia 30.0 ms) suavizan los picos cortos.
5. Ajuste Release para definir qué tan rápido se recupera el seguidor después de que los niveles bajan. Los valores más bajos (hacia 10.0 ms) se recuperan más rápido; los valores más altos (hacia 500.0 ms) permiten que el efecto se mantenga por más tiempo.
6. Observe la bola de entrada en vivo en la curva de transferencia: con Envelope activo, la bola se moverá más a lo largo de la curva en los picos que en los pasajes silenciosos, lo que confirma que el seguidor está funcionando.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Configuración persistente (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Envelope | 0 % | −1.0 a +1.0 | `ClientTubeTxEnvelope` / `ClientTubeRxEnvelope` | Positivo: aumenta el drive en picos fuertes. Negativo: reduce el drive en picos fuertes. Cero: sin modulación dinámica. |
| Attack | 5.00 ms | 0.1 a 30.0 ms | `ClientTubeTxAttackMs` / `ClientTubeRxAttackMs` | Qué tan rápido responde el seguidor a niveles crecientes. Usa escala exponencial. No tiene efecto cuando Envelope es 0. |
| Release | 35.00 ms | 10.0 a 500.0 ms | `ClientTubeTxReleaseMs` / `ClientTubeRxReleaseMs` | Qué tan rápido se recupera el seguidor después de que los niveles bajan. Usa escala exponencial. No tiene efecto cuando Envelope es 0. |

## Atenuación por bypass

Cuando una etapa Tube está en bypass, AetherSDR aplica un `QGraphicsOpacityEffect` al mosaico del applet y lo renderiza al 55 % de opacidad. El mosaico vuelve a la opacidad completa tan pronto como se vuelve a habilitar la etapa. Este comportamiento se aplica tanto a los mosaicos TX como RX y no requiere configuración.

## Edición inline de valores

Cada control admite entrada numérica directa para un ajuste preciso. Haga clic en el valor mostrado debajo de cualquier control para activar un campo de edición inline. El campo aparece en un recuadro oscuro con borde cian cuando está enfocado.

- Escriba un valor numérico y presione **Enter** para confirmar. El valor se limita al rango válido del control.
- Haga clic en otra parte de la interfaz o presione **Tab** para confirmar el valor al perder el foco.
- Presione **Escape** para cancelar la edición y volver al valor anterior.
- En configuraciones regionales que usan coma como separador decimal (ej., "12,5"), el editor acepta el formato local.
- El editor también acepta valores con texto de unidad al final (ej., "5.00 ms" o "−6 dB") eliminando los caracteres no numéricos antes de analizar.
- La entrada no válida se revierte silenciosamente al último valor válido.

## Consejos

- Después de establecer un valor positivo de Envelope, verifique el medidor OUT en el editor. Los picos pueden ser más fuertes de lo que el ajuste estático de Drive produciría por sí solo; use el control Output para compensar.
- Para obtener un sonido natural de armónicos dinámicos en TX, comience con Envelope alrededor de +30 %, Attack en 5 ms y Release entre 50 y 80 ms, luego ajuste según su gusto.
- Los valores negativos de Envelope se comportan como un reductor de saturación dinámica, útil en RX para domar picos agresivos sin eliminar el carácter del tubo en pasajes más silenciosos.
- El control Dry/Wet mezcla la señal completamente procesada (incluyendo la saturación modulada por envolvente) con la señal seca, por lo que puede usar valores altos de Envelope sin comprometerse completamente con el efecto.
- Use la edición inline de valores para establecer valores exactos de Attack, Release o Envelope en lugar de posiciones aproximadas de los controles.
- Si un mosaico aparece atenuado y los controles no responden, la etapa está en bypass. Vuelva a habilitarla a través del widget CHAIN; el mosaico volverá al brillo completo.

## Solución de problemas

- **El control Envelope no tiene efecto audible**: es probable que Drive esté en o cerca de 0 dB. Ajuste Drive a un valor donde la curva de transferencia se doble visiblemente, luego pruebe Envelope nuevamente.
- **El efecto suena errático o con bombeo**: los valores de Attack o Release son demasiado cortos para el material de programa. Aumente Release hacia 100 ms o más; aumente Attack por encima de 10 ms para ignorar transitorios cortos.
- **El nivel de salida tiene picos en los transitorios**: Envelope positivo agrega ganancia en los picos. Reduzca Output para compensar, o reduzca la profundidad de Envelope.
- **El mosaico del applet aparece atenuado**: la etapa Tube está en bypass. Habilite la etapa a través del widget CHAIN para restaurar la opacidad completa y el procesamiento DSP.
- **El editor inline no acepta el valor escrito**: asegúrese de que el valor esté dentro del rango válido del control. Los valores fuera del rango se limitan silenciosamente. Verifique que esté utilizando el separador decimal apropiado para su configuración regional.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Tune Attack and Release for natural-sounding envelope following](tune-attack-and-release-for-natural-sounding-envelope-following.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-dry-wet.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
