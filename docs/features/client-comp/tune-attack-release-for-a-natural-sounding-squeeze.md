# Ajuste de Ataque / Liberación para una Compresión de Sonido Natural

Los mandos de Ataque y Liberación controlan la rapidez con la que el compresor actúa sobre los transitorios fuertes y la rapidez con la que se recupera después. Ajustarlos correctamente es lo que diferencia una compresión transparente y de sonido natural de un bombeo audible.

## Antes de comenzar

- El applet Compresor Aetherial (TX) o AGC-C Aetherial (RX) debe estar visible. El mosaico está oculto hasta que su etapa se habilite a través del widget CHAIN. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico no se muestra.
- Cuando una etapa del compresor está desactivada, todo el mosaico se renderiza con opacidad reducida (aproximadamente al 55% del brillo total). Esto es solo un indicador visual y no afecta la configuración de sus mandos.
- Decida si está ajustando la ruta de TX ("Aetherial Compressor" sub-contenedor) o la ruta de RX ("Aetherial AGC-C" sub-contenedor). Ambos tienen mandos de Ataque y Liberación independientes con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del mosaico del compresor. Los mandos están etiquetados, de izquierda a derecha, Thresh, Ratio, Attack, Release y Makeup.
2. Observe la barra de reducción de ganancia (la barra horizontal de color ámbar sobre la fila de mandos) mientras habla por el micrófono (TX) o mientras se reproduce audio (RX). La barra se llena desde la derecha; una marca indica 6 dB de reducción.
3. Gire el mando **Attack** para ajustar la rapidez con la que el compresor responde después de que la entrada supere el umbral. Gire a la izquierda para una acción más rápida (más control de transitorios), a la derecha para un inicio más lento (más paso de transitorios).
4. Gire el mando **Release** para ajustar la rapidez con la que la ganancia se recupera después de que la entrada vuelva a caer por debajo del umbral. Gire a la izquierda para una liberación más rápida (sonido más ajustado), a la derecha para una liberación más lenta (sonido más suave, menos bombeo).
5. Observe la bola de sobre dinámico en la curva de transferencia sobre la fila de mandos. Una bola que sube rápidamente y vuelve a bajar bruscamente en cada sílaba sugiere que Release es demasiado rápido. Una bola que nunca vuelve al reposo sugiere que Release es demasiado lento.
6. Repita los pasos 3–5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de −6 dB durante los picos normales del habla y el sonido se sienta uniforme sin bombeo.

## Función de cada control

| Mando | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |

**Attack** — Mapeo exponencial del mando. Los valores por debajo de 10 ms se muestran como `X.X ms`; los valores de 10 ms o más se muestran como `X ms`. Los tiempos de ataque más cortos limitan los picos más rápido, pero pueden apagar las consonantes. Los tiempos de ataque más largos permiten que los transitorios pasen antes de que actúe la compresión.

**Release** — Mapeo exponencial del mando. Se muestra como `X ms`. Los tiempos de liberación más cortos permiten que la ganancia vuelva rápidamente entre sílabas; si es demasiado corto, el compresor bombea de forma audible. Los tiempos de liberación más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se ajustan demasiado largos.

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz con balística suavizada, por lo que refleja el sobre promediado en lugar de los picos instantáneos. Confíe en sus oídos junto con el medidor.
- La visualización de la curva de transferencia almacena en caché las etiquetas de los ejes por rendimiento. Las etiquetas se reconstruyen automáticamente cuando alterna el modo compacto (por ejemplo, al cambiar entre el mosaico del applet y el editor flotante). Esto asegura que el tamaño de fuente (9 px en modo completo, 7 px en modo compacto) siempre coincida con la pantalla actual sin ningún retraso visual.
- Un punto de partida que funciona para la mayoría de las voces en SSB: Attack 10–20 ms, Release 150–300 ms. Ajuste a partir de ahí según el comportamiento de la barra de reducción de ganancia.
- Si el mosaico aparece atenuado, la etapa del compresor está actualmente desactivada. Vuelva a habilitarla a través del widget CHAIN antes de evaluar la configuración de los mandos.
- Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo, que también expone los controles de Knee y Limiter. Suavizar la rodilla puede reducir la necesidad de una sincronización de ataque extremadamente precisa. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente cuando mueve un mando; no se necesita ningún paso de guardado explícito.

## Solución de problemas

- **Bombeo audible o respiración en cada sílaba** — Release es demasiado rápido. Aumente el valor de Release. Pruebe con un rango de 200–500 ms como punto de partida.
- **La ganancia nunca se recupera completamente entre palabras; todo suena comprimido** — Release es demasiado lento, o Ratio es demasiado alto. Disminuya Release y verifique que Ratio no esté ajustado por encima de 6:1 para trabajo vocal normal.
- **Los transitorios fuertes aún recortan incluso con un Attack rápido** — Attack no se puede ajustar a 0 ms; el mínimo es 0.1 ms. Si el recorte persiste, habilite el limitador en el editor completo. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El mosaico está atenuado y el compresor parece no estar haciendo nada** — La etapa está desactivada. Habilítela a través del widget CHAIN. El mosaico vuelve al brillo completo cuando la etapa está activa.
- **El valor del mando se restablece inesperadamente** — Otra fuente (como la carga de un perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Vuelva a ajustar y el nuevo valor persistirá inmediatamente.

## Relacionado

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
