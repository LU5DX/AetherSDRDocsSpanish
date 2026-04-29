# Ajustar el ataque y la liberación para una compresión de sonido natural

Los controles de ataque (Attack) y liberación (Release) determinan la rapidez con que el compresor actúa sobre los transitorios fuertes y la rapidez con que los suelta después. Ajustarlos correctamente es lo que diferencia una compresión transparente y natural de un artefacto de bombeo audible.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. El tile permanece oculto hasta que su etapa se habilite mediante el widget CHAIN. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md) si el tile no aparece.
- Decida si está ajustando la ruta TX (subcontenedor "Aetherial Compressor") o la ruta RX (subcontenedor "Aetherial AGC-C"). Ambas tienen controles independientes de Attack y Release con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco perillas en la parte inferior del tile del compresor. Las perillas están etiquetadas, de izquierda a derecha, como Thresh, Ratio, Attack, Release y Makeup.
2. Observe la barra de reducción de ganancia (la franja horizontal ámbar sobre la fila de perillas) mientras habla al micrófono (TX) o mientras se reproduce audio (RX). La barra se llena desde la derecha; una marca indica 6 dB de reducción.
3. Gire la perilla **Attack** para establecer la rapidez con que el compresor responde después de que la entrada supera el umbral. Gire a la izquierda para un bloqueo más rápido (mayor control de transitorios); gire a la derecha para un inicio más lento (mayor paso de transitorios).
4. Gire la perilla **Release** para establecer la rapidez con que la ganancia se recupera tras bajar la entrada por debajo del umbral. Gire a la izquierda para una liberación más rápida (sonido más ajustado); gire a la derecha para una liberación más lenta (más suave, menos bombeo).
5. Observe la bola de envolvente en tiempo real sobre la curva de transferencia encima de la fila de perillas. Una bola que sube y regresa bruscamente en cada sílaba indica que Release es demasiado rápido. Una bola que nunca vuelve a la posición de reposo indica que Release es demasiado lento.
6. Repita los pasos 3–5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de −6 dB durante los picos normales de voz y el sonido se sienta uniforme sin bombeo.

## Qué hace cada control

| Perilla | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |

**Attack** — Mapeo exponencial de perilla. Los valores inferiores a 10 ms se muestran como `X.X ms`; los valores de 10 ms en adelante se muestran como `X ms`. Tiempos de ataque más cortos bloquean los picos con mayor rapidez, pero pueden apagar las consonantes. Tiempos de ataque más largos dejan pasar los transitorios antes de que la compresión entre en acción.

**Release** — Mapeo exponencial de perilla. Se muestra como `X ms`. Tiempos de liberación más cortos permiten que la ganancia regrese rápidamente entre sílabas; si son demasiado cortos, el compresor produce bombeo audible. Tiempos de liberación más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se configuran demasiado largos.

## Consejos

- La barra de reducción de ganancia se actualiza aproximadamente a 30 Hz con balística suavizada, por lo que refleja la envolvente promediada en lugar de los picos instantáneos. Confíe en su oído además del medidor.
- Un punto de partida que funciona para la mayoría de las transmisiones de voz en SSB: Attack de 10–20 ms, Release de 150–300 ms. Ajuste desde ahí según el comportamiento de la barra de reducción de ganancia.
- Haga doble clic en la etapa COMP del widget CHAIN para abrir el editor completo, que también expone los controles Knee y Limiter. El suavizado de Knee puede reducir la necesidad de una sincronización de ataque extremadamente precisa. Consulte [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente al mover una perilla; no se necesita ningún paso de guardado explícito.

## Solución de problemas

- **Bombeo o respiración audible en cada sílaba** — Release es demasiado rápido. Aumente el valor de Release. Pruebe un rango de inicio de 200–500 ms.
- **La ganancia nunca se recupera completamente entre palabras; todo suena aplastado** — Release es demasiado lento, o Ratio es demasiado alto. Reduzca Release y verifique que Ratio no esté configurado por encima de 6:1 para trabajo normal de voz.
- **Los transitorios fuertes aún recortan incluso con un Attack rápido** — Attack no puede configurarse en 0 ms; el mínimo es 0.1 ms. Si el recorte persiste, habilite el limitador en el editor completo. Consulte [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El valor de la perilla se restablece inesperadamente** — Otra fuente (como una carga de perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Reajuste y el nuevo valor persistirá de inmediato.

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Establecer la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en tiempo real mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
