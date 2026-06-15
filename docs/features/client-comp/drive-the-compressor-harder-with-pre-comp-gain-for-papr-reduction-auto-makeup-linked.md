# Impulse más fuerte el compresor con la ganancia previa para reducción de PAPR (auto-makeup vinculado)

Use el mando Drive para enviar más señal al compresor antes del umbral y recupere automáticamente esa ganancia en la salida. Esto permite trabajar el compresor con más intensidad — aumentando la reducción de la relación pico a potencia promedio (PAPR) — mientras mantiene su nivel RMS promedio sin cambios, para que no tenga que reajustar el mando Makeup.

## Antes de empezar

- Confirme que el compresor de TX está activado (haga clic en el mosaico del compresor en el widget CHAIN para que se muestre como activo, no atenuado).
- Abra el panel flotante StripCompPanel haciendo doble clic en el mosaico COMP en el lado TX del widget CHAIN.

## Pasos

1. Localice el mando Drive en la columna derecha del panel flotante StripCompPanel (etiquetado como `+X.X dB`).
2. Gire Drive en sentido horario desde su valor predeterminado `0.0 dB` (rango: `0.0` a `18.0 dB`). Cada dB de Drive empuja más señal por encima del umbral, por lo que el compresor actúa con más fuerza sobre los picos.
3. Opcionalmente, combine Drive con el mando Phase Rotator (también en la columna derecha); consulte la tarea relacionada para configurar la rotación de fase y reducir aún más el PAPR.

El medidor de reducción de ganancia del compresor y la bola en vivo en la curva de transferencia mostrarán más actividad a medida que aumente Drive. El auto-makeup garantiza que su nivel de salida no disminuya al aumentar la compresión, por lo que su mando Makeup sigue siendo un ajuste final limpio posterior a todo.

## Qué hace cada control

| Control | Predeterminado | Rango válido        | Clave de configuración           |
|---------|----------------|---------------------|----------------------------------|
| Drive   | `0.0 dB`       | `0.0` a `18.0 dB`   | `ClientCompTxDriveDb`            |
| Phase   | `0 etapas`     | `0` a `6 etapas`    | `ClientCompTxPhaseRotatorStages` |
| Thresh  | `-18.0 dB`     | `-60.0` a `0.0 dB`  | `ClientCompTxThresholdDb`        |
| Ratio   | `3.0`          | `1.0` a `20.0`      | `ClientCompTxRatio`              |
| Attack  | `20.0 ms`      | `0.1` a `300.0 ms`  | `ClientCompTxAttackMs`           |
| Release | `200 ms`       | `5` a `2000 ms`     | `ClientCompTxReleaseMs`          |
| Makeup  | `0.0 dB`       | `-12.0` a `24.0 dB` | `ClientCompTxMakeupDb`           |

## Consejos

- Drive está diseñado para usarse *antes* de tocar Makeup. Con el auto-makeup activo, puede aumentar Drive para obtener una compresión más intensa sin perder nivel promedio.
- La configuración predeterminada de transmisión de Phase Rotator es 4 etapas. Comience allí y escuche picos más limpios y simétricos.
- El mando Drive solo está disponible en el panel flotante StripCompPanel; no aparece en el mosaico compacto del applet.

## Relacionado

- [Open the full Compressor editor for knee, limiter, Drive, and Phase controls](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Rotate voice phase symmetry with the Phase rotator (0–6 stages at staggered frequencies)](rotate-voice-phase-symmetry-with-the-phase-rotator-0-6-stages-at-staggered-frequencies.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
