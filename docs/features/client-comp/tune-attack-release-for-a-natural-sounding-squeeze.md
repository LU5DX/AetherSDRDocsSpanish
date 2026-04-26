# Ajuste del Ataque y la Liberación para una Compresión de Sonido Natural

Ajuste los controles Attack y Release en el applet Compressor para controlar con qué rapidez el compresor responde a los picos de voz y se recupera entre sílabas. Establecer correctamente estos dos valores evita que el compresor produzca bombeo en transitorios rápidos o que reaccione tan lentamente que los picos escapen.

## Antes de comenzar

- La etapa Compressor debe estar habilitada (bypass desactivado). Si el panel COMPRESSOR está oculto, habilite la etapa mediante el widget CHAIN o haga doble clic en la etapa Comp en el widget CHAIN para abrir el editor flotante y habilitarla desde allí. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).
- Necesita una fuente de audio (micrófono) activa para que la barra de reducción de ganancia proporcione retroalimentación en tiempo real mientras ajusta.

## Pasos

1. Localice el subcontenedor COMPRESSOR dentro del contenedor principal PooDoo Audio (TXDSP).
2. Encuentre el control Attack en la fila de cinco controles en la parte inferior del applet.
3. Gire Attack para establecer con qué rapidez el compresor actúa tras superar la señal el umbral. El valor predeterminado es 20.0 ms. Para voz, comience ahí y aumente hacia 50–80 ms si las consonantes suenan apagadas, o disminuya hacia 5–10 ms si los picos están escapando.
4. Encuentre el control Release inmediatamente a la derecha de Attack.
5. Gire Release para establecer con qué rapidez regresa la ganancia después de que la señal cae por debajo del umbral. El valor predeterminado es 200 ms. Aumente Release si escucha bombeo o respiración entre palabras; disminúyalo si el compresor mantiene el nivel reducido demasiado tiempo entre sílabas.
6. Hable al micrófono a un nivel normal y observe la barra Gain-reduction. El relleno ámbar debe moverse de forma fluida con su voz. La marca de referencia en la barra indica 6 dB de reducción, que es una cantidad de trabajo típica. Si la barra sube y baja con un ritmo audible, el Release es demasiado corto para su cadencia de habla.
7. Una vez que la barra Gain-reduction se mueve de forma uniforme sin bombeo, los ajustes de ataque y liberación funcionan correctamente en conjunto.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de ajuste |
|---|---|---|---|
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` |
| Barra Gain-reduction | — | 0 a 20 dB GR | — |

**Attack** — Establece con qué rapidez el compresor actúa después de que la entrada supera el umbral. Utiliza un mapeo de control exponencial; la etiqueta muestra los valores por debajo de 10 ms como `X.X ms` y los valores en 10 ms o superiores como `X ms`.

**Release** — Establece con qué rapidez regresa la ganancia después de que la entrada cae por debajo del umbral. Utiliza un mapeo de control exponencial; la etiqueta muestra los valores como `X ms`.

**Barra Gain-reduction** — Una franja ámbar horizontal que se llena desde la derecha. Alcanza un máximo de 20 dB de reducción. Una marca señala el punto de 6 dB. Úsela como referencia visual principal mientras ajusta el ataque y la liberación.

## Consejos

- La barra Gain-reduction se actualiza aproximadamente a 30 Hz con balística suavizada, por lo que los cambios pequeños y rápidos en su voz aparecerán ligeramente promediados. Evalúe el bombeo por el oído, no únicamente por el medidor.
- Attack y Release interactúan con Ratio y Thresh. Si cambia el umbral o la relación de forma significativa, vuelva a verificar el ataque y la liberación. Consulte [Ajustar el umbral del compresor](adjust-compressor-threshold.md) y [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md).
- Para una compresión lenta y transparente en voz, pruebe Attack alrededor de 30–50 ms y Release alrededor de 300–500 ms. Para un control de picos más preciso, pruebe Attack alrededor de 5–10 ms y Release alrededor de 100–150 ms.
- La curva de transferencia y su punto de envoltura en tiempo real muestran la relación estática entrada/salida, pero no animan directamente los tiempos de ataque y liberación. Use la barra Gain-reduction para retroalimentación dinámica.

## Solución de problemas

- **Bombeo o respiración audible entre palabras** — El Release es demasiado corto. Aumente Release hasta que el nivel se recupere de forma uniforme entre sílabas en lugar de regresar bruscamente.
- **Los transitorios rápidos o las consonantes suenan aplastados** — El Attack es demasiado corto. Aumente Attack para dejar pasar el transitorio inicial antes de que el compresor actúe.
- **El compresor no reacciona en absoluto a los picos** — Es posible que Attack esté en su valor máximo o cerca de él (300.0 ms). Disminuya Attack. Confirme también que la etapa del compresor está habilitada y que el umbral está configurado por debajo de su nivel de entrada habitual. Consulte [Ajustar el umbral del compresor](adjust-compressor-threshold.md).
- **La barra Gain-reduction está fijada en el máximo** — El compresor está aplicando su reducción máxima de 20 dB. Es probable que el Release sea demasiado largo en relación con su cadencia de habla, o que Ratio y Thresh juntos sean demasiado agresivos. Reduzca Release y luego vuelva a verificar Thresh y Ratio.

## Relacionado

- [Ver la reducción de ganancia en tiempo real mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Establecer la relación de compresión para voz](set-compression-ratio-for-voice.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
