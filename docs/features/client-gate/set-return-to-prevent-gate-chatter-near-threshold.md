# Ajuste de Return para evitar el parloteo de la compuerta cerca del umbral

Cuando los niveles de audio rondan cerca del umbral, la compuerta puede abrirse y cerrarse rápidamente, produciendo un efecto de tartamudeo audible llamado parloteo. La perilla Return añade una histéresis de banda muerta para que la compuerta no se cierre nuevamente hasta que la señal caiga una cantidad determinada por debajo del umbral donde se abrió.

## Antes de comenzar

- La compuerta debe estar habilitada en el lado TX o RX. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md) para confirmar que la etapa de compuerta esté activa.
- Ajuste primero Thresh para tener un punto de referencia estable. Consulte [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el subcontenedor **Aetherial TX Gate** (lado TX) o el subcontenedor **Aetherial AGC-G** (lado RX) dentro del contenedor principal Aetherial Audio (TXDSP). Alternativamente, haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante titulado **Aetherial Gate — TX** o **Aetherial Gate — RX**.
2. Localice la perilla **Return**.
3. Gire **Return** hacia arriba desde su valor predeterminado de 2.0 dB hasta que el parloteo se detenga. Comience con incrementos pequeños — de 3 a 5 dB suele ser suficiente para voz.
4. Observe la curva de transferencia. Una banda vertical de color cian claro aparece entre (Thresh − Return) y Thresh, mostrando la banda muerta de histéresis. Amplíela o redúzcala ajustando **Return** hasta que la banda cubra el rango donde fluctúa su señal.
5. Hable o pase audio a un nivel que antes causaba parloteo. Confirme que la compuerta se abre limpiamente y no se vuelve a cerrar hasta que su nivel caiga por debajo del borde inferior de la banda cian.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| **Return** | 2.0 dB | 0.0 a 20.0 dB | `ClientGateTxReturnDb` / `ClientGateRxReturnDb` |
| **Thresh** | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` / `ClientGateRxThresholdDb` |

**Return** establece el ancho de la banda muerta de histéresis en decibelios. La compuerta se abre cuando la entrada supera Thresh y no se cierra nuevamente hasta que la entrada cae por debajo de Thresh − Return. Establecer Return en 0.0 dB elimina la banda muerta por completo; la compuerta se abre y se cierra en el mismo nivel, lo que maximiza el riesgo de parloteo cerca del umbral.

La curva de transferencia dibuja una banda vertical de color cian claro entre (Thresh − Return) y Thresh siempre que Return sea mayor que 0.0 dB. Esta banda es la zona pegajosa de la compuerta — las señales dentro de ella mantienen la compuerta en el estado en que ya se encuentre.

## Edición de valor en línea

Cada perilla en Aetherial TX Gate y Aetherial AGC-G admite entrada numérica directa. Haga clic en el valor mostrado debajo de una perilla para activar un editor en línea que reemplaza la etiqueta pintada. El editor aparece idéntico a la etiqueta normal hasta que se enfoca, momento en el cual un sutil fondo oscuro y un borde cian indican el modo de edición.

1. Haga clic en el texto del valor debajo de cualquier perilla (Thresh, Ratio, Return, Release o Floor).
2. Escriba el valor deseado usando la convención de unidad de la perilla. Por ejemplo, escriba `15` para establecer Return en 15 dB.
3. Presione **Enter** para confirmar el valor, o haga clic en cualquier otro lugar del applet para aplicar el cambio.
4. Para cancelar, presione **Escape** mientras el editor esté activo. El valor vuelve a su configuración anterior.

El editor acepta separadores decimales según la configuración regional (por ejemplo, `12,5` en configuraciones de coma decimal) y elimina texto de unidad final como "dB" o "ms". Las entradas no válidas se revierten silenciosamente al último valor válido.

El ajuste de perilla mediante arrastre del ratón o rueda del ratón continúa funcionando mientras el editor no esté enfocado.

## Apariencia en bypass

Cuando la etapa de compuerta está en bypass, todo el mosaico del applet se atenúa con una opacidad reducida. Esto coincide con el efecto de atenuación utilizado en la curva del ecualizador y proporciona un recordatorio visual de que la compuerta no está procesando audio. Vuelva a habilitar la etapa de compuerta para restaurar la opacidad completa y reanudar el procesamiento. Consulte [Bypass the gate from the chain](bypass-the-gate-from-the-chain.md).

## Consejos

- Si eleva Return tanto que la compuerta permanece abierta durante pausas largas en el habla, redúzcalo en pequeños pasos (0.5 dB a la vez) hasta que las pausas cierren la compuerta de forma natural.
- Use la barra de reducción de ganancia (franja ámbar, escala de 0 a 40 dB) para confirmar que la compuerta se cierra durante el silencio real. Si la barra nunca se llena durante una pausa, Return puede ser demasiado amplio en relación con su piso de ruido real.
- Los cambios en Return surten efecto inmediatamente y se guardan automáticamente. No se requiere reinicio.

## Solución de problemas

- **El parloteo persiste después de aumentar Return** — Thresh puede estar configurado demasiado cerca de una señal ruidosa que fluctúa ampliamente. Baje Thresh ligeramente para que la compuerta se abra solo con habla clara, luego reajuste Return.
- **La compuerta permanece abierta permanentemente** — Return está configurado más ancho que la brecha entre el nivel de su señal y el piso de ruido. Reduzca Return hasta que la compuerta se cierre de manera confiable durante el silencio.
- **La banda cian no es visible en la curva de transferencia** — Return está configurado en 0.0 dB. Cualquier valor superior a 0.0 dB mostrará la banda.
- **El mosaico del applet aparece atenuado** — La etapa de compuerta está en bypass. Habilite la etapa de compuerta para restaurar la opacidad completa y el procesamiento activo.
- **El editor en línea no aparece al hacer clic en el valor** — La perilla puede no admitir la edición en línea en su configuración actual, o el editor puede estar deshabilitado. Las cinco perillas en el applet de compuerta admiten esta función de forma predeterminada.

## Relacionados

- [Set TX threshold just above room noise floor](set-tx-threshold-just-above-room-noise-floor.md)
- [Tune release for natural gate close](tune-release-for-natural-gate-close.md)
- [Watch live GR while not speaking](watch-live-gr-while-not-speaking.md)
- [Choose gate vs soft-expander behaviour via ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
