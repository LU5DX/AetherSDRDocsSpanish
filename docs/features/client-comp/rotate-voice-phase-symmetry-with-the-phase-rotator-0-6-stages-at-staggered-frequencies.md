# Visión general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)

El Compresor Aetherial (TX) y el AGC-C Aetherial (RX) son procesadores de rango dinámico del lado del cliente. El applet crea una copia para TX ("Compresor Aetherial") y una para RX ("AGC-C Aetherial") con estado completamente independiente.

## Vista del applet

El applet muestra:
- Una curva de transferencia estática con una "bola" en vivo que se desplaza sobre la envolvente actual
- Un medidor horizontal de reducción de ganancia (20 dB máx.)
- Cinco perillas de ajuste: Thresh, Ratio, Attack, Release, Makeup

## Controles

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Curva de transferencia | — | — | ClientCompCurveWidget en modo compacto. Dibuja la curva de transferencia entrada/salida más una bola en vivo que muestra el nivel de envolvente actual. Solo vista en el applet; editable en el ClientCompEditor flotante. |
| Barra de reducción de ganancia | — | 0 a 20 dB GR | Franja horizontal ámbar, relleno desde la derecha. La escala llega a 20 dB de reducción; una marca en -6 dB señala un valor de trabajo típico. Se muestrea a ~30 Hz desde ClientComp::gainReductionDb(); las características balísticas de MeterSmoother (animación a 125 Hz, ataque de 30 ms / liberación de 180 ms) hacen que el relleno se lea de forma idéntica en todas las superficies de medición. |
| Thresh | -18.0 dB | -60.0 a 0.0 dB | Mapeo lineal. Define el nivel a partir del cual comienza la compresión. La etiqueta se muestra como '-18.0 dB'. Clave de configuración: `ClientCompTxThresholdDb`. |
| Ratio | 3.0 | 1.0 a 20.0 | Mapeo logarítmico (1 * 20^n). Define qué tanto se limitan los picos una vez superado el umbral. La etiqueta se muestra como 'X.XX:1'. Clave de configuración: `ClientCompTxRatio`. |
| Attack | 20.0 ms | 0.1 a 300.0 ms | Mapeo exponencial (0.1 * 3000^n). Define la rapidez con que el compresor actúa tras superar el umbral. La etiqueta se muestra como 'X.X ms' por debajo de 10, 'X ms' por encima. Clave de configuración: `ClientCompTxAttackMs`. |
| Release | 200 ms | 5 a 2000 ms | Mapeo exponencial (5 * 400^n). Define qué tan rápido regresa la ganancia tras volver la entrada por debajo del umbral. La etiqueta se muestra como 'X ms'. Clave de configuración: `ClientCompTxReleaseMs`. |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | Mapeo lineal. Agrega ganancia para compensar la pérdida por compresión. La etiqueta muestra un signo '+' explícito para valores positivos. Clave de configuración: `ClientCompTxMakeupDb`. |
| Drive | 0.0 dB | 0.0 a 18.0 dB | Aumento de ganancia previo a la compresión con auto-makeup vinculado. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza, y simultáneamente agrega la misma ganancia a la salida, elevando el RMS promedio junto con los picos en lugar de reducirlo. Combínelo con Phase para mantener los picos limpios. Se muestra solo en el StripCompPanel flotante (columna derecha). La etiqueta se muestra como '+X.X dB'. Clave de configuración: `ClientCompTxDriveDb`. El auto-makeup sigue el modelo broadcast-Optimod: Drive introduce más material en la curva Y agrega la misma ganancia de vuelta, de modo que el Makeup fijo del usuario sigue siendo una perilla de ajuste final limpia. |
| Phase | 0 etapas | 0 a 6 etapas | Número de secciones pasa-todo en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de voz antes de la compresión para reducir el PAPR. Se muestra solo en el StripCompPanel flotante (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Clave de configuración: `ClientCompTxPhaseRotatorStages`. Los centros predeterminados (300/700/1500/2500 Hz con 1000/2000 Hz opcionales) cubren el rango de formantes del habla sin agruparse. |

## Indicadores

| Indicador | Estados | Significado |
|-----------|---------|-------------|
| Bola de envolvente | en reposo sobre la línea de umbral, desplazándose por la curva | Nivel de entrada en vivo representado sobre la curva de transferencia estática. |
| Franja de reducción de ganancia | vacía, relleno ámbar, marca de -6 dB | Cantidad de atenuación dinámica aplicada actualmente por el compresor. |

## Comportamiento del medidor de reducción de ganancia

El medidor de reducción de ganancia utiliza características balísticas de MeterSmoother para una respuesta visual natural. El medidor se actualiza aproximadamente a 30 Hz y proporciona retroalimentación visual continua durante la compresión activa.

## Relacionados

- [Abra el editor completo del compresor para knee, limiter, Drive y controles de Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)

---

# Abra el editor completo del compresor para knee, limiter, Drive y controles de Phase

El StripCompPanel flotante amplía los controles del applet con parámetros adicionales para ajustar finamente el compresor.

## Antes de comenzar

- El compresor debe estar habilitado en el lado TX (Compresor Aetherial) o en el lado RX (AGC-C Aetherial).

## Pasos

1. Abra el widget de CHAIN en el lado deseado (TX o RX).
2. Haga doble clic en el mosaico **COMP** en el widget de CHAIN.
3. Aparece el StripCompPanel flotante.

## Controles en el StripCompPanel flotante

El StripCompPanel agrega los siguientes controles en la columna derecha:

| Control | Valor predeterminado | Rango válido | Comportamiento |
|---------|---------------------|--------------|----------------|
| Knee | — | — | Define la suavidad de la transición alrededor del umbral. |
| Ceiling | — | — | Define el nivel máximo de salida. |
| Makeup | — | — | Ajuste de ganancia posterior a la compresión. |
| Limiter | Desactivado | Activar/Desactivar | Activa un limitador duro después de la compresión. |
| Drive | 0.0 dB | 0.0 a 18.0 dB | Aumento de ganancia previo a la compresión con auto-makeup vinculado. Empuja más señal por encima del umbral para que el compresor actúe con más fuerza, y simultáneamente agrega la misma ganancia a la salida, elevando el RMS promedio junto con los picos en lugar de reducirlo. Combínelo con Phase para mantener los picos limpios. La etiqueta se muestra como "+X.X dB". Clave de configuración: `ClientCompTxDriveDb`. |
| Phase | 0 etapas | 0 a 6 etapas | Número de secciones pasa-todo en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de voz antes de la compresión para reducir el PAPR. Etiqueta "Off" cuando es 0, "N stg" cuando está activo. Clave de configuración: `ClientCompTxPhaseRotatorStages`. |

## Combinación de Drive y Phase

Las perillas Drive y Phase trabajan juntas para una reducción óptima de la relación pico-promedio (PAPR):

- **Drive** empuja más señal al compresor mientras agrega la misma ganancia a la salida. Esto eleva el RMS promedio junto con los picos.
- **Phase** simetriza los picos asimétricos de voz antes de la compresión, evitando que el compresor reaccione de forma exagerada a la asimetría de la forma de onda.
- Comience con 4 etapas de rotación de fase (predeterminado de radiodifusión) y ajuste Drive hacia arriba mientras monitorea el medidor de reducción de ganancia.

## Relacionados

- [Visión general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)

---

# Accione el compresor con más fuerza usando ganancia previa a la compresión para reducir el PAPR (auto-makeup vinculado)

La perilla **Drive** (0–18 dB) agrega un aumento de ganancia previo a la compresión con ganancia de auto-makeup vinculada. Esto empuja más señal por encima del umbral mientras simultáneamente agrega la misma ganancia a la salida, elevando el RMS promedio junto con los picos en lugar de reducirlos.

## Antes de comenzar

- El compresor debe estar habilitado en el lado TX (Compresor Aetherial).
- Debe tener abierto el StripCompPanel flotante. Haga doble clic en el mosaico **COMP** en el widget de CHAIN en el lado TX.

## Pasos

1. Abra el StripCompPanel flotante haciendo doble clic en el mosaico **COMP** en el widget de CHAIN en el lado TX.
2. Localice la perilla **Drive** en la columna derecha del StripCompPanel.
3. Gire la perilla **Drive** en el sentido de las agujas del reloj para aumentar la ganancia previa a la compresión (0.0 a 18.0 dB).
4. Observe el medidor de reducción de ganancia: valores más altos de Drive harán que el compresor actúe de forma más agresiva.
5. Ajuste el rotador **Phase** según sea necesario para mantener los picos simétricos (consulte el tema relacionado).

## Cómo funciona el auto-makeup

El auto-makeup sigue el modelo broadcast-Optimod:

- **Drive** introduce más material en la curva de compresión.
- Se agrega automáticamente la misma ganancia a la salida.
- La perilla fija **Makeup** sigue siendo un control de ajuste final limpio.

Esto significa que puede aumentar Drive para que el compresor actúe con más fuerza sin perder nivel promedio.

## Consejos

- Comience con el rotador **Phase** en 4 etapas (predeterminado de radiodifusión) antes de ajustar Drive.
- Aumente Drive gradualmente mientras monitorea la calidad del audio transmitido.
- Reajuste la perilla **Thresh** si el compresor actúa de forma demasiado agresiva.

## Relacionados

- Rote la simetría de fase de la voz con el rotador Phase (0–6 etapas en frecuencias escalonadas)
- [Abra el editor completo del compresor para knee, limiter, Drive y controles de Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)

---

# Rote la simetría de fase de la voz con el rotador Phase (0–6 etapas en frecuencias escalonadas)

El rotador Phase encadena secciones de filtro pasa-todo para simetrizar los picos asimétricos de voz antes de la compresión, reduciendo la relación pico-promedio (PAPR). Esto le permite usar más potencia promedio sin recortar o distorsionar.

## Antes de comenzar

- El compresor debe estar habilitado en el lado TX (Compresor Aetherial).
- Debe tener abierto el StripCompPanel flotante. Haga doble clic en el mosaico **COMP** en el widget de CHAIN en el lado TX.

## Pasos

1. Abra el StripCompPanel flotante haciendo doble clic en el mosaico **COMP** en el widget de CHAIN en el lado TX.
2. Localice la perilla **Phase** en la columna derecha del StripCompPanel.
3. Gire la perilla **Phase** al número deseado de etapas (0–6):
   - **0** — desactivado (sin rotación de fase).
   - **4** — predeterminado de radiodifusión, punto de partida recomendado.
   - **1–6** — número de etapas pasa-todo en cascada en frecuencias escalonadas.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido |
|---------|---------------------|--------------|
| Perilla Phase | 0 etapas | 0–6 etapas |

## Frecuencias y comportamiento

Cada etapa añade 12 dB/oct de rotación de fase en frecuencias escalonadas:
- Centros principales: 300/700/1500/2500 Hz
- Opcionales: 1000/2000 Hz

Estas frecuencias cubren el rango de formantes del habla sin agruparse. La cascada simetriza los picos asimétricos de voz antes de la compresión para reducir el PAPR.

- La etiqueta muestra "Off" cuando es 0, "N stg" cuando está activo.
- Tooltip: "Rotador de fase previo a la compresión (#2887). Cascada pasa-todo que simetriza los picos asimétricos de voz antes de la compresión. 0 = desactivado, 4 = predeterminado de radiodifusión."

## Consejos

- Comience con **4 etapas** (el valor predeterminado de la industria de radiodifusión) y escuche mientras habla. Aumente las etapas si su forma de onda de voz aún muestra picos asimétricos en la bola de envolvente de la curva de transferencia.
- El rotador Phase funciona antes de la compresión, por lo que los cambios afectan cómo responde el compresor. Reajuste Threshold y Drive después de cambiar el número de etapas.
- Combine el rotador Phase con la perilla **Drive** (0–18 dB con ganancia de auto-makeup) para una reducción máxima del PAPR. Drive empuja más señal al compresor, y la rotación de fase mantiene los picos simétricos para que el compresor no reaccione de forma exagerada a la asimetría de la forma de onda.

## Relacionados

- [Accione el compresor con más fuerza usando ganancia previa a la compresión para reducir el PAPR (auto-makeup vinculado)](drive-the-compressor-harder-with-pre-comp-gain-for-papr-reduction-auto-makeup-linked.md)
- [Abra el editor completo del compresor para knee, limiter, Drive y controles de Phase](open-the-full-compressor-editor-for-knee-limiter-drive-and-phase-controls.md)
- [Visión general del Compresor Aetherial (TX) / AGC-C Aetherial (RX)](overview.md)
