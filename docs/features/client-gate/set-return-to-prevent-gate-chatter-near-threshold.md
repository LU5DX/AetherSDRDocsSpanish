# Ajuste de Retorno (Return) para evitar el parloteo del compuerta cerca del umbral

Cuando los niveles de audio oscilan cerca del umbral, la compuerta puede abrirse y cerrarse rápidamente, produciendo un efecto de tartamudeo audible llamado parloteo (chatter). El mando de Retorno (Return) añade una banda muerta de histéresis para que la compuerta no se cierre nuevamente hasta que la señal caiga una cantidad determinada por debajo del umbral donde se abrió.

## Antes de empezar

- La compuerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) para confirmar que la etapa de compuerta esté activa.
- Ajuste primero el umbral (Thresh) para tener un punto de referencia estable. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-G** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP). Alternativamente, haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**.
2. Localice el mando **Return**.
3. Gire **Return** hacia arriba desde su valor predeterminado de 2.0 dB hasta que el parloteo se detenga. Comience con incrementos pequeños: de 3 a 5 dB suele ser suficiente para voz.
4. Observe la curva de transferencia. Aparece una banda vertical cian suave entre (Thresh − Return) y Thresh, que muestra la banda muerta de histéresis. Ajústela girando **Return** hasta que la banda cubra el rango donde fluctúa su señal.
5. Hable o pase audio a un nivel que antes causaba parloteo. Confirme que la compuerta se abre limpiamente y no se cierra de nuevo hasta que su nivel caiga por debajo del borde inferior de la banda cian.

## Función de cada control

| Control | Predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Thresh** | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |
| **Ratio** | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` |
| **Return** | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |
| **Floor** | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` |

**Return** establece el ancho de la banda muerta de histéresis en decibelios. La compuerta se abre cuando la entrada supera Thresh y no se cierra de nuevo hasta que la entrada cae por debajo de Thresh − Return. Configurar Return a 0.0 dB elimina la banda muerta por completo; la compuerta se abre y se cierra en el mismo nivel, lo que maximiza el riesgo de parloteo cerca del umbral.

**Ratio** controla la inclinación de la expansión descendente. Las relaciones más altas (cercanas a 10.0) producen un corte más duro, similar a una compuerta; las relaciones más bajas (cercanas a 1.0) actúan como un expansor descendente suave. La etiqueta se muestra como `X.X:1`.

**Release** determina qué tan rápido se cierra la compuerta después de que la entrada cae por debajo de Thresh − Return. El rango es de 5 a 2000 ms con mapeo exponencial. Por debajo de 100 ms, la etiqueta muestra `X.X ms`; por encima de 100 ms, muestra `X ms`.

**Floor** establece la atenuación máxima que puede aplicar la compuerta. El valor predeterminado es −15.0 dB; el rango es de −80.0 a 0.0 dB.

La curva de transferencia dibuja una banda vertical cian suave entre (Thresh − Return) y Thresh cuando Return es mayor que 0.0 dB. Esta banda es la zona pegajosa de la compuerta: las señales dentro de ella dejan la compuerta en el estado en el que ya se encuentra.

## Curva de transferencia e indicadores en vivo

El indicador **Curva de transferencia** representa la curva de transferencia estática del expansor y una bola en vivo al nivel de entrada actual. Aparece una banda vertical cian suave entre (Thresh − Return) y Thresh para hacer visible la banda muerta de histéresis.

La **Barra de reducción de ganancia** es una barra horizontal ámbar rellena por la derecha, con una escala que alcanza un máximo de 40 dB. Una marca en -15 dB señala el valor de piso predeterminado del expansor suave. La barra se llena para mostrar la profundidad de la atenuación mientras la compuerta está cerrada.

La **Bola de entrada** en la curva de transferencia muestra si la compuerta está actualmente abierta o cerrada según su posición relativa al umbral y la banda de histéresis.

