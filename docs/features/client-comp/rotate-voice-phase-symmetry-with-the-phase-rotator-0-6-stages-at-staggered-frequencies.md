# Resumen del Compresor Aetherial (TX) / AGC-C Aetherial (RX)

El Compresor Aetherial (TX) y el AGC-C Aetherial (RX) son procesadores de rango dinámico del lado del cliente. El applet instancia una copia vinculada a TX ("Compresor Aetherial") y una copia vinculada a RX ("AGC-C Aetherial") con un estado completamente independiente.

## Vista del applet

El applet muestra:
- Una curva de transferencia estática con una "bola" en vivo que se desplaza sobre la envolvente actual
- Un medidor horizontal de reducción de ganancia (máx. 20 dB)
- Cinco perillas de ajuste: Thresh, Ratio, Attack, Release, Makeup

## Controles

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Curva de transferencia | — | — | ClientCompCurveWidget en modo compacto. Dibuja la curva de transferencia de entrada/salida más una bola en vivo que muestra el nivel de envolvente actual. Solo visualización en el applet; editable en el ClientCompEditor flotante. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | Barra ámbar horizontal, relleno desde la derecha. La escala alcanza un máximo de 20 dB de reducción; una marca en -6 dB señala un valor de trabajo típico. Se actualiza a ~30 Hz desde `ClientComp::gainReductionDb()` con la balística de MeterSmoother. |
| Thresh | -18,0 dB | -60,0 a 0,0 dB | Mapeo lineal. Establece el nivel por encima del cual comienza la compresión. La etiqueta se formatea como "-18.0 dB". Clave de configuración: `ClientCompTxThresholdDb`. |
| Ratio | 3,0 | 1,0 a 20,0 | Mapeo logarítmico (1 * 20^n). Establece la intensidad con la que se contienen los picos una vez superado el umbral. La etiqueta se formatea como "X.XX:1". Clave de configuración: `ClientCompTxRatio`. |
| Attack | 20,0 ms | 0,1 a 300,0 ms | Mapeo exponencial (0,1 * 3000^n). Establece la rapidez con la que el compresor se activa después de superar el umbral. Etiqueta formateada "X.X ms" por debajo de 10, "X ms" por encima. Clave de configuración: `ClientCompTxAttackMs`. |
| Release | 200 ms | 5 a 2000 ms | Mapeo exponencial (5 * 400^n). Establece la rapidez con la que la ganancia regresa después de que la entrada vuelve a estar por debajo del umbral. Etiqueta formateada "X ms". Clave de configuración: `ClientCompTxReleaseMs`. |
| Makeup | 0,0 dB | -12,0 a 24,0 dB | Mapeo lineal. Añade ganancia para compensar la pérdida por compresión. La etiqueta muestra un signo "+" explícito para valores positivos. Clave de configuración: `ClientCompTxMakeupDb`. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Bola de envolvente | reposando en la línea de umbral, moviéndose a lo largo de la curva | Nivel de entrada en vivo trazado contra la curva de transferencia estática. |
| Barra de reducción de ganancia | vacía, relleno ámbar, marca de -6 dB | Cantidad de atenuación dinámica aplicada actualmente por el compresor. |

## Comportamiento del medidor de reducción de ganancia

El medidor de reducción de ganancia utiliza la balística de MeterSmoother para una respuesta visual natural. El medidor se actualiza aproximadamente a 30 Hz y deja de repintarse cuando la señal se estabiliza. Esto reduce el uso de la CPU mientras mantiene una retroalimentación visual receptiva durante la compresión activa.

## Relacionado

- [Abra el editor completo del compresor para los controles de Knee, Limiter, Drive y Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)

---

# Abra el editor completo del compresor para los controles de Knee, Limiter, Drive y Phase

El StripCompPanel flotante extiende los controles del applet con parámetros adicionales para el ajuste preciso del compresor.

## Antes de comenzar

- El compresor debe estar habilitado en el lado TX (Compresor Aetherial) o en el lado RX (AGC-C Aetherial).

## Pasos

1. Abra el widget CHAIN en el lado deseado (TX o RX).
2. Haga doble clic en el mosaico **COMP** en el widget CHAIN.
3. Aparece el StripCompPanel flotante.

## Controles en el StripCompPanel flotante

El StripCompPanel agrega los siguientes controles en la columna derecha:

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Knee | — | — | Establece la suavidad de la transición alrededor del umbral. |
| Ceiling | — | — | Establece el nivel máximo de salida. |
| Makeup | — | — | Ajuste de ganancia posterior a la compresión. |
| Limiter | Deshabilitado | Habilitar/Deshabilitar | Habilita un limitador duro después de la compresión. |
| Drive | 0,0 dB | 0,0 a 18,0 dB | Aumento de ganancia previa a la compresión con auto-makeup vinculado. Empuja más señal a través del umbral para que el compresor actúe con más fuerza y, simultáneamente, añade la misma cantidad de ganancia en la salida para que el RMS promedio se eleve junto con los picos en lugar de caer. Combínelo con Phase para mantener los picos limpios. La etiqueta se muestra como "+X.X dB". Clave de configuración: `ClientCompTxDriveDb`. |
| Phase | 0 etapas | 0 a 6 etapas | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos de voz asimétricos antes de la compresión para reducir el PAPR. Etiqueta "Off" cuando es 0, "N stg" cuando está activo. Clave de configuración: `ClientCompTxPhaseRotatorStages`. |

## Combinación de Drive y Phase

Las perillas Drive y Phase trabajan juntas para una reducción óptima de la relación de potencia pico a promedio (PAPR):

