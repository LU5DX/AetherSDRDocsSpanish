# Ajuste del Attack y Release para una compresión de sonido natural

Ajuste los controles **Attack** y **Release** para controlar con qué rapidez el compresor responde a los picos fuertes de voz y se recupera de ellos. Establecer correctamente estos valores de temporización evita que el compresor suene abrupto o que produzca un efecto de bombeo entre sílabas.

## Antes de comenzar

- La etapa del compresor debe estar habilitada (bypass desactivado). Si el bloque COMPRESSOR está oculto, habilite la etapa primero desde el widget CHAIN. Consulte [Desactivar el bypass del compresor desde la cadena](bypass-the-compressor-from-the-chain.md).
- El subcontenedor COMPRESSOR debe estar visible dentro del contenedor principal PooDoo Audio (TXDSP).
- Tenga un micrófono activo para poder hablar mientras observa cómo responde en tiempo real la barra de reducción de ganancia.

## Pasos

1. Localice el subcontenedor COMPRESSOR en el panel del applet.
2. Encuentre el control **Attack** en la fila de cinco controles ubicada en la parte inferior del bloque.
3. Gire **Attack** mientras habla a un nivel normal. Observe la barra de reducción de ganancia: un tiempo de ataque más corto hace que la barra se llene rápidamente tras el inicio de cada palabra; un tiempo de ataque más largo deja pasar el transitorio inicial antes de aplicar la compresión.
4. Encuentre el control **Release**, inmediatamente a la derecha de **Attack**.
5. Gire **Release** mientras habla. Un tiempo de release más corto hace que el compresor se recupere rápidamente entre palabras; si es demasiado corto, produce un efecto de bombeo audible. Un release más largo mantiene la reducción de ganancia estable a lo largo de las sílabas, lo que puede sonar apagado en el habla rápida.
6. Repita los pasos 3–5 hasta que la barra de reducción de ganancia suba y baje suavemente con el ritmo de su voz y el audio suene natural.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` | Velocidad con la que el compresor actúa tras superar el umbral la señal de entrada. Usa mapeo de control exponencial. Las etiquetas muestran un decimal por debajo de 10 ms y milisegundos enteros por encima. |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` | Velocidad con la que la ganancia se recupera tras bajar la señal de entrada por debajo del umbral. Usa mapeo de control exponencial. La etiqueta muestra milisegundos enteros. |

Los demás controles de la misma fila son:

| Control | Valor predeterminado | Rango válido | Clave persistida |
|---|---|---|---|
| Thresh | -18.0 dB | -60.0 a 0.0 dB | `ClientCompTxThresholdDb` |
| Ratio | 3.0 | 1.0 a 20.0 | `ClientCompTxRatio` |
| Makeup | 0.0 dB | -12.0 a 24.0 dB | `ClientCompTxMakeupDb` |

La **barra de reducción de ganancia** es la franja ámbar horizontal situada sobre la fila de controles. Se llena desde la derecha y tiene una marca de referencia en 6 dB. La reducción máxima indicada es de 20 dB. Úsela para verificar que Attack y Release producen la respuesta deseada mientras habla.

## Consejos

- Comience con un Attack largo (40–80 ms) para preservar el impacto de las consonantes; redúzcalo solo si los picos pasan por encima antes de que la compresión actúe.
- Si la barra de reducción de ganancia sube y baja rápidamente entre palabras, aumente el Release hasta que el movimiento sea más suave.
- La bola de envelope sobre la curva de transferencia se desplaza a lo largo de la curva en tiempo real. Observarla junto con la barra de reducción de ganancia ofrece una segunda vista de la rapidez con que se aplica y libera la ganancia.
- Los ajustes de rodilla y limitador (almacenados como `ClientCompTxKneeDb`, `ClientCompTxLimEnabled`, `ClientCompTxLimCeilingDb`) no son accesibles desde los controles del applet. Abra el editor completo si necesita ajustarlos. Consulte [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).

## Solución de problemas

- **La barra de reducción de ganancia no se mueve cuando habla** — Es posible que la etapa del compresor esté en bypass, o que el umbral esté ajustado demasiado alto para el nivel de su micrófono. Confirme que la etapa está habilitada y verifique el control Thresh. Consulte [Ajustar el umbral del compresor](adjust-compressor-threshold.md).
- **El audio suena como si bombeara o respirara** — El Release es demasiado corto. Gire el control **Release** en sentido horario para aumentar el tiempo de recuperación.
- **Los inicios de palabras fuertes siguen distorsionando** — El Attack es demasiado largo y permite que los picos pasen antes de que la compresión actúe. Gire el control **Attack** en sentido antihorario para reducir el tiempo de ataque.

## Relacionados

- [Ver la reducción de ganancia en vivo mientras habla](watch-live-gain-reduction-while-speaking.md)
- [Ajustar el umbral del compresor](adjust-compressor-threshold.md)
- [Configurar la ratio de compresión para voz](set-compression-ratio-for-voice.md)
- [Aplicar ganancia de compensación tras la compresión](apply-make-up-gain-after-compression.md)
- [Abrir el editor completo del compresor para los controles de rodilla y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
