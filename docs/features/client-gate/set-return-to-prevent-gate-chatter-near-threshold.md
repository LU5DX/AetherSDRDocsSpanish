# Ajustar el retorno para evitar el trémolo cerca del umbral

Cuando los niveles de audio oscilan cerca del umbral, la puerta puede abrirse y cerrarse rápidamente, produciendo un efecto audible de trémolo. El control **Return** añade una banda muerta por histéresis para que la puerta no se cierre de nuevo hasta que la señal caiga una cantidad determinada por debajo del umbral donde se abrió.

## Antes de empezar

- La puerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) para confirmar que la etapa de puerta está activa.
- Ajuste primero el umbral (Thresh) para tener un punto de referencia estable. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-G** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP). Alternativamente, haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**.
2. Localice el control **Return**.
3. Gire **Return** hacia arriba desde su valor predeterminado de 2.0 dB hasta que el trémolo se detenga. Empiece con incrementos pequeños: de 3 a 5 dB suele ser suficiente para voz.
4. Observe la curva de transferencia. Aparece una banda vertical de color cian suave entre (Thresh − Return) y Thresh, mostrando la banda muerta por histéresis. Ajústela girando **Return** hasta que la banda cubra el rango donde fluctúa su señal.
5. Hable o pase audio a un nivel que antes causaba trémolo. Confirme que la puerta se abre limpiamente y no se vuelve a cerrar hasta que su nivel caiga por debajo del borde inferior de la banda cian.

## Función de cada control

| Control | Predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Return** | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Thresh** | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |
| **Ratio** | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` / `ClientGateRxRatio` |
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` |
| **Floor** | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` / `ClientGateRxFloorDb` |

**Return** establece la anchura de la banda muerta por histéresis en decibelios. La puerta se abre cuando la entrada supera Thresh y no se vuelve a cerrar hasta que la entrada cae por debajo de Thresh − Return. Si ajusta Return a 0.0 dB, la banda muerta se elimina por completo; la puerta se abre y se cierra al mismo nivel, lo que maximiza el riesgo de trémolo cerca del umbral.

**Ratio** controla la pendiente de la expansión descendente. Las relaciones más altas (cercanas a 10.0) producen un corte más duro, similar a una puerta; las relaciones más bajas (cercanas a 1.0) actúan como un expansor descendente suave. La etiqueta se muestra como `X.X:1`.

**Release** determina la rapidez con que se cierra la puerta después de que la entrada caiga por debajo de Thresh − Return. El rango es de 5 a 2000 ms con mapeo exponencial. Por debajo de 100 ms, la etiqueta muestra `X.X ms`; por encima de 100 ms, muestra `X ms`.

**Floor** establece la atenuación máxima que puede aplicar la puerta. El valor predeterminado es −15.0 dB; el rango es de −80.0 a 0.0 dB.

La curva de transferencia dibuja una banda vertical de color cian suave entre (Thresh − Return) y Thresh siempre que Return sea mayor que 0.0 dB. Esta banda es la zona de adherencia de la puerta: las señales dentro de ella dejan la puerta en el estado en que se encuentre.

## Edición de valor en línea

Cada control en Aetherial TX Gate y Aetherial AGC-G admite entrada numérica directa. Haga clic en el valor mostrado debajo de un control para activar un editor en línea que reemplaza la etiqueta pintada. El editor aparece idéntico a la etiqueta normal hasta que se enfoca, momento en el que un fondo oscuro sutil y un borde cian indican el modo de edición.

1. Haga clic en el texto del valor debajo de cualquier control (Thresh, Ratio, Return, Release o Floor).
2. Escriba el valor deseado usando la convención de unidad del control. Por ejemplo, escriba `15` para ajustar Return a 15 dB, o `2` para ajustar Ratio a 2.0.
3. Presione **Enter** para confirmar el valor, o haga clic en cualquier otro lugar del applet para aplicar el cambio.
4. Para cancelar, presione **Escape** mientras el editor esté activo. El valor vuelve a su ajuste anterior.

El editor acepta separadores decimales según la configuración regional (por ejemplo, `12,5` en regiones que usan coma decimal) y elimina texto de unidad final como "dB" o "ms". La entrada no válida se revierte silenciosamente al último valor válido.

El ajuste de los controles mediante arrastre del ratón o la rueda del ratón sigue funcionando mientras el editor no está enfocado.

## Apariencia cuando está en derivación

Cuando la etapa de puerta está en derivación, todo el mosaico del applet se atenúa con una opacidad reducida. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona un recordatorio visual de que la puerta no está procesando audio. Vuelva a habilitar la etapa de puerta para restaurar la opacidad completa y reanudar el procesamiento. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Consejos

- Si sube tanto Return que la puerta permanece abierta durante pausas largas en el habla, reduzca Return en pequeños pasos (0.5 dB cada vez) hasta que las pausas cierren la puerta de forma natural.
- Use la barra de reducción de ganancia (franja ámbar, escala de 0 a 40 dB, con una marca en −15 dB) para confirmar que la puerta se cierra durante el silencio real. Si la barra nunca se llena durante una pausa, puede que Return sea demasiado amplio en relación con su nivel de ruido real.
- Los cambios en Return surten efecto inmediatamente y se guardan automáticamente. No es necesario reiniciar.

## Solución de problemas

- **El trémolo persiste después de aumentar Return** — Es posible que Thresh esté ajustado demasiado cerca de una señal ruidosa que fluctúa ampliamente. Baje Thresh ligeramente para que la puerta se abra solo con voz clara y luego reajuste Return.
- **La puerta permanece abierta permanentemente** — Return es más amplio que la diferencia entre su nivel de señal y el ruido de fondo. Reduzca Return hasta que la puerta se cierre de forma fiable durante el silencio.
- **La banda cian no es visible en la curva de transferencia** — Return está ajustado a 0.0 dB. Cualquier valor superior a 0.0 dB mostrará la banda.
- **El mosaico del applet aparece atenuado** — La etapa de puerta está en derivación. Habilite la etapa de puerta para restaurar la opacidad completa y el procesamiento activo.
- **El editor en línea no aparece al hacer clic en el valor** — Es posible que el control no admita la edición en línea en su configuración actual, o que el editor esté desactivado. Los cinco controles en el applet de puerta admiten esta función de forma predeterminada.
- **La barra de reducción de ganancia no muestra relleno ámbar** — La puerta está actualmente abierta sin atenuación aplicada. Hable o pase audio por debajo de Thresh para ver la puerta cerrarse y la barra llenarse.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Tune release for natural gate close](tune-release-for-natural-gate-close.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
