# Ver la reducción de ganancia en tiempo real mientras habla

El applet COMPRESSOR muestra una barra horizontal de reducción de ganancia y una bola de envolvente animada sobre la curva de transferencia, para que pueda ver exactamente cuánto está trabajando el compresor mientras transmite. Use estos indicadores para confirmar que sus ajustes producen la cantidad de compresión deseada, sin tener que adivinarla solo por el audio.

## Antes de comenzar

- El applet COMPRESSOR debe estar visible. Aparece dentro del contenedor padre PooDoo Audio (TXDSP) únicamente cuando la etapa Compressor está habilitada (no omitida) mediante el widget CHAIN.
- Debe haber un motor de audio conectado; el medidor no se anima sin una ruta de audio activa.

## Pasos

1. Localice el subcontenedor COMPRESSOR dentro del panel PooDoo Audio (TXDSP).
2. Hable al micrófono a un nivel de voz normal.
3. Observe la **barra de reducción de ganancia** — la franja ámbar directamente debajo de la curva de transferencia. Se llena desde la derecha a medida que el compresor reduce la ganancia. Una marca en la posición −6 dB sirve como referencia para una cantidad de trabajo típica.
4. Observe la **curva de transferencia** para localizar la bola de envolvente. La bola se desplaza a lo largo de la curva estática para mostrar su nivel de entrada actual en relación con el umbral.
5. Ajuste los controles **Thresh** o **Ratio** hasta que la barra de reducción de ganancia se estabilice en un rango que se adapte a su estilo de operación. La barra se actualiza aproximadamente 30 veces por segundo con balística suavizada.

## Qué hace cada control

| Control | Tipo | Valor predeterminado | Rango válido | Clave persistente |
|---|---|---|---|---|
| Transfer curve | Indicador | — | — | — |
| Gain-reduction bar | Medidor | — | 0 a 20 dB GR | — |
| Thresh | Perilla | −18.0 dB | −60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | Perilla | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Attack | Perilla | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | Perilla | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Makeup | Perilla | +0.0 dB | −12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

**Transfer curve** — Solo lectura en el applet. Dibuja la curva estática de entrada/salida. La bola de envolvente se desplaza sobre la curva según su nivel de entrada actual.

**Gain-reduction bar** — Franja ámbar horizontal, rellena desde la derecha. Vacía significa que no hay compresión activa. El relleno crece hacia la izquierda a medida que aumenta la reducción de ganancia. La escala llega hasta 20 dB; la marca señala el punto −6 dB.

**Thresh** — Nivel a partir del cual comienza la compresión. Valores más bajos activan el compresor antes. Se muestra como un valor en dB (por ejemplo, `−18.0 dB`).

**Ratio** — Qué tan agresivamente se controlan los picos una vez superado el umbral. Se muestra como `X.XX:1`. Relaciones más altas producen un carácter más duro, más cercano a la limitación.

**Attack** — Qué tan rápidamente actúa el compresor después de que la entrada supera el umbral. Se muestra como `X.X ms` por debajo de 10 ms, y como `X ms` por encima.

**Release** — Qué tan rápidamente se recupera la ganancia después de que la entrada cae por debajo del umbral. Se muestra en ms.

**Makeup** — Ganancia añadida después de la compresión para recuperar el nivel de volumen perdido. Se muestra con un signo `+` explícito para valores positivos.

## Consejos

- La marca de la barra de reducción de ganancia en −6 dB es un punto de referencia práctico. Para la mayoría de las operaciones de voz, mantener el relleno promedio cerca o por debajo de esa marca produce una compresión de sonido natural.
- Si la barra permanece fijada en 20 dB de forma continua, el umbral es demasiado bajo o la relación es demasiado alta para el nivel de su micrófono. Suba **Thresh** o baje **Ratio** hasta que la barra respire con su voz.
- La bola de envolvente sobre la curva de transferencia muestra si está operando en la región lineal, de rodilla o comprimida de la curva — útil al ajustar con precisión los parámetros de rodilla en el editor completo.
- Los controles de rodilla y limitador (`ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) no son accesibles desde las perillas del applet. Abra el editor completo para acceder a ellos.

## Solución de problemas

- **La barra de reducción de ganancia no muestra nada mientras habla** — Es posible que la etapa Compressor esté omitida. Verifique el widget CHAIN y asegúrese de que la etapa Compressor esté habilitada. Si la etapa está omitida, el applet se oculta y el medidor no funciona.
- **La bola sobre la curva de transferencia no se mueve** — El motor de audio no está recibiendo entrada del micrófono. Verifique que su dispositivo de entrada de audio esté seleccionado y que la ruta de audio TX esté activa.

## Relacionados

- [Descripción general del compresor](overview.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Ajustar attack y release para una compresión de sonido natural](tune-attack-release-for-a-natural-sounding-squeeze.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
- [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md)
