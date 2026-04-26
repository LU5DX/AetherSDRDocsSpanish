# Ajustar el ataque y la liberación para una compresión de sonido natural

Los controles de ataque (Attack) y liberación (Release) determinan con qué rapidez el compresor actúa sobre las transientes fuertes y con qué rapidez las suelta después. Calibrarlos correctamente es lo que distingue una compresión transparente y natural de un artefacto de bombeo audible.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. El panel permanece oculto hasta que su etapa se habilita mediante el widget CHAIN. Consulte [Omitir el compresor desde la cadena](bypass-the-compressor-from-the-chain.md) si el panel no aparece.
- Decida si está ajustando la ruta TX (subcontenedor "Aetherial Compressor") o la ruta RX (subcontenedor "Aetherial AGC-C"). Ambas tienen controles de Attack y Release independientes con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco perillas en la parte inferior del panel del compresor. Las perillas están etiquetadas de izquierda a derecha: Thresh, Ratio, Attack, Release y Makeup.
2. Observe la barra de reducción de ganancia (la franja horizontal ámbar sobre la fila de perillas) mientras habla al micrófono (TX) o mientras se reproduce audio (RX). La franja se llena desde la derecha; una marca indica 6 dB de reducción.
3. Gire la perilla **Attack** para establecer con qué rapidez responde el compresor después de que la señal supera el umbral. Gire a la izquierda para un cierre más rápido (mayor control de transientes); a la derecha para un inicio más lento (mayor paso de transientes).
4. Gire la perilla **Release** para establecer con qué rapidez se recupera la ganancia después de que la señal cae por debajo del umbral. Gire a la izquierda para una liberación más rápida (sonido más apretado); a la derecha para una liberación más lenta (más suave, menos bombeo).
5. Observe la bola de envolvente en vivo sobre la curva de transferencia, encima de la fila de perillas. Una bola que sube y baja bruscamente en cada sílaba indica que Release es demasiado rápido. Una bola que nunca regresa al reposo indica que Release es demasiado lento.
6. Repita los pasos 3–5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de −6 dB durante los picos normales de la voz y el sonido resulte uniforme sin bombeo.

## Qué hace cada control

| Perilla | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |

**Attack** — Asignación exponencial de la perilla. Los valores inferiores a 10 ms se muestran como `X.X ms`; los valores de 10 ms en adelante se muestran como `X ms`. Tiempos de ataque más cortos suprimen los picos con mayor rapidez, pero pueden atenuar las consonantes. Tiempos de ataque más largos permiten que las transientes pasen antes de que la compresión actúe.

**Release** — Asignación exponencial de la perilla. Se muestra como `X ms`. Tiempos de liberación más cortos permiten que la ganancia se recupere rápidamente entre sílabas; si son demasiado cortos, el compresor genera un bombeo audible. Tiempos de liberación más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se configuran demasiado largos.

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz con balística suavizada, por lo que refleja la envolvente promediada en lugar de los picos instantáneos. Confíe en su oído junto con el medidor.
- Un punto de partida que funciona bien para la mayoría de las transmisiones de voz en SSB: Attack de 10–20 ms, Release de 150–300 ms. Ajuste a partir de ahí según el comportamiento de la barra de reducción de ganancia.
- Haga doble clic en la etapa COMP del widget CHAIN para abrir el editor completo, que también expone los controles Knee y Limiter. Un Knee suavizado puede reducir la necesidad de una temporización de ataque extremadamente precisa. Consulte [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente al mover una perilla; no se necesita ningún paso de guardado explícito.

## Solución de problemas

- **Bombeo o respiración audibles en cada sílaba** — Release es demasiado rápido. Aumente el valor de Release. Pruebe un rango de 200–500 ms como punto de partida.
- **La ganancia nunca se recupera completamente entre palabras; todo suena comprimido** — Release es demasiado lento, o Ratio es demasiado alto. Disminuya Release y verifique que Ratio no esté por encima de 6:1 para trabajo de voz normal.
- **Las transientes fuertes aún recortan incluso con un Attack rápido** — Attack no puede ajustarse a 0 ms; el mínimo es 0.1 ms. Si el recorte persiste, habilite el limitador en el editor completo. Consulte [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El valor de la perilla se restablece de forma inesperada** — Otra fuente (como la carga de un perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Vuelva a ajustar y el nuevo valor se conservará de inmediato.

## Relacionados

- [Descripción general de Aetherial Compressor (TX) / Aetherial AGC-C (RX)](overview.md)
- [Ajustar el umbral del compresor (lado TX o RX)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Configurar la relación de compresión para voz (TX) o para audio recibido (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Aplicar ganancia de compensación después de la compresión](apply-make-up-gain-after-compression.md)
- [Observar la reducción de ganancia en vivo mientras habla o escucha](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Abrir el editor completo del compresor para los controles de knee y limitador](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
