# Ajuste de Ataque / Liberación para una Compresión de Sonido Natural

Los controles de Ataque y Liberación determinan la rapidez con que el compresor actúa sobre los transitorios fuertes y la velocidad con que se recupera después. Ajustarlos correctamente marca la diferencia entre una compresión transparente y de sonido natural, y un bombeo audible no deseado.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. El mosaico permanece oculto hasta que su etapa se habilite a través del widget CHAIN. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico no se muestra.
- Cuando una etapa del compresor está desviada, todo el mosaico se muestra con opacidad reducida (aproximadamente al 55% del brillo total). Esto es solo un indicador visual y no afecta la configuración de sus controles.
- Decida si está ajustando la ruta de TX ("Aetherial Compressor" sub-contenedor) o la ruta de RX ("Aetherial AGC-C" sub-contenedor). Ambos tienen controles independientes de Ataque y Liberación con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco controles en la parte inferior del mosaico del compresor. Los controles están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Observe la barra de reducción de ganancia (la franja horizontal de color ámbar sobre la fila de controles) mientras habla por el micrófono (TX) o mientras se reproduce audio (RX). La barra se llena desde la derecha; una marca de graduación indica 6 dB de reducción.
3. Gire el control **Attack** para ajustar la rapidez con que responde el compresor después de que la entrada supera el umbral. Gire a la izquierda para una sujeción más rápida (mayor control de transitorios), a la derecha para un inicio más lento (mayor paso de transitorios).
4. Gire el control **Release** para ajustar la velocidad con que se recupera la ganancia después de que la entrada vuelve a estar por debajo del umbral. Gire a la izquierda para una liberación más rápida (sonido más ajustado), a la derecha para una liberación más lenta (sonido más suave, con menos bombeo).
5. Observe la bola de envolvente en vivo en la curva de transferencia sobre la fila de controles. Una bola que sube rápidamente y retrocede bruscamente en cada sílaba sugiere que Release es demasiado rápida. Una bola que nunca regresa al reposo sugiere que Release es demasiado lenta.
6. Repita los pasos 3–5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de −6 dB durante los picos normales de voz y el sonido se sienta uniforme sin bombeo.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |

**Attack** — Mapeo de control exponencial. Los valores por debajo de 10 ms se muestran como `X.X ms`; los valores de 10 ms o más se muestran como `X ms`. Tiempos de ataque más cortos sujetan los picos más rápido, pero pueden apagar las consonantes. Tiempos de ataque más largos permiten que los transitorios pasen antes de que la compresión se active.

**Release** — Mapeo de control exponencial. Se muestra como `X ms`. Tiempos de liberación más cortos permiten que la ganancia regrese rápidamente entre sílabas; si es demasiado corta, el compresor bombea audiblemente. Tiempos de liberación más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se ajustan demasiado largos.

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz con balística suavizada, por lo que refleja la envolvente promediada en lugar de los picos instantáneos. Confíe en sus oídos junto con el medidor.
- Un punto de partida que funciona para la mayoría de las voces en SSB: Attack de 10 a 20 ms, Release de 150 a 300 ms. Ajuste desde allí según el comportamiento de la barra de reducción de ganancia.
- Si el mosaico aparece atenuado, la etapa del compresor está actualmente desviada. Vuelva a habilitarla a través del widget CHAIN antes de evaluar la configuración de los controles.
- Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo, que también expone los controles de Knee y Limiter. Suavizar la rodilla (Knee) puede reducir la necesidad de un ajuste de ataque extremadamente preciso. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente cuando mueve un control; no se necesita ningún paso de guardado explícito.

## Solución de problemas

- **Bombeo audible o respiración en cada sílaba** — Release es demasiado rápida. Aumente el valor de Release. Pruebe con un rango inicial de 200–500 ms.
- **La ganancia nunca se recupera completamente entre palabras; todo suena comprimido** — Release es demasiado lenta, o Ratio es demasiado alto. Disminuya Release y verifique que Ratio no esté configurado por encima de 6:1 para trabajo de voz normal.
- **Los transitorios fuertes aún recortan incluso con un Attack rápido** — Attack no se puede configurar a 0 ms; el mínimo es 0.1 ms. Si el recorte persiste, habilite el limitador en el editor completo. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El mosaico está atenuado y el compresor parece no estar haciendo nada** — La etapa está desviada. Habilítela a través del widget CHAIN. El mosaico vuelve al brillo completo cuando la etapa está activa.
- **El valor del control se restablece inesperadamente** — Otra fuente (como la carga de un perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Reajuste y el nuevo valor persistirá inmediatamente.

## Relacionado

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
