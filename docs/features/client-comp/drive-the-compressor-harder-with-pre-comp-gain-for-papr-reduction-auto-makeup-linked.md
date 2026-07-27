# Compresor Aetherial (TX) / AGC-C Aetherial (RX)

Compresor de rango dinámico del lado del cliente. El applet crea una copia vinculada a TX ("Compresor Aetherial") y una copia vinculada a RX ("AGC-C Aetherial") con estado completamente independiente. Ambas muestran la curva de transferencia estática con una "bola" animada que sigue la envolvente actual, un medidor horizontal de reducción de ganancia (20 dB máx.) y cinco perillas de ajuste — Thresh, Ratio, Attack, Release, Makeup — para controlar los picos de voz (TX) o de audio (RX) sin abrir el editor flotante. El StripCompPanel flotante (haga doble clic en el mosaico COMP del widget CHAIN) añade Knee, Ceiling, Makeup, un botón para activar/desactivar el limitador, una perilla Drive de precompresión (0–18 dB) con ganancia de compensación automática vinculada a Drive (el RMS sube junto con los picos), y una perilla Phase Rotator (0–6 etapas de paso total a frecuencias escalonadas de 300/700/1500/2500 Hz con 1000/2000 Hz opcionales, valor predeterminado de transmisión 4) para la reducción de la relación pico a potencia promedio (PAPR).

## Controles en el mosaico compacto del applet

