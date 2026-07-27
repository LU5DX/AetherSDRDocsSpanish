# Elegir comportamiento de compuerta o expansor suave mediante la relación

El mando de **Ratio** controla la agresividad con la que la compuerta atenúa el audio por debajo del umbral. Un valor bajo produce un expansor descendente suave que reduce el audio silencioso gradualmente; un valor alto produce una compuerta fuerte que lo corta drásticamente. Elegir la relación adecuada permite adaptar el carácter de la compuerta a su situación de ruido y estilo de operación.

## Antes de comenzar

- La etapa de compuerta debe estar habilitada en el lado que desea ajustar (TX o RX). Si el applet no está visible, habilite la compuerta mediante el widget CHAIN o haga doble clic en la etapa GATE para abrir el editor flotante.
- Abra el subcontenedor **Aetherial TX Gate** (TX) o el subcontenedor **Aetherial AGC-G** (RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el Panel de Applets.
- Cuando una etapa de compuerta está en bypass, todo el mosaico del applet se atenúa aproximadamente al 55 % de opacidad. Esta señal visual coincide con el efecto de atenuación usado en la curva EQ y confirma que la etapa no está procesando audio. Vuelva a habilitar la etapa para restaurar la opacidad completa y el procesamiento activo.

## Pasos

1. Localice el mando **Ratio** en la fila de cinco mandos en la parte inferior del applet.
2. Para configurar el comportamiento de expansor suave, gire **Ratio** hacia un valor bajo (por ejemplo, 2.0:1). El audio por debajo del umbral se reduce gradualmente.
3. Para configurar el comportamiento de compuerta fuerte, gire **Ratio** hacia un valor alto (por ejemplo, 8.0:1 o superior). El audio por debajo del umbral se corta bruscamente.
4. Observe la barra de reducción de ganancia mientras el audio pasa. Un ajuste de expansor suave produce un relleno ámbar más superficial y gradual; un ajuste de compuerta fuerte produce un relleno profundo y abrupto cuando la compuerta se cierra.
5. Si el corte de la compuerta fuerte es demasiado severo entre palabras, ajuste **Floor** para limitar la atenuación máxima. Consulte [Ajustar Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).

## Qué hace cada control

| Control                | Predeterminado | Rango válido    |
|------------------------|----------------|-----------------|
| **Thresh**             | -40.0 dB       | -80.0 a 0.0 dB  |
| **Ratio**              | 2.0            | 1.0 a 10.0      |
| **Return**             | 2.0 dB         | 0.0 a 20.0 dB   |
| **Release**            | 100 ms         | 5 a 2000 ms     |
| **Floor**              | -15.0 dB       | -80.0 a 0.0 dB  |
| **Barra de reducción de ganancia** | —         | 0 a 40 dB GR    |
| Curva de transferencia  | —              | —               |

## Edición en línea de mandos

Cada mando en el applet admite edición de valor en línea. Haga clic en el valor mostrado de un mando para abrir un campo de texto editable superpuesto sobre el mando. Escriba un valor y presione Enter o haga clic en otro lugar para confirmar el cambio. El editor acepta formatos decimales adaptados a la configuración regional (por ejemplo, "12,5" en regiones que usan coma decimal) y elimina caracteres no numéricos, por lo que puede ingresar valores con unidades (por ejemplo, "−6 dB" o "12.5 ms"). Si ingresa un valor no válido, el mando vuelve silenciosamente a su ajuste anterior. Presione Escape para cancelar la edición sin confirmar un cambio.

## Consejos

- Una relación de 2.0:1 (la predeterminada) es un punto de partida conservador adecuado para la mayoría de los usos en TX. Auméntela solo si el ruido de bajo nivel sigue siendo audible cuando no está hablando.
- Con relaciones superiores a aproximadamente 8.0:1, la compuerta se comporta casi como un interruptor de encendido/apagado. Combínelo con un **Thresh** cuidadosamente ajustado para evitar recortar el borde inicial de las palabras.
- Use el mando **Return** para eliminar el parloteo de la compuerta. Si la compuerta se abre y cierra rápidamente cuando hace una pausa al hablar, aumente **Return** para que la compuerta permanezca abierta hasta que el nivel de entrada caiga claramente por debajo del umbral. La banda cian en la curva de transferencia se ensancha a medida que aumenta **Return**, mostrando directamente la zona de histéresis.
- La curva de transferencia se actualiza en tiempo real a medida que mueve **Ratio** o **Return**. Use la bola de entrada en vivo para confirmar que la forma de la curva y la banda de histéresis coinciden con su intención antes de transmitir.
- Los cambios en cualquier mando surten efecto inmediatamente y se guardan automáticamente. No se requiere ningún botón de Aplicar o Guardar.
- La barra de reducción de ganancia y la curva de transferencia se redibujan constantemente mientras la compuerta procesa audio. La pantalla se actualiza en cada fotograma de animación para garantizar que siempre vea la lectura actual del medidor sin ningún parpadeo visual.

## Solución de problemas

- **El mando Ratio no tiene efecto en el sonido** — Confirme que la etapa de compuerta está habilitada. Una compuerta en bypass pasa el audio sin modificaciones independientemente de los ajustes del mando; el mosaico del applet aparecerá atenuado aproximadamente al 55 % de opacidad cuando esté en bypass. Consulte [Poner en bypass la compuerta desde la cadena](bypass-the-gate-from-the-chain.md).
- **La relación de compuerta fuerte corta demasiado profundo y crea silencios antinaturales** — Baje **Floor** hacia 0 dB para reducir la atenuación máxima, o reduzca **Ratio** hacia el rango de expansor suave.
- **La relación de expansor suave no suprime suficiente ruido** — Aumente **Ratio** o baje **Thresh** para que la atenuación comience en un nivel de entrada más alto.
- **La compuerta parlotea o parpadea en el umbral** — Aumente **Return** para que la compuerta permanezca abierta hasta que la señal caiga más por debajo del umbral. Observe cómo la banda de histéresis cian en la curva de transferencia se ensancha al hacerlo.
- **El medidor o la curva de la pantalla parece entrecortarse** — El sistema de animación se repinta continuamente mientras se procesa audio. Si ve parpadeos, verifique que ninguna otra aplicación esté interfiriendo con la tubería de audio.

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-G (RX)](overview.md)
- [Establecer umbral TX justo por encima del piso de ruido ambiente](set-tx-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar silencio antinatural entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar Release para un cierre natural de compuerta](tune-release-for-natural-gate-close.md)
- [Observar GR en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
