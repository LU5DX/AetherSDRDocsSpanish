# Usar Envelope para añadir drive dinámico en los transitorios

El control Envelope conecta un seguidor de envolvente al drive del tubo, de modo que la cantidad de saturación cambia en tiempo real con el nivel de la señal de entrada. Úselo en TX para añadir carácter armónico en los transitorios del micrófono, o en RX para que el audio recibido se sienta más presente en los picos.

## Antes de comenzar

- La etapa Tube debe estar habilitada para el lado que desea ajustar (TX o RX). Si el applet no es visible, habilite la etapa a través del widget CHAIN primero.
- Ajuste Drive a un nivel donde la curva de transferencia ya muestre cierta curvatura. Envelope modula ese drive; si Drive está en 0 dB, el efecto será sutil.
- Cuando una etapa Tube está en bypass, todo el mosaico del applet se atenúa a aproximadamente un 55 % de opacidad. Esta señal visual coincide con el efecto de atenuación utilizado en la curva EQ y confirma que la etapa DSP está inactiva.

## Pasos

1. Haga doble clic en la etapa TUBE en el widget CHAIN del lado TX o RX para abrir el editor flotante titulado "Aetherial Tube — TX" o "Aetherial Tube — RX".
2. Localice el control Envelope en la columna derecha del editor.
3. Gire Envelope en sentido horario (positivo) para aumentar el drive en los transitorios — el tubo se calienta más a medida que suben los niveles de entrada. Gírelo en sentido antihorario (negativo) para reducir el drive en los transitorios, comprimiendo los armónicos de forma dinámica. El valor predeterminado es 0 %.
4. Ajuste Attack para establecer la rapidez con que responde el seguidor de envolvente cuando los niveles suben. Los valores más bajos (hacia 0.1 ms) reaccionan más rápido; los valores más altos (hacia 30.0 ms) suavizan los picos cortos.
5. Ajuste Release para establecer la rapidez con que el seguidor se recupera después de que los niveles bajan. Los valores más bajos (hacia 10.0 ms) se recuperan más rápido; los valores más altos (hacia 500.0 ms) prolongan el efecto por más tiempo.
6. Observe la bola de entrada en vivo en la curva de transferencia — con Envelope activo, la bola se moverá más a lo largo de la curva en los picos que en los pasajes silenciosos, confirmando que el seguidor está funcionando.

## Qué hace cada control

| Control  | Predeterminado | Rango válido     |
|----------|----------------|------------------|
| Envelope | 0 %            | -1.0 a +1.0      |
| Attack   | 5.00 ms        | 0.1 a 30.0 ms    |
| Release  | 35.00 ms       | 10.0 a 500.0 ms  |
| RN2      | sin marcar     | —                |

## Atenuación por bypass

Cuando una etapa Tube está en bypass, AetherSDR aplica un `QGraphicsOpacityEffect` al mosaico del applet y lo renderiza al 55 % de opacidad. El mosaico vuelve a la opacidad completa tan pronto como se reactiva la etapa. Este comportamiento se aplica tanto a los mosaicos de TX como de RX y no requiere configuración.

## Edición de valor en línea

Cada control admite la introducción numérica directa para un ajuste preciso. Haga clic en el valor mostrado debajo de cualquier control para activar un campo de edición en línea. El campo aparece en un cuadro oscuro empotrado con un borde cian cuando está enfocado.

- Escriba un valor numérico y presione **Enter** para confirmar. El valor se ajusta al rango válido del control.
- Haga clic en cualquier otro lugar de la interfaz o presione **Tab** para confirmar el valor al perder el foco.
- Presione **Escape** para cancelar la edición y revertir al valor anterior.
- En configuraciones regionales que usan coma como separador decimal (p. ej., "12,5"), el editor acepta el formato de la configuración regional.
- El editor también acepta valores con texto de unidad al final (p. ej., "5.00 ms" o "−6 dB") eliminando los caracteres no numéricos antes del análisis.
- La entrada no válida revierte silenciosamente al último valor válido.

## Consejos

- Después de ajustar un valor positivo de Envelope, verifique el medidor OUT en el editor. Los picos pueden ser más fuertes de lo que produciría el ajuste estático de Drive por sí solo; use el control Output para compensar.
- Para un carácter de micrófono TX de sonido natural, comience con Envelope alrededor de +30 %, Attack en 5 ms y Release en 50–80 ms, luego ajuste al gusto.
- Los valores negativos de Envelope se comportan como un reductor de saturación dinámico — útil en RX para domar picos agresivos sin eliminar el carácter del tubo en pasajes más silenciosos.
- El control Dry/Wet mezcla la señal totalmente procesada (incluyendo la saturación modulada por envolvente) con la señal seca, por lo que puede usar valores altos de Envelope sin comprometerse totalmente con el efecto.
- Use la edición de valor en línea para establecer valores exactos de Attack, Release o Envelope en lugar de posiciones aproximadas de los controles.
- Si un mosaico aparece atenuado y los controles no responden, la etapa está en bypass. Vuelva a habilitarla a través del widget CHAIN; el mosaico volverá al brillo completo.
- El mosaico del applet ahora utiliza colores adaptables al tema a través del espacio de nombres `color.knob.*`. El fondo del control, el arco de primer plano, el mango, el texto de la etiqueta y el texto del valor respetan la configuración del tema actual en lugar de usar colores fijos.
- La curva de transferencia en el widget de curva también utiliza colores adaptables al tema: fondo (`color.background.0`), marco y cuadrícula (`color.background.1`), eje (`color.background.1`), curva (`color.accent.dim`), resplandor de la bola (`color.accent.warning`) y núcleo de la bola (`color.text.primary`).

## Solución de problemas

- **El control Envelope no tiene efecto audible** — Es probable que Drive esté en o cerca de 0 dB. Ajuste Drive a un valor donde la curva de transferencia se doble visiblemente, luego vuelva a probar Envelope.
- **El efecto suena errático o con bombeo** — Los valores de Attack o Release son demasiado cortos para el material de programa. Aumente Release hacia 100 ms o más; aumente Attack por encima de 10 ms para ignorar los transitorios cortos.
- **El nivel de salida aumenta en los transitorios** — Envelope positivo añade ganancia en los picos. Reduzca Output para compensar, o reduzca la profundidad de Envelope.
- **El mosaico del applet aparece atenuado** — La etapa Tube está en bypass. Habilite la etapa a través del widget CHAIN para restaurar la opacidad completa y el procesamiento DSP.
- **El editor en línea no acepta el valor escrito** — Asegúrese de que el valor esté dentro del rango válido del control. Los valores fuera del rango se ajustan silenciosamente. Verifique que está utilizando el separador decimal apropiado para su configuración regional.
- **Los colores del control se ven incorrectos** — Verifique que está utilizando un tema compatible. Los componentes del control ahora leen de `color.knob.background`, `color.knob.foreground`, `color.knob.handle`, `color.text.secondary` y `color.text.primary` en la definición del tema.

## Relacionados

- [Dial Drive until the curve starts to bend (TX warmth or RX tone shaping)](dial-drive-until-the-curve-starts-to-bend-tx-warmth-or-rx-tone-shaping.md)
- [Tune Attack and Release for natural-sounding envelope following](tune-attack-and-release-for-natural-sounding-envelope-following.md)
- [Compensate level changes with Output](compensate-level-changes-with-output.md)
- [Parallel-blend saturation with Dry/Wet](parallel-blend-saturation-with-dry-wet.md)
- [Monitor output clipping with the level meter in the editor](monitor-output-clipping-with-the-level-meter-in-the-editor.md)
