# Ajuste de Retorno para evitar el chisporroteo de la puerta cerca del umbral

Cuando los niveles de audio fluctúan cerca del umbral, la puerta puede abrirse y cerrarse rápidamente, produciendo un efecto de chisporroteo audible llamado "chatter". El mando de Retorno añade una banda muerta de histéresis para que la puerta no se cierre de nuevo hasta que la señal caiga una cantidad determinada por debajo del umbral en el que se abrió.

## Antes de empezar

- La puerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) para confirmar que la etapa de puerta está activa.
- Ajuste primero Thresh para tener un punto de referencia estable. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-G** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP). Alternativamente, haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**.
2. Localice el mando **Return**.
3. Gire **Return** hacia arriba desde su valor predeterminado de 2.0 dB hasta que el chisporroteo se detenga. Comience con pequeños incrementos; de 3 a 5 dB suele ser suficiente para voz.
4. Observe la curva de transferencia. Aparece una banda vertical cian claro entre (Thresh − Return) y Thresh, mostrando la banda muerta de histéresis. Ajústela girando **Return** hasta que la banda cubra el rango donde fluctúa su señal.
5. Hable o pase audio a un nivel que antes causaba chisporroteo. Confirme que la puerta se abre limpiamente y no se vuelve a cerrar hasta que su nivel caiga por debajo del borde inferior de la banda cian.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Thresh** | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |
| **Ratio** | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` |
| **Return** | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |
| **Floor** | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` |

**Return** establece el ancho de la banda muerta de histéresis en decibelios. La puerta se abre cuando la entrada supera Thresh y no se cierra de nuevo hasta que la entrada cae por debajo de Thresh − Return. Establecer Return a 0.0 dB elimina completamente la banda muerta; la puerta se abre y se cierra al mismo nivel, lo que maximiza el riesgo de chisporroteo cerca del umbral.

**Ratio** controla la inclinación de la expansión descendente. Las relaciones más altas (cercanas a 10.0) producen un corte más duro, similar a una puerta; las relaciones más bajas (cercanas a 1.0) actúan como un expansor descendente suave. La etiqueta se muestra como `X.X:1`.

**Release** determina la rapidez con la que se cierra la puerta después de que la entrada caiga por debajo de Thresh − Return. El rango es de 5 a 2000 ms con mapeo exponencial. Por debajo de 100 ms, la etiqueta muestra `X.X ms`; por encima de 100 ms, muestra `X ms`.

**Floor** establece la atenuación máxima que puede aplicar la puerta. El valor predeterminado es −15.0 dB; el rango es de −80.0 a 0.0 dB.

La curva de transferencia dibuja una banda vertical cian claro entre (Thresh − Return) y Thresh siempre que Return sea mayor que 0.0 dB. Esta banda es la zona adhesiva de la puerta: las señales dentro de ella dejan la puerta en el estado en que se encuentre.

## Curva de transferencia e indicadores en vivo

El indicador **Curva de transferencia** traza la curva de transferencia estática del expansor y una bola en vivo en el nivel de entrada actual. Aparece una banda vertical cian claro entre (Thresh − Return) y Thresh para hacer visible la banda muerta de histéresis.

La **Barra de reducción de ganancia** es una tira horizontal de color ámbar, rellena desde la derecha, con una escala que llega hasta 40 dB. Una marca en -15 dB señala el valor predeterminado del expansor suave. La barra se llena para mostrar la profundidad de atenuación mientras la puerta está cerrada.

La **Bola de entrada** en la curva de transferencia muestra si la puerta está actualmente abierta o cerrada según su posición relativa al umbral y la banda de histéresis.

La animación de la barra de reducción de ganancia y la bola de entrada utiliza un temporizador preciso para actualizaciones visuales suaves. Cuando el nivel de audio se estabiliza, el temporizador de la animación se detiene para conservar CPU. Si el valor suavizado cambia entre tics, el widget se redibuja inmediatamente sin esperar al siguiente intervalo del temporizador, asegurando una retroalimentación visual receptiva incluso durante cambios rápidos de nivel.

## Edición de valor en línea

Cada mando en Aetherial TX Gate y Aetherial AGC-G admite entrada numérica directa. Haga clic en el valor mostrado debajo de un mando para activar un editor en línea que reemplaza la etiqueta pintada. El editor aparece idéntico a la etiqueta normal hasta que se enfoca, momento en el que un fondo oscuro sutil y un borde cian indican el modo de edición.

1. Haga clic en el texto del valor debajo de cualquier mando (Thresh, Ratio, Return, Release o Floor).
2. Escriba el valor deseado utilizando la convención de unidad del mando. Por ejemplo, escriba `15` para establecer Return en 15 dB, o `2` para establecer Ratio en 2.0.
3. Presione **Enter** para confirmar el valor, o haga clic en cualquier otro lugar del applet para aplicar el cambio.
4. Para cancelar, presione **Escape** mientras el editor esté activo. El valor vuelve a su configuración anterior.

El editor acepta separadores decimales según la configuración regional (por ejemplo, `12,5` en configuraciones regionales que usan coma decimal) y elimina el texto de unidad final como "dB" o "ms". La entrada no válida se revierte silenciosamente al último valor válido.

El ajuste del mando mediante arrastre del ratón o rueda del ratón continúa funcionando mientras el editor no esté enfocado.

## Apariencia en bypass

Cuando la etapa de puerta está en bypass, todo el mosaico del applet se atenúa a una opacidad reducida. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona un recordatorio visual de que la puerta no está procesando audio. Vuelva a habilitar la etapa de puerta para restaurar la opacidad completa y reanudar el procesamiento. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Consejos

- Si eleva Return tanto que la puerta permanece abierta durante pausas largas en el habla, redúzcalo en pequeños pasos (0.5 dB a la vez) hasta que las pausas cierren la puerta de forma natural.
- Utilice la barra de reducción de ganancia (tira ámbar, escala de 0 a 40 dB, con una marca en -15 dB) para confirmar que la puerta se cierra durante el silencio real. Si la barra nunca se llena durante una pausa, Return puede ser demasiado amplio en relación con su nivel de ruido real.
- Los cambios en Return surten efecto inmediatamente y se guardan automáticamente. No es necesario reiniciar.

## Solución de problemas

- **El chisporroteo persiste después de aumentar Return** — Thresh puede estar ajustado demasiado cerca de una señal ruidosa que fluctúa ampliamente. Baje Thresh ligeramente para que la puerta se abra solo con habla clara, luego reajuste Return.
- **La puerta permanece abierta permanentemente** — Return está ajustado más amplio que la brecha entre el nivel de su señal y el piso de ruido. Reduzca Return hasta que la puerta se cierre de manera confiable durante el silencio.
- **La banda cian no es visible en la curva de transferencia** — Return está ajustado a 0.0 dB. Cualquier valor por encima de 0.0 dB hará que se renderice la banda.
- **El mosaico del applet aparece atenuado** — La etapa de puerta está en bypass. Habilite la etapa de puerta para restaurar la opacidad completa y el procesamiento activo.
- **El editor en línea no aparece al hacer clic en el valor** — Es posible que el mando no admita la edición en línea en su configuración actual, o que el editor esté deshabilitado. Los cinco mandos en el applet de puerta admiten esta función de forma predeterminada.
- **La barra de reducción de ganancia no muestra relleno ámbar** — La puerta está actualmente abierta sin atenuación aplicada. Hable o pase audio por debajo de Thresh para ver cómo se cierra la puerta y se llena la barra.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Tune release for natural gate close](tune-release-for-natural-gate-close.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
