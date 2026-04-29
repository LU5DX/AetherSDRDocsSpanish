# Ajuste de la profundidad de enmascaramiento y la intensidad de supresión de NR4

Los controles deslizantes **Masking Depth:** y **Suppression:** del motor NR4 permiten controlar con precisión la agresividad con que se aplica el enmascaramiento espectral y la intensidad general de supresión de ruido. Ajuste estos dos parámetros de forma conjunta para equilibrar la reducción de ruido con la claridad de la voz.

## Antes de comenzar

- Abra AetherSDR y active NR4 en el receptor que desea ajustar.
- Tenga activa una señal o fuente de ruido para escuchar el efecto de los cambios en tiempo real.

## Pasos

1. Haga clic en `Settings > AetherDSP Settings...`.
2. Haga clic en la pestaña **NR4**.
3. Localice el control deslizante **Masking Depth:**. Arrástrelo hacia la izquierda para reducir el enmascaramiento espectral o hacia la derecha para aumentarlo. El valor predeterminado es **0.50**; el rango válido es **0.00–1.00**.
4. Localice el control deslizante **Suppression:** directamente debajo. Arrástrelo hacia la izquierda para reducir la supresión general o hacia la derecha para aumentarla. El valor predeterminado es **0.50**; el rango válido es **0.00–1.00**.
5. Escuche el resultado. Si la voz suena sobrепrocesada o hueca, reduzca uno o ambos controles. Si el ruido residual es demasiado audible, auméntelos.
6. Para deshacer todos los cambios de NR4 a la vez, haga clic en **Reset Defaults**. Esto restaura **Masking Depth:** a **0.50** y **Suppression:** a **0.50**, junto con los demás valores predeterminados de NR4.

## Qué hace cada control

| Control | Predeterminado | Rango | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Masking Depth:** | 0.50 | 0.00–1.00 | `NR4MaskingDepth` | Controla la profundidad con que se aplica el enmascaramiento espectral a los contenedores de ruido. Valores más altos suprimen más ruido, pero pueden afectar la calidad tonal. |
| **Suppression:** | 0.50 | 0.00–1.00 | `NR4SuppressionStrength` | Establece la intensidad general de supresión de NR4. Valores más altos producen una reducción de ruido más agresiva en todo el espectro. |

## Consejos

- **Masking Depth:** y **Suppression:** interactúan entre sí: aumentar ambos a la vez produce la máxima reducción de ruido, pero también el mayor riesgo de distorsión en la voz. Auméntelos de forma incremental y realice pruebas con una señal en vivo o grabada.
- Si también tiene **Reduction (dB):** configurado en un valor alto, reducir ligeramente **Suppression:** puede recuperar la naturalidad sin perder mucha reducción del piso de ruido.
- La casilla **Adaptive Noise Estimation** afecta la velocidad con que NR4 sigue un piso de ruido cambiante, lo que a su vez influye en cómo suenan ambos controles en la práctica. Consulte [Activar o desactivar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md).
- Haga clic en **Reset Defaults** para devolver todos los parámetros de NR4 —no solo estos dos controles— a sus valores de fábrica antes de experimentar de nuevo.

## Solución de problemas

- **La voz suena hueca o como bajo el agua después de aumentar los controles** — Ambos controles con valores altos pueden suprimir en exceso componentes espectrales que se superponen con la voz. Reduzca primero **Masking Depth:** y luego **Suppression:** hasta que la naturalidad regrese.
- **El piso de ruido sigue siendo audible incluso con los ajustes al máximo** — Asegúrese de que **Adaptive Noise Estimation** esté activado para que NR4 pueda reestimar el piso de ruido de forma continua. Considere también aumentar **Reduction (dB):** mediante [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md).
- **El control vuelve a su posición o no se mueve** — Los controles deslizantes utilizan un modelo de entrada con protección. Haga clic directamente sobre el manejador del control en lugar de hacerlo en la ranura.

## Temas relacionados

- [Ajustar la cantidad de reducción de NR4 en dB](adjust-nr4-reduction-amount-in-db.md)
- [Activar o desactivar la estimación adaptativa de ruido de NR4](enable-or-disable-nr4-adaptive-noise-estimation.md)
- [Restablecer los parámetros de NR2 o NR4 a los valores predeterminados](reset-nr2-or-nr4-parameters-to-defaults.md)
- [Elección de la reducción de ruido adecuada: NR2, NR4, DFNR, MNR](../../operating/dsp/noise-reduction-overview.md)
