# Descripción general del compresor

El compresor de TX del lado del cliente en AetherSDR reduce el rango dinámico del audio transmitido antes de que llegue al radio. Úselo para controlar los picos de voz, mantener una potencia promedio constante y reducir la posibilidad de salpicadura en SSB.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado) mediante el widget CHAIN o el editor flotante antes de que el tile del applet COMPRESSOR sea visible.
- No se requiere conexión con el radio para ajustar la configuración del compresor.

## Cómo funciona

El compresor se ejecuta completamente en el lado del cliente: procesa el audio en AetherSDR antes de que la señal se envíe al FLEX-8600. Aplica un modelo estándar de reducción de ganancia: cuando el nivel de entrada supera el umbral, el compresor atenúa la señal según la relación configurada. Los tiempos de ataque y de recuperación controlan la rapidez con que el compresor actúa y se recupera. La ganancia de compensación (makeup gain) permite restaurar el nivel promedio perdido por la compresión.

El tile del applet **COMPRESSOR** se encuentra dentro del contenedor principal PooDoo Audio (TXDSP). Muestra una curva de transferencia con un indicador de envolvente en tiempo real y un medidor horizontal de reducción de ganancia para observar la compresión mientras se transmite.

Para acceder a los controles de rodilla y limitador (`ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`), abra el editor flotante haciendo doble clic en la etapa Comp del widget CHAIN.

## Qué hace cada control

| Control | Descripción | Valor predeterminado | Rango | Clave de configuración |
|---|---|---|---|---|
| Curva de transferencia | Dibuja la curva de transferencia estática de entrada/salida. Una bola en movimiento recorre la curva para mostrar el nivel de envolvente actual. Solo lectura en el applet; editable en el editor flotante. | — | — | — |
| Barra de reducción de ganancia | Franja ámbar horizontal, rellena desde la derecha. Muestra cuánta atenuación se aplica en el momento. Una marca señala el punto de −6 dB como referencia de trabajo típica. La escala llega hasta 20 dB de reducción. | — | 0–20 dB GR | — |
| Thresh | Nivel a partir del cual comienza la compresión. | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | Agresividad con que se controlan los picos una vez superado el umbral. Se muestra como X.XX:1. | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | Rapidez con que el compresor actúa después de que la entrada supera el umbral. | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | Rapidez con que la ganancia se recupera después de que la entrada cae por debajo del umbral. | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | Agrega la ganancia perdida por la compresión. Los valores positivos se muestran con signo `+` explícito. | 0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

Las siguientes configuraciones están disponibles únicamente en el editor flotante:

| Clave de configuración | Propósito |
|---|---|
| `ClientCompTxEnabled` | Habilita o desactiva (bypass) la etapa del compresor. |
| `ClientCompTxKneeDb` | Suaviza la transición hacia la compresión alrededor del umbral. |
| `ClientCompTxLimEnabled` | Habilita el limitador de salida. |
| `ClientCompTxLimCeilingDb` | Establece el techo máximo que aplica el limitador. |

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz. Obsérvela mientras habla para evaluar si la configuración es adecuada antes de transmitir en el aire.
- La marca de −6 dB en la barra de reducción de ganancia es una referencia útil: una reducción constante en esa zona generalmente produce una compresión de sonido natural en voz SSB.
- Los cinco controles del tile del applet son suficientes para la mayoría de los ajustes. Abra el editor flotante solo cuando necesite ajustar la rodilla o habilitar el limitador.
- Haga clic derecho en la barra de título del subcontenedor COMPRESSOR para flotarlo, desplegarlo o ocultarlo.

## Temas relacionados

- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar el ataque y la recuperación para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación tras la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Desactivar el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
