# Ajuste de Ataque / Liberación para una Compresión de Sonido Natural

Los controles Ataque y Liberación determinan la rapidez con que el compresor reacciona a los transientes fuertes y la velocidad con que se recupera después. Ajustarlos correctamente es lo que diferencia una compresión transparente y natural de un bombeo audible no deseado.

## Antes de comenzar

- La ventana del Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. El panel permanece oculto hasta que su etapa se habilita mediante el widget CHAIN. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el panel no se muestra.
- Cuando una etapa del compresor está desactivada, todo el panel se muestra con opacidad reducida (aproximadamente el 55% del brillo total). Esto es solo un indicador visual y no afecta los ajustes de los controles.
- Decida si está ajustando la ruta de TX ("Aetherial Compressor" sub-contenedor) o la ruta de RX ("Aetherial AGC-C" sub-contenedor). Ambos tienen controles independientes de Ataque y Liberación con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco controles en la parte inferior del panel del compresor. Los controles están etiquetados como Thresh, Ratio, Attack, Release y Makeup, de izquierda a derecha.
2. Observe la barra de reducción de ganancia (la franja horizontal ámbar sobre la fila de controles) mientras habla al micrófono (TX) o mientras se reproduce audio (RX). La barra se llena desde la derecha; una marca indica 6 dB de reducción.
3. Gire el control **Attack** para definir la rapidez con que el compresor responde después de que la entrada supera el umbral. Gírelo a la izquierda para una respuesta más rápida (mayor control de transientes), a la derecha para una activación más lenta (mayor paso de transientes).
4. Gire el control **Release** para definir la rapidez con que se recupera la ganancia después de que la entrada vuelve a estar por debajo del umbral. Gírelo a la izquierda para una liberación más rápida (sonido más ajustado), a la derecha para una liberación más lenta (sonido más suave, con menos bombeo).
5. Observe la bola dinámica del nivel en la curva de transferencia sobre la fila de controles. Una bola que sube rápidamente y vuelve a bajar con cada sílaba sugiere que la liberación es demasiado rápida. Una bola que nunca regresa al reposo sugiere que la liberación es demasiado lenta.
6. Repita los pasos 3 a 5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de −6 dB durante los picos de voz normales y el sonido sea uniforme sin bombeo.

## Función de cada control

| Control  | Valor predeterminado                                                                                                                                                                                                                       | Rango válido                                                                                                                                                              |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Attack   | 20.0 ms                                                                                                                                                                                                                                     | 0.1 a 300.0 ms                                                                                                                                                            |
| Release  | 200 ms                                                                                                                                                                                                                                      | 5 a 2000 ms                                                                                                                                                               |
| Drive    | Aumento de ganancia previo a la compresión. Empuja más señal a través del umbral para que el compresor actúe con más fuerza, elevando la potencia promedio. Combínelo con Phase para mantener los picos limpios.                              | Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta muestra '+X.X dB'. El tooltip explica la reducción de PAPR #2887.                     |
| Phase    | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/oct de rotación de fase a frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza picos de voz asimétricos antes de la compresión para reducir PAPR. | Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Tooltip: 'Pre-comp phase rotator (#2887). 0=off, 4=broadcast default.' |

**Attack** — Asignación de control exponencial. Los valores por debajo de 10 ms se muestran como `X.X ms`; los valores de 10 ms o más se muestran como `X ms`. Tiempos de ataque más cortos comprimen los picos más rápido, pero pueden atenuar las consonantes. Tiempos de ataque más largos permiten que los transientes pasen antes de que el compresor actúe.

**Release** — Asignación de control exponencial. Se muestra como `X ms`. Tiempos de liberación más cortos permiten que la ganancia regrese rápidamente entre sílabas; si es demasiado corto, el compresor bombea audiblemente. Tiempos de liberación más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se ajustan demasiado largos.

## Uso del editor de valor en línea

Al hacer clic en la etiqueta del valor numérico de un control, se transforma en un campo de texto editable. Esto permite la entrada numérica precisa sin arrastrar el control.

1. Haga clic en el valor numérico debajo de cualquier control (Thresh, Ratio, Attack, Release o Makeup). El texto del valor se convierte en un campo de entrada resaltado con un borde cian.
2. Escriba el valor deseado. Los formatos admitidos incluyen:
   - Números simples: `150`
   - Números con unidades: `150 ms`
   - Formato de locale con coma decimal: `12,5`
   - Valores con signo negativo: `−18`
3. Presione **Enter** o haga clic en cualquier lugar fuera del editor para confirmar el valor. El control se actualiza inmediatamente.
4. Presione **Escape** para cancelar la edición y revertir al valor anterior.

El editor en línea está habilitado de forma predeterminada para los cinco controles. No se puede desactivar en la vista de la ventana.

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz con balística suavizada, por lo que refleja el nivel promedio en lugar de los picos instantáneos. Confíe en sus oídos junto con el medidor.
- La pantalla de la curva de transferencia almacena en caché las etiquetas de los ejes para mejorar el rendimiento. Las etiquetas se reconstruyen automáticamente al alternar el modo compacto (por ejemplo, al cambiar entre el panel de la ventana y el editor flotante). Esto asegura que el tamaño de fuente (9 px en modo completo, 7 px en modo compacto) siempre coincida con la pantalla actual sin retraso visual.
- Un punto de partida que funciona para la mayoría de las voces en SSB: Attack de 10 a 20 ms, Release de 150 a 300 ms. Ajuste a partir de ahí según el comportamiento de la barra de reducción de ganancia.
- Si el panel aparece atenuado, la etapa del compresor está actualmente desactivada. Vuelva a habilitarla mediante el widget CHAIN antes de evaluar los ajustes de los controles.
- Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo, que también expone los controles Knee y Limiter. El suavizado de Knee puede reducir la necesidad de un ajuste extremadamente preciso del ataque. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente al mover un control; no es necesario ningún paso de guardado explícito.
- Use el editor de valor en línea para valores exactos y repetibles. Por ejemplo, escriba `12.5` para Attack en lugar de arrastrar para aproximarlo.

## Solución de problemas

- **Bombeo audible o respiración en cada sílaba** — La liberación es demasiado rápida. Aumente el valor de Release. Pruebe con un rango inicial de 200 a 500 ms.
- **La ganancia nunca se recupera completamente entre palabras; todo suena comprimido** — La liberación es demasiado lenta o la relación es demasiado alta. Disminuya Release y verifique que Ratio no esté ajustado por encima de 6:1 para voz normal.
- **Los transientes fuertes aún distorsionan incluso con un Attack rápido** — Attack no se puede ajustar a 0 ms; el mínimo es 0.1 ms. Si la distorsión persiste, active el limitador en el editor completo. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El panel está atenuado y el compresor parece no hacer nada** — La etapa está desactivada. Actívela mediante el widget CHAIN. El panel vuelve al brillo completo cuando la etapa está activa.
- **El valor del control se restablece inesperadamente** — Otra fuente (como la carga de un perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Vuelva a ajustar y el nuevo valor persistirá inmediatamente.
- **El valor del editor en línea es rechazado** — La entrada debe ser un número válido dentro del rango del control. Si el valor está fuera del rango, se ajusta automáticamente. Los caracteres no numéricos (distintos de separadores decimales, signo y coma) hacen que la edición se ignore.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
