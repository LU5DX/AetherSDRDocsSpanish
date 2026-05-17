# Ajuste de Ataque / Liberación para una Compresión de Sonido Natural

Los perillas de Ataque y Liberación controlan la rapidez con la que el compresor actúa sobre los transitorios fuertes y la rapidez con la que se recupera después. Ajustarlos correctamente es lo que diferencia una compresión transparente y de sonido natural de un bombeo audible no deseado.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. El mosaico está oculto hasta que su etapa se habilite a través del widget CHAIN. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico no se muestra.
- Cuando una etapa del compresor está en bypass, todo el mosaico se renderiza con opacidad reducida (aproximadamente el 55% del brillo total). Esto es solo un indicador visual y no afecta la configuración de las perillas.
- Decida si está ajustando la ruta de TX (subcontenedor "Aetherial Compressor") o la ruta de RX (subcontenedor "Aetherial AGC-C"). Ambos tienen perillas de Ataque y Liberación independientes con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco perillas en la parte inferior del mosaico del compresor. Las perillas están etiquetadas como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Observe la barra de reducción de ganancia (la franja horizontal de color ámbar sobre la fila de perillas) mientras habla por el micrófono (TX) o mientras se reproduce audio (RX). La franja se llena desde la derecha; una marca indica 6 dB de reducción.
3. Gire la perilla **Attack** para establecer la rapidez con la que el compresor responde después de que la entrada supera el umbral. Gire hacia la izquierda para una sujeción más rápida (mayor control de transitorios), hacia la derecha para un inicio más lento (mayor paso de transitorios).
4. Gire la perilla **Release** para establecer la rapidez con la que se recupera la ganancia después de que la entrada vuelve a caer por debajo del umbral. Gire hacia la izquierda para una liberación más rápida (sonido más ajustado), hacia la derecha para una liberación más lenta (más suave, menos bombeo).
5. Observe la bola de envolvente en vivo en la curva de transferencia sobre la fila de perillas. Una bola que sube rápidamente y vuelve a bajar de golpe en cada sílaba sugiere que la Liberación es demasiado rápida. Una bola que nunca vuelve al reposo sugiere que la Liberación es demasiado lenta.
6. Repita los pasos 3 a 5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de -6 dB durante los picos normales del habla y el sonido se sienta uniforme sin bombeo.

## Qué hace cada control

| Perilla | Valor predeterminado | Rango válido | Clave persistida (TX / RX) |
|---|---|---|---|
| Attack | 20.0 ms | 0.1 a 300.0 ms | `ClientCompTxAttackMs` / `ClientCompRxAttackMs` |
| Release | 200 ms | 5 a 2000 ms | `ClientCompTxReleaseMs` / `ClientCompRxReleaseMs` |

**Attack** — Mapeo exponencial de la perilla. Los valores por debajo de 10 ms se muestran como `X.X ms`; los valores de 10 ms y superiores se muestran como `X ms`. Tiempos de ataque más cortos sujetan los picos más rápido, pero pueden apagar las consonantes. Tiempos de ataque más largos permiten que los transitorios pasen antes de que el compresor actúe.

**Release** — Mapeo exponencial de la perilla. Se muestra como `X ms`. Tiempos de liberación más cortos permiten que la ganancia regrese rápidamente entre sílabas; si es demasiado corto, el compresor bombea de forma audible. Tiempos de liberación más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se configuran demasiado largos.

## Uso del editor de valor en línea

Cuando hace clic en la etiqueta del valor numérico de una perilla, esta se transforma en un campo de texto editable. Esto permite una entrada numérica precisa sin necesidad de arrastrar la perilla.

1. Haga clic en el valor numérico debajo de cualquier perilla (Thresh, Ratio, Attack, Release o Makeup). El texto del valor se convierte en un campo de entrada resaltado con un borde cian.
2. Escriba el valor deseado. Los formatos admitidos incluyen:
   - Números simples: `150`
   - Números con unidades: `150 ms`
   - Formato de coma decimal local: `12,5`
   - Valores con signo negativo: `−18`
3. Presione **Enter** o haga clic en cualquier lugar fuera del editor para confirmar el valor. La perilla se actualiza inmediatamente.
4. Presione **Escape** para cancelar la edición y revertir al valor anterior.

El editor en línea está habilitado de forma predeterminada para las cinco perillas. No se puede deshabilitar en la vista del applet.

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz con balística suavizada, por lo que refleja la envolvente promedio en lugar de picos instantáneos. Confíe en sus oídos junto con el medidor.
- La visualización de la curva de transferencia almacena en caché las etiquetas de los ejes para mejorar el rendimiento. Las etiquetas se reconstruyen automáticamente cuando cambia al modo compacto (por ejemplo, al alternar entre el mosaico del applet y el editor flotante). Esto garantiza que el tamaño de fuente (9 px en modo completo, 7 px en modo compacto) siempre coincida con la visualización actual sin ningún retraso visual.
- Un punto de partida que funciona para la mayoría de la voz en SSB: Attack de 10 a 20 ms, Release de 150 a 300 ms. Ajuste a partir de ahí según el comportamiento de la barra de reducción de ganancia.
- Si el mosaico aparece atenuado, la etapa del compresor está actualmente en bypass. Vuelva a habilitarla a través del widget CHAIN antes de evaluar la configuración de las perillas.
- Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo, que también expone los controles Knee (rodilla) y Limiter (limitador). El suavizado de la rodilla puede reducir la necesidad de un ajuste extremadamente preciso del ataque. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente cuando mueve una perilla; no se necesita un paso de guardado explícito.
- Utilice el editor de valor en línea para valores exactos y repetibles. Por ejemplo, escriba `12.5` para Attack en lugar de arrastrar para aproximarse.

## Solución de problemas

- **Bombeo o respiración audible en cada sílaba** — La Liberación es demasiado rápida. Aumente el valor de Release. Pruebe con un rango inicial de 200 a 500 ms.
- **La ganancia nunca se recupera completamente entre palabras; todo suena aplastado** — La Liberación es demasiado lenta, o la Relación (Ratio) es demasiado alta. Reduzca Release y verifique que Ratio no esté configurada por encima de 6:1 para trabajo de voz normal.
- **Los transitorios fuertes siguen recortando incluso con un Attack rápido** — Attack no se puede configurar a 0 ms; el mínimo es 0.1 ms. Si el recorte persiste, habilite el limitador en el editor completo. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El mosaico está atenuado y el compresor parece no estar haciendo nada** — La etapa está en bypass. Actívela a través del widget CHAIN. El mosaico vuelve al brillo completo cuando la etapa está activa.
- **El valor de la perilla se restablece inesperadamente** — Otra fuente (como la carga de un perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Vuelva a ajustar y el nuevo valor se conservará inmediatamente.
- **El valor del editor en línea es rechazado** — La entrada debe ser un número válido dentro del rango válido de la perilla. Si el valor está fuera del rango, se ajusta automáticamente. Los caracteres no numéricos (que no sean separadores decimales, signo y coma) hacen que la edición sea ignorada.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