| Control | Tipo | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---------|------|----------------------|--------------|-----------------|----------------|
| Curva de transferencia | indicador | — | — | — | ClientCompCurveWidget en modo compacto. Dibuja la curva de transferencia de entrada/salida más una bola animada que muestra el nivel actual de la envolvente. Solo visualización en el applet; editable en el ClientCompEditor flotante. |
| Barra de reducción de ganancia | medidor | — | 0 a 20 dB GR | — | Franja horizontal de color ámbar, rellena desde la derecha. La escala máxima es de 20 dB de reducción; una marca en -6 dB indica una cantidad de trabajo típica. Se consulta a ~30 Hz desde `ClientComp::gainReductionDb()`; la balística de MeterSmoother (animación a 125 Hz, ataque de 30 ms / liberación de 180 ms) hace que el relleno se lea de forma idéntica en todas las superficies de medición. |
| Thresh | perilla | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` | Mapeo lineal. Establece el nivel por encima del cual comienza la compresión. La etiqueta tiene el formato "-18.0 dB". |
| Ratio | perilla | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` | Mapeo logarítmico (1 * 20^n). Establece la intensidad con la que se contienen los picos una vez superado el umbral. La etiqueta tiene el formato "X.XX:1". |
| Attack | perilla | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | Mapeo exponencial (0.1 * 3000^n). Establece la rapidez con la que el compresor reduce la ganancia después de superar el umbral. La etiqueta tiene el formato "X.X ms" por debajo de 10, "X ms" por encima. |
| Release | perilla | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | Mapeo exponencial (5 * 400^n). Establece la rapidez con la que la ganancia regresa después de que la entrada vuelve a estar por debajo del umbral. La etiqueta tiene el formato "X ms". |
| Makeup | perilla | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` | Mapeo lineal. Añade ganancia para compensar la pérdida por compresión. La etiqueta muestra un signo "+" explícito para valores positivos. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Bola de envolvente | en reposo en la línea de umbral, moviéndose a lo largo de la curva | Nivel de entrada en vivo trazado contra la curva de transferencia estática. |
| Franja de reducción de ganancia | vacía, relleno ámbar, marca de -6 dB | Cantidad de atenuación dinámica aplicada actualmente por el compresor. |

## Impulse el compresor con más fuerza usando ganancia de precompresión para la reducción de PAPR (compensación automática vinculada)

Use la perilla Drive para enviar más señal al compresor antes del umbral y luego recupere automáticamente esa ganancia a la salida. Esto le permite operar el compresor con más intensidad — aumentando la reducción de la relación pico a potencia promedio (PAPR) — mientras mantiene su nivel RMS promedio sin cambios, para no tener que reajustar la perilla Makeup.

### Antes de comenzar

- Confirme que el compresor TX esté habilitado (haga clic en el mosaico del compresor en el widget CHAIN para que se muestre como activo, no atenuado).
- Abra el StripCompPanel flotante haciendo doble clic en el mosaico COMP en el lado TX del widget CHAIN.

### Pasos

1. Localice la perilla Drive en la columna derecha del StripCompPanel flotante (etiquetada como `+X.X dB`).
2. Gire Drive en el sentido de las agujas del reloj desde su valor predeterminado `0.0 dB` (rango: `0.0` a `18.0 dB`). Cada dB de Drive empuja más señal por encima del umbral, por lo que el compresor actúa con más fuerza sobre los picos.
3. Opcionalmente, combine Drive con la perilla Phase Rotator (también en la columna derecha).

El medidor de reducción de ganancia del compresor y la bola animada en la curva de transferencia mostrarán más actividad a medida que aumente Drive. La compensación automática garantiza que su nivel de salida no disminuya a medida que aumenta la compresión, por lo que su perilla Makeup permanece como un ajuste limpio posterior a todo.

## Controles en el StripCompPanel flotante (haga doble clic en el mosaico COMP)

| Control | Tipo | Valor predeterminado | Rango válido | Clave de ajuste | Comportamiento |
|---------|------|----------------------|--------------|-----------------|----------------|
| Drive | perilla | 0.0 dB | 0.0 a 18.0 dB | `ClientCompTxDriveDb` | Aumento de ganancia de precompresión con compensación automática vinculada. Empuja más señal a través del umbral para que el compresor actúe con más fuerza y, simultáneamente, añade la misma ganancia a la salida para que el RMS promedio suba junto con los picos en lugar de caer. La etiqueta se muestra como "+X.X dB". La información sobre herramientas explica el emparejamiento para la reducción de PAPR #2887. La compensación automática sigue el modelo broadcast-Optimod: Drive empuja más material hacia la curva Y añade la misma ganancia de vuelta, por lo que el Makeup fijo del usuario permanece como una perilla de ajuste limpio posterior a todo. |
| Phase | perilla | 0 etapas | 0 a 6 etapas | `ClientCompTxPhaseRotatorStages` | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase a frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos de voz asimétricos antes de la compresión para reducir la PAPR. La etiqueta muestra "Off" cuando es 0, "N stg" cuando está activo. Información sobre herramientas: "Rotador de fase de precompresión (#2887). Cascada de paso total que simetriza los picos de voz asimétricos antes de la compresión. 0 = desactivado, 4 = valor predeterminado de transmisión". Los centros predeterminados (300/700/1500/2500 Hz con 1000/2000 Hz opcionales) cubren el rango de formantes del habla sin agruparse. |

## Qué hace cada control

| Control | Valor predeterminado | Rango válido |
|---------|----------------------|--------------|
| Drive | `0.0 dB` | `0.0` a `18.0 dB` |
| Phase | `0 etapas` | `0` a `6 etapas` |
| Thresh | `-18.0 dB` | `-60.0` a `0.0 dB` |
| Ratio | `3.0` | `1.0` a `20.0` |
| Attack | `20.0 ms` | `0.1` a `300.0 ms` |
| Release | `200 ms` | `5` a `2000 ms` |
| Makeup | `0.0 dB` | `-12.0` a `24.0 dB` |

## Consejos

- Drive está diseñado para usarse *antes* de tocar Makeup. Con la compensación automática activa, puede aumentar Drive para obtener una compresión más intensa sin perder nivel promedio.
- La configuración predeterminada de transmisión del Phase Rotator es 4 etapas. Comience allí y escuche si obtiene picos más limpios y simétricos.
- La perilla Drive solo está disponible en el StripCompPanel flotante; no aparece en el mosaico compacto del applet.

## Relacionado

- [Abra el editor completo del compresor para los controles Knee, Limiter, Drive y Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Rote la simetría de fase de la voz con el rotador de fase (0–6 etapas a frecuencias escalonadas)](rotate-voice-phase-symmetry-with-the-phase-rotator-0-6-stages-at-staggered-frequencies.md)
- [Ajuste el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Aplique ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
