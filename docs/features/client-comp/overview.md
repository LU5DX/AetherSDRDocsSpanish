# Descripción general del compresor

El compresor del lado del cliente es un procesador de rango dinámico de TX integrado en la cadena de audio de AetherSDR. Reduce los niveles de pico antes de la transmisión, lo que permite aumentar la potencia promedio sin distorsionar la señal.

## Antes de comenzar

- El panel COMPRESSOR forma parte de la cadena de procesamiento PooDoo Audio (TXDSP). Permanece oculto hasta que la etapa Compressor esté habilitada — desactívela mediante el widget CHAIN o el editor flotante para que el panel sea visible.
- No se requiere conexión a la radio para configurar el compresor.

## Cómo funciona

El compresor monitorea en tiempo real el nivel del audio de TX. Cuando la señal supera el umbral definido, el compresor reduce la ganancia según la relación especificada. Los tiempos de ataque y liberación controlan la rapidez con que el compresor actúa y deja de actuar. La ganancia de compensación recupera el nivel general perdido por la compresión.

El applet COMPRESSOR ofrece una vista compacta de todo esto a la vez:

- La **curva de transferencia** muestra la relación estática de ganancia entrada/salida como una curva. Una bola en movimiento recorre la curva para indicar dónde se encuentra el nivel de envolvente actual. Esta vista es de solo lectura en el applet; la curva es editable en el editor flotante.
- La **barra de reducción de ganancia** es una franja horizontal de color ámbar que se llena desde la derecha. Muestra cuánta atenuación está aplicando el compresor en ese momento, hasta un máximo de 20 dB. Una marca en −6 dB indica una cantidad de reducción de ganancia típica en uso. El medidor se actualiza a aproximadamente 30 Hz con balística suavizada.

Dos controles que afectan si el compresor está activo — habilitar/omitir y la configuración de rodilla y limitador — no se encuentran en el propio applet. La función de omisión se controla desde el widget CHAIN (un solo clic) o el editor flotante. La configuración de rodilla y limitador solo está disponible en el editor flotante.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Ajuste persistente | Comportamiento |
|---|---|---|---|---|
| Thresh | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` | Define el nivel de entrada a partir del cual comienza la compresión. Valores más bajos comprimen más la señal. |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` | Define la agresividad con que se controlan los picos una vez superado el umbral. Se muestra como X.XX:1. Usa mapeo logarítmico del control. |
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | Define la rapidez con que responde el compresor cuando la señal supera el umbral. Usa mapeo exponencial del control. |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | Define la rapidez con que se recupera la ganancia cuando la señal cae por debajo del umbral. Usa mapeo exponencial del control. |
| Makeup | 0.0 dB | −12.0 a +24.0 dB | `ClientCompTxMakeupDb` | Agrega de vuelta la ganancia perdida por la compresión. Los valores positivos se muestran con signo + explícito. |
| `ClientCompTxEnabled` | — | activado/desactivado | `ClientCompTxEnabled` | Indica si la etapa del compresor está activa u omitida. Se controla desde el widget CHAIN o el editor flotante, no directamente desde el applet. |
| `ClientCompTxKneeDb` | — | — | `ClientCompTxKneeDb` | Ancho de rodilla. Solo accesible en el editor flotante. |
| `ClientCompTxLimEnabled` | — | activado/desactivado | `ClientCompTxLimEnabled` | Habilita el limitador de salida. Solo accesible en el editor flotante. |
| `ClientCompTxLimCeilingDb` | — | — | `ClientCompTxLimCeilingDb` | Nivel de techo del limitador. Solo accesible en el editor flotante. |

## Consejos

- Observe la barra de reducción de ganancia mientras habla a su nivel de voz normal. Trate de mantener el relleno ámbar trabajando principalmente a la izquierda de la marca de −6 dB para obtener un resultado de sonido natural.
- La bola de la curva de transferencia ofrece una comprobación visual rápida de que el umbral está ajustado correctamente — si la bola nunca se mueve de la posición de reposo, es posible que el umbral esté demasiado alto para su nivel de señal.
- La configuración de rodilla y limitador solo está disponible en el editor flotante. Haga doble clic en la etapa Comp del widget CHAIN para abrirlo.

## Temas relacionados

- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Configurar la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar el ataque y la liberación para un sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación tras la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