- **Drive** empuja más señal al compresor mientras añade la misma ganancia en la salida. Esto eleva el RMS promedio junto con los picos.
- **Phase** simetriza los picos de voz asimétricos antes de la compresión, evitando que el compresor reaccione excesivamente a la asimetría de la forma de onda.
- Comience con 4 etapas de rotación de fase (valor predeterminado de radiodifusión) y ajuste Drive hacia arriba mientras monitorea el medidor de reducción de ganancia.

## Relacionado

- [Resumen del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)

---

# Impulse el compresor con más fuerza con ganancia previa a la compresión para la reducción del PAPR (auto-makeup vinculado)

La perilla **Drive** (0–18 dB) añade un aumento de ganancia previo a la compresión con una ganancia de auto-makeup vinculada. Esto empuja más señal a través del umbral mientras añade simultáneamente la misma cantidad de ganancia en la salida, de modo que el RMS promedio se eleva junto con los picos en lugar de caer.

## Antes de comenzar

- El compresor debe estar habilitado en el lado TX (Compresor Aetherial).
- Necesita tener abierto el StripCompPanel flotante. Haga doble clic en el mosaico **COMP** en el widget CHAIN del lado TX.

## Pasos

1. Abra el StripCompPanel flotante haciendo doble clic en el mosaico **COMP** en el widget CHAIN del lado TX.
2. Localice la perilla **Drive** en la columna derecha del StripCompPanel.
3. Gire la perilla **Drive** en el sentido de las agujas del reloj para aumentar la ganancia previa a la compresión (0,0 a 18,0 dB).
4. Observe el medidor de reducción de ganancia: los valores más altos de Drive harán que el compresor actúe de forma más agresiva.
5. Ajuste el rotador **Phase** según sea necesario para mantener los picos simétricos (consulte el tema relacionado).

## Cómo funciona el auto-makeup

El auto-makeup coincide con el modelo de Optimod de radiodifusión:

- **Drive** introduce más material en la curva de compresión.
- Se añade automáticamente la misma cantidad de ganancia en la salida.
- La perilla fija **Makeup** sigue siendo un control de ajuste limpio posterior a todo.

Esto significa que puede aumentar Drive para que el compresor actúe con más fuerza sin perder el nivel promedio.

## Consejos

- Comience con el rotador **Phase** en 4 etapas (valor predeterminado de radiodifusión) antes de ajustar Drive.
- Aumente Drive gradualmente mientras monitorea la calidad del audio transmitido.
- Reajuste la perilla **Thresh** si el compresor actúa de forma demasiado agresiva.

## Relacionado

- Rote la simetría de fase de la voz con el rotador Phase (0–6 etapas en frecuencias escalonadas)
- [Abra el editor completo del compresor para los controles de Knee, Limiter, Drive y Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)

---

# Rote la simetría de fase de la voz con el rotador Phase (0–6 etapas en frecuencias escalonadas)

El rotador Phase pone en cascada secciones de filtro de paso total para simetrizar los picos de voz asimétricos antes de la compresión, reduciendo la relación de potencia pico a promedio (PAPR). Esto le permite usar más potencia promedio sin recortar ni distorsionar.

## Antes de comenzar

- El compresor debe estar habilitado en el lado TX (Compresor Aetherial).
- Necesita tener abierto el StripCompPanel flotante. Haga doble clic en el mosaico **COMP** en el widget CHAIN del lado TX.

## Pasos

1. Abra el StripCompPanel flotante haciendo doble clic en el mosaico **COMP** en el widget CHAIN del lado TX.
2. Localice la perilla **Phase** en la columna derecha del StripCompPanel.
3. Gire la perilla **Phase** al número deseado de etapas (0–6):
   - **0** — desactivado (sin rotación de fase).
   - **4** — valor predeterminado de radiodifusión, punto de partida recomendado.
   - **1–6** — número de etapas de paso total en cascada en frecuencias escalonadas.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido |
|---------|---------------------|--------------|
| Perilla Phase | 0 etapas | 0–6 etapas |

## Frecuencias y comportamiento

Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas:
- Centros principales: 300/700/1500/2500 Hz
- Opcionales: 1000/2000 Hz

Estas frecuencias cubren el rango de formantes del habla sin agruparse. La cascada simetriza los picos de voz asimétricos antes de la compresión para reducir el PAPR.

- La etiqueta muestra "Off" cuando es 0, "N stg" cuando está activo.
- Información sobre herramientas: "Pre-comp phase rotator (#2887). All-pass cascade that symmetrizes asymmetric voice peaks before compression. 0 = off, 4 = broadcast default."

## Consejos

- Comience con **4 etapas** (el valor predeterminado de la industria de la radiodifusión) y escuche mientras habla. Aumente las etapas si la forma de onda de su voz todavía muestra picos asimétricos en la bola de envolvente de la curva de transferencia.
- El rotador Phase funciona antes de la compresión, por lo que los cambios afectan la forma en que responde el compresor. Reajuste Threshold y Drive después de cambiar el número de etapas.
- Combine el rotador Phase con la perilla **Drive** (0–18 dB con ganancia de auto-makeup) para una reducción máxima del PAPR. Drive empuja más señal al compresor, y la rotación de fase mantiene los picos simétricos para que el compresor no reaccione excesivamente a la asimetría de la forma de onda.

## Relacionado

- [Impulse el compresor con más fuerza con ganancia previa a la compresión para la reducción del PAPR (auto-makeup vinculado)](drive-the-compressor-harder-with-pre-comp-gain-for-papr-reduction-auto-makeup-linked.md)
- [Abra el editor completo del compresor para los controles de Knee, Limiter, Drive y Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Resumen del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
