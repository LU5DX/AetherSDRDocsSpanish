# Ver la reducción de ganancia en tiempo real mientras habla

El applet Compressor muestra un medidor de reducción de ganancia en tiempo real y un indicador de curva de transferencia en vivo mientras transmite. Use estos elementos para confirmar que el compresor está funcionando y para evaluar con qué intensidad está limitando los picos de su voz.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado). Si el tile COMPRESSOR está oculto, habilite la etapa desde el widget CHAIN o haga doble clic en la etapa Comp del widget CHAIN para abrir el editor flotante y activarla desde allí.
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).
- Un micrófono debe estar enrutado a través de la cadena de audio TX para que haya una señal de entrada en vivo que comprimir.

## Pasos

1. Localice el subcontenedor COMPRESSOR dentro del contenedor principal PooDoo Audio (TXDSP) en el panel de applets.
2. Active la transmisión y hable al micrófono con su nivel de voz normal.
3. Observe la **barra de reducción de ganancia** — la franja horizontal ámbar en la parte superior de la fila de mandos. Cuando el compresor actúa sobre su voz, la barra se llena desde la derecha. Un relleno más amplio indica mayor reducción.
4. Observe la marca de referencia situada a un tercio desde el borde derecho. Esa marca indica −6 dB de reducción de ganancia, un valor de trabajo típico para voz.
5. Observe la pantalla de **curva de transferencia** ubicada encima de la barra. La pequeña bola se desplaza a lo largo de la curva estática de entrada/salida para mostrar el nivel de envolvente actual. Cuando habla más fuerte, la bola se mueve hacia arriba y hacia la derecha; cuando la bola pasa el punto de inflexión (knee), la curva se aplana y la barra de reducción de ganancia crece.
6. Si la barra está consistentemente vacía, su nivel de entrada está por debajo del umbral. Aumente la ganancia del micrófono o baje el mando **Thresh** (valor predeterminado −18.0 dB) hasta que la barra muestre actividad en los picos de voz.
7. Si la barra está pegada al borde derecho, el compresor está aplicando más de 20 dB de reducción. Suba **Thresh** o baje **Ratio** (valor predeterminado 3.0:1) para reducir la cantidad de compresión.

## Qué hace cada control

| Control | Qué muestra o hace | Predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Transfer curve | Curva estática de entrada/salida con una bola en vivo en el nivel de envolvente actual. Solo visualización en el applet. | — | — | — |
| Gain-reduction bar | Franja horizontal ámbar. Se llena desde la derecha para mostrar la reducción de ganancia actual. Vacía = sin reducción. Marca en −6 dB indica un nivel de trabajo típico. Escala máxima de 20 dB. | — | 0–20 dB | — |
| Thresh | Nivel a partir del cual comienza la compresión. | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | Intensidad con la que se controlan los picos una vez superado el umbral. | 3.0:1 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | Rapidez con la que el compresor actúa tras superar el umbral. | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | Rapidez con la que la ganancia se recupera cuando la entrada cae por debajo del umbral. | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | Ganancia añadida tras la compresión. | +0.0 dB | −12.0 a +24.0 dB | `ClientCompTxMakeupDb` |

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz con balística suavizada, por lo que los transitorios breves pueden no mostrar su pico completo; utilice la bola en la curva de transferencia como verificación secundaria del movimiento de la envolvente.
- Una reducción constante de 3–6 dB (barra que alcanza aproximadamente la marca o la toca levemente) es un punto de partida razonable para la compresión de voz sin procesamiento excesivo.
- Los controles de knee y techo del limitador (`ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) no están disponibles en el applet. Abra el editor completo para ajustarlos.

## Solución de problemas

- **La barra de reducción de ganancia permanece vacía durante la transmisión** — El nivel de entrada no está alcanzando el umbral. Baje el mando **Thresh** o aumente la ganancia del micrófono hasta que la barra comience a moverse en los picos de voz.
- **La barra de reducción de ganancia siempre está llena (pegada al máximo)** — El umbral está demasiado bajo o el ratio demasiado alto para el nivel de su micrófono. Suba **Thresh** hacia 0 dB o reduzca **Ratio** hacia 1.0:1.
- **El tile COMPRESSOR no es visible** — La etapa Compressor está en bypass o deshabilitada. Habilítela desde el widget CHAIN. Consulte [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).

## Relacionados

- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer el ratio de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar attack y release para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación (make-up gain) tras la compresión](apply-make-up-gain-after-compression.md)
- [Abrir el editor completo del Compressor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
