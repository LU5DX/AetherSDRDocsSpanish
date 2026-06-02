# Elegir entre comportamiento de puerta y expansor suave mediante la relación de compresión

El control **Ratio** (Relación de compresión) determina cuán agresivamente la puerta atenúa el audio por debajo del umbral. Configurar una relación baja produce un expansor descendente suave que reduce gradualmente el audio silencioso; configurar una relación alta produce una puerta fuerte que lo corta de forma abrupta. Elegir la relación adecuada le permite adaptar el carácter de la puerta a su situación de ruido y estilo de operación.

## Antes de comenzar

- La etapa de puerta debe estar habilitada en el lado que desea ajustar (TX o RX). Si el applet no está visible, habilite la puerta a través del widget CHAIN o haga doble clic en la etapa GATE para abrir el editor flotante.
- Abra el subcontenedor **Aetherial TX Gate** (TX) o el subcontenedor **Aetherial AGC-G** (RX) dentro del contenedor principal Aetherial Audio (TXDSP) en el Panel de Applets.
- Cuando una etapa de puerta está en bypass, todo el mosaico del applet se atenúa hasta aproximadamente un 55 % de opacidad. Esta señal visual coincide con el efecto de atenuación utilizado en la curva de EQ y confirma que la etapa no está procesando audio. Vuelva a habilitar la etapa para restaurar la opacidad completa y el procesamiento activo.

## Pasos

1. Localice el control **Ratio** en la fila de cinco controles en la parte inferior del applet.
2. Para configurar un comportamiento de expansor suave, gire **Ratio** hacia un valor bajo (por ejemplo, 2.0:1). El audio por debajo del umbral se reduce gradualmente.
3. Para configurar un comportamiento de puerta fuerte, gire **Ratio** hacia un valor alto (por ejemplo, 8.0:1 o superior). El audio por debajo del umbral se corta abruptamente.
4. Observe la barra de reducción de ganancia mientras el audio pasa. Una configuración de expansor suave produce un relleno ámbar más superficial y gradual; una configuración de puerta fuerte produce un relleno profundo y abrupto cuando la puerta se cierra.
5. Si el corte de la puerta fuerte es demasiado severo entre palabras, ajuste **Floor** para limitar la atenuación máxima. Consulte [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md).

## Qué hace cada control

| Control                | Valor predeterminado | Rango válido   |
|------------------------|----------------------|----------------|
| **Thresh**             | -40.0 dB             | -80.0 a 0.0 dB |
| **Ratio**              | 2.0                  | 1.0 a 10.0     |
| **Return**             | 2.0 dB               | 0.0 a 20.0 dB  |
| **Release**            | 100 ms               | 5 a 2000 ms    |
| **Floor**              | -15.0 dB             | -80.0 a 0.0 dB |
| **Barra de reducción de ganancia** | —       | 0 a 40 dB GR   |
| Curva de transferencia | —                    | —              |

## Edición en línea de los controles

Cada control en el applet admite la edición de valores en línea. Haga clic en el valor mostrado de un control para abrir un campo de texto editable superpuesto sobre el control. Escriba un nuevo valor y presione Enter o haga clic en otro lugar para confirmar el cambio. El editor acepta formatos decimales compatibles con la configuración regional (por ejemplo, "12,5" en configuraciones regionales que usan coma decimal) y elimina caracteres no numéricos, por lo que puede ingresar valores con unidades (por ejemplo, "−6 dB" o "12.5 ms"). Si ingresa un valor no válido, el control vuelve silenciosamente a su configuración anterior. Presione Escape para cancelar la edición sin confirmar un cambio.

## Consejos

- Una relación de 2.0:1 (el valor predeterminado) es un punto de partida conservador adecuado para la mayoría de los usos en TX. Auméntela solo si el ruido de bajo nivel aún es audible cuando no está hablando.
- Con relaciones superiores a aproximadamente 8.0:1, la puerta se comporta casi como un interruptor de encendido/apagado. Combine esto con un **Thresh** cuidadosamente ajustado para evitar recortar el borde inicial de las palabras.
- Utilice el control **Return** para eliminar el parloteo de la puerta. Si la puerta se abre y se cierra rápidamente cuando hace una pausa al hablar, aumente **Return** para que la puerta permanezca abierta hasta que el nivel de entrada caiga muy por debajo del umbral. La banda cian en la curva de transferencia se ensancha a medida que aumenta **Return**, mostrando directamente la zona de histéresis.
- La curva de transferencia se actualiza en tiempo real a medida que mueve **Ratio** o **Return**. Use el punto de entrada en vivo para confirmar que la forma de la curva y la banda de histéresis coinciden con su intención antes de transmitir.
- Los cambios en cualquier control surten efecto de inmediato y se guardan automáticamente. No se requiere ningún botón Aplicar o Guardar.

## Solución de problemas

- **El control Ratio no tiene efecto en el sonido** — Confirme que la etapa de puerta esté habilitada. Una puerta en bypass pasa el audio sin modificaciones independientemente de la configuración del control; el mosaico del applet aparecerá atenuado aproximadamente al 55 % de opacidad cuando esté en bypass. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).
- **La relación de puerta fuerte corta demasiado y crea silencios no naturales** — Reduzca **Floor** hacia 0 dB para disminuir la atenuación máxima, o reduzca **Ratio** hacia el rango de expansor suave.
- **La relación de expansor suave no suprime el ruido lo suficiente** — Aumente **Ratio** o reduzca **Thresh** para que la atenuación comience a un nivel de entrada más alto.
- **La puerta parpadea o oscila en el umbral** — Aumente **Return** para que la puerta permanezca abierta hasta que la señal caiga aún más por debajo del umbral. Observe cómo la banda cian de histéresis en la curva de transferencia se ensancha al hacerlo.

## Relacionados

- [Aetherial TX Gate / Aetherial AGC-G (RX) overview](overview.md)
- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Set Floor to avoid unnatural silence between words](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Tune release for natural gate close](tune-release-for-natural-gate-close.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