La animación de la barra de reducción de ganancia y la bola de entrada utiliza un temporizador preciso para obtener actualizaciones visuales suaves. Cuando el nivel de audio se estabiliza, el temporizador de animación se detiene para conservar CPU. El widget se vuelve a dibujar continuamente durante la animación para garantizar una retroalimentación visual receptiva.

## Edición de valor en línea

Cada mando en Aetherial TX Gate y Aetherial AGC-G admite la entrada numérica directa. Haga clic en el valor mostrado debajo de un mando para activar un editor en línea que reemplaza la etiqueta pintada. El editor aparece idéntico a la etiqueta normal hasta que se enfoca, momento en el cual un sutil fondo oscuro y un borde cian indican el modo de edición.

1. Haga clic en el texto del valor debajo de cualquier mando (Thresh, Ratio, Return, Release o Floor).
2. Escriba el valor deseado usando la convención de unidad del mando. Por ejemplo, escriba `15` para configurar Return a 15 dB, o `2` para configurar Ratio a 2.0.
3. Presione **Enter** para confirmar el valor, o haga clic en cualquier otro lugar del applet para aplicar el cambio.
4. Para cancelar, presione **Escape** mientras el editor esté activo. El valor vuelve a su configuración anterior.

El editor acepta separadores decimales según la configuración regional (por ejemplo, `12,5` en locales de coma decimal) y elimina texto de unidad final como "dB" o "ms". La entrada no válida se revierte silenciosamente al último valor válido.

El ajuste del mando mediante arrastre del ratón o rueda del ratón sigue funcionando mientras el editor no esté enfocado.

## Apariencia en bypass

Cuando la etapa de compuerta está en bypass, todo el mosaico del applet se atenúa con opacidad reducida. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona un recordatorio rápido de que la compuerta no está procesando audio. Vuelva a habilitar la etapa de compuerta para restaurar la opacidad completa y reanudar el procesamiento. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Consejos

- Si eleva tanto Return que la compuerta permanece abierta durante pausas largas en el habla, redúzcalo en pequeños pasos (0.5 dB a la vez) hasta que las pausas cierren la compuerta de forma natural.
- Use la barra de reducción de ganancia (franja ámbar, escala de 0 a 40 dB, con una marca en -15 dB) para confirmar que la compuerta se cierra durante el silencio real. Si la barra nunca se llena durante una pausa, Return puede ser demasiado amplio en relación con su piso de ruido real.
- Los cambios en Return surten efecto de inmediato y se guardan automáticamente. No es necesario reiniciar.

## Solución de problemas

- **El parloteo persiste después de aumentar Return** — Es posible que Thresh esté configurado demasiado cerca de una señal ruidosa que fluctúa ampliamente. Baje ligeramente Thresh para que la compuerta se abra solo con el habla clara y luego reajuste Return.
- **La compuerta permanece abierta permanentemente** — Return está configurado más amplio que la brecha entre el nivel de su señal y el piso de ruido. Reduzca Return hasta que la compuerta se cierre de manera confiable durante el silencio.
- **La banda cian no es visible en la curva de transferencia** — Return está configurado a 0.0 dB. Cualquier valor superior a 0.0 dB mostrará la banda.
- **El mosaico del applet aparece atenuado** — La etapa de compuerta está en bypass. Habilite la etapa de compuerta para restaurar la opacidad completa y el procesamiento activo.
- **El editor en línea no aparece al hacer clic en el valor** — Es posible que el mando no admita la edición en línea en su configuración actual, o que el editor esté deshabilitado. Los cinco mandos del applet de compuerta admiten esta función de forma predeterminada.
- **La barra de reducción de ganancia no muestra relleno ámbar** — La compuerta está actualmente abierta sin atenuación aplicada. Hable o pase audio por debajo de Thresh para ver la compuerta cerrarse y la barra llenarse.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Tune release for natural gate close](tune-release-for-natural-gate-close.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
