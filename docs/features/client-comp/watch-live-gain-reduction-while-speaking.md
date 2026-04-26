# Ver la reducción de ganancia en tiempo real mientras habla

El applet COMPRESSOR muestra una barra horizontal de reducción de ganancia y una bola de envolvente en vivo sobre la curva de transferencia, para que pueda ver con exactitud cuánto está trabajando el compresor mientras transmite. Use estos indicadores para confirmar que sus ajustes producen la cantidad de compresión deseada, sin tener que adivinar solo por el audio.

## Antes de comenzar

- El applet COMPRESSOR debe estar visible. Aparece dentro del contenedor padre PooDoo Audio (TXDSP) únicamente cuando la etapa Compressor está habilitada (no bypassed) mediante el widget CHAIN.
- Debe haber un motor de audio conectado; el medidor no se anima sin una ruta de audio activa.

## Pasos

1. Localice el subcontenedor COMPRESSOR dentro del panel PooDoo Audio (TXDSP).
2. Hable al micrófono a un nivel de voz normal.
3. Observe la **barra de reducción de ganancia** — la franja ámbar directamente debajo de la curva de transferencia. Se llena desde la derecha a medida que el compresor reduce la ganancia. Una marca en la posición −6 dB sirve de referencia para una cantidad de trabajo típica.
4. Observe la **curva de transferencia** para localizar la bola de envolvente. La bola se desplaza sobre la curva estática para mostrar su nivel de entrada actual en relación con el umbral.
5. Ajuste los controles **Thresh** o **Ratio** hasta que la barra de reducción de ganancia se estabilice en un rango adecuado para su estilo de operación. La barra se actualiza aproximadamente 30 veces por segundo con balística suavizada.

## Qué hace cada control

| Control | Tipo | Valor por defecto | Rango válido | Clave persistida |
|---|---|---|---|---|
| Transfer curve | Indicador | — | — | — |
| Gain-reduction bar | Medidor | — | 0 a 20 dB GR | — |
| Thresh | Mando | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | Mando | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | Mando | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | Mando | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | Mando | +0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

**Transfer curve** — Solo lectura en el applet. Dibuja la curva estática de entrada/salida. La bola de envolvente se desplaza sobre la curva según su nivel de entrada actual.

**Gain-reduction bar** — Franja horizontal ámbar, rellena desde la derecha. Vacía significa que no hay compresión activa. El relleno crece hacia la izquierda a medida que aumenta la reducción de ganancia. La escala llega hasta 20 dB; la marca señala el punto −6 dB.

**Thresh** — Nivel a partir del cual comienza la compresión. Valores más bajos activan el compresor antes. Se muestra como un valor en dB (por ejemplo, `−18.0 dB`).

**Ratio** — Qué tan agresivamente se controlan los picos una vez que se supera el umbral. Se muestra como `X.XX:1`. Ratios más altos producen un carácter más duro, más limitante.

**Attack** — Qué tan rápido actúa el compresor después de que la entrada supera el umbral. Se muestra como `X.X ms` por debajo de 10 ms, `X ms` por encima.

**Release** — Qué tan rápido se recupera la ganancia después de que la entrada cae por debajo del umbral. Se muestra en ms.

**Makeup** — Ganancia añadida tras la compresión para recuperar el volumen perdido. Se muestra con un signo `+` explícito para valores positivos.

## Consejos

- La marca de la barra de reducción de ganancia en −6 dB es un punto de referencia práctico. Para la mayoría de la operación de voz, mantener el relleno promedio cerca de esa marca o por debajo produce una compresión de sonido natural.
- Si la barra permanece fija en 20 dB de forma continua, el umbral es demasiado bajo o el ratio es demasiado alto para su nivel de micrófono. Suba **Thresh** o baje **Ratio** hasta que la barra respire con su voz.
- La bola de envolvente sobre la curva de transferencia muestra si está operando en la región lineal, de rodilla o de compresión de la curva — útil al ajustar finamente los parámetros de rodilla en el editor completo.
- Los controles de rodilla y limitador (`ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) no son accesibles desde los mandos del applet. Abra el editor completo para acceder a ellos.

## Solución de problemas

- **La barra de reducción de ganancia no muestra nada mientras habla** — Es posible que la etapa Compressor esté en bypass. Verifique el widget CHAIN y asegúrese de que la etapa Compressor esté habilitada. Si la etapa está en bypass, el applet se oculta y el medidor no funciona.
- **La bola sobre la curva de transferencia no se mueve** — El motor de audio no está recibiendo señal del micrófono. Verifique que su dispositivo de entrada de audio esté seleccionado y que la ruta de audio TX esté activa.

## Relacionados

- [Descripción general del Compressor](overview.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer el ratio de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar ataque y release para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Abrir el editor completo del Compressor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Poner el compresor en bypass desde la cadena](bypass-the-compressor-from-the-chain.md)
