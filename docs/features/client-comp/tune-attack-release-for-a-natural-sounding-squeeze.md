# Ajuste de Ataque/Soltada para una Compresión de Sonido Natural

Los mandos de Ataque y Soltada controlan la rapidez con que el compresor actúa sobre los transitorios fuertes y la rapidez con que los libera posteriormente. Ajustarlos correctamente es lo que diferencia una compresión transparente y de sonido natural de un bombeo audible no deseado.

## Antes de comenzar

- El applet Aetherial Compressor (TX) o Aetherial AGC-C (RX) debe estar visible. El panel permanece oculto hasta que su etapa se habilita a través del widget CHAIN. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el panel no se muestra.
- Cuando una etapa del compresor está en bypass, todo el panel se muestra con opacidad reducida (aproximadamente al 55% del brillo total). Esto es solo un indicador visual y no afecta la configuración de los mandos.
- Decida si está ajustando la ruta de TX (subcontenedor "Aetherial Compressor") o la ruta de RX (subcontenedor "Aetherial AGC-C"). Ambos tienen mandos independientes de Ataque y Soltada con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco mandos en la parte inferior del panel del compresor. Los mandos están etiquetados como **Thresh**, **Ratio**, **Attack**, **Release** y **Makeup**, de izquierda a derecha.
2. Observe la barra de reducción de ganancia (la franja horizontal de color ámbar sobre la fila de mandos) mientras habla por el micrófono (TX) o mientras se reproduce audio (RX). La barra se llena desde la derecha; una marca indica 6 dB de reducción.
3. Gire el mando **Attack** para definir la rapidez con que el compresor responde después de que la entrada supera el umbral. Gírelo a la izquierda para una actuación más rápida (mayor control de transitorios), a la derecha para un inicio más lento (mayor paso de transitorios).
4. Gire el mando **Release** para definir la rapidez con que se recupera la ganancia después de que la entrada vuelve a estar por debajo del umbral. Gírelo a la izquierda para una soltada más rápida (sonido más ajustado), a la derecha para una soltada más lenta (más suave, menos bombeo).
5. Observe la bola de envolvente en tiempo real sobre la curva de transferencia, encima de la fila de mandos. Una bola que sube y retrocede rápidamente en cada sílaba sugiere que la Soltada es demasiado rápida. Una bola que nunca vuelve al reposo sugiere que la Soltada es demasiado lenta.
6. Repita los pasos 3 a 5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de −6 dB durante los picos normales del habla y el sonido se sienta uniforme sin bombeo.

## Función de cada control

| Mando   | Valor predeterminado | Rango válido   | Comportamiento |
|---------|-----------|---------------|----------|
| Attack  | 20.0 ms   | 0.1 a 300.0 ms | Mapeo exponencial (0.1 * 3000^n). Define la rapidez con que el compresor actúa después de superar el umbral. |
| Release | 200 ms    | 5 a 2000 ms   | Mapeo exponencial (5 * 400^n). Define la rapidez con que la ganancia regresa después de que la entrada vuelve a estar por debajo del umbral. |
| Drive   | 0.0 dB    | 0.0 a 18.0 dB | Aumento de ganancia previo a la compresión con ecualización automática vinculada. Envía más señal a través del umbral para que el compresor actúe con más fuerza y, simultáneamente, agrega la misma ganancia en la salida para que el RMS promedio suba junto con los picos en lugar de caer. Se muestra solo en el panel flotante StripCompPanel (columna derecha). La etiqueta se muestra como '+X.X dB'. |
| Phase   | 0 etapas | 0 a 6 etapas | Número de secciones de paso total en cascada (0 = desactivado). Cada etapa añade 12 dB/octava de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos asimétricos de la voz antes de la compresión para reducir el PAPR. Se muestra solo en el panel flotante StripCompPanel (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. |

**Attack** — Mapeo de mando exponencial. Los valores por debajo de 10 ms se muestran como `X.X ms`; los valores de 10 ms o más se muestran como `X ms`. Tiempos de ataque más cortos actúan sobre los picos más rápido, pero pueden opacar las consonantes. Tiempos de ataque más largos permiten el paso de los transitorios antes de que el compresor actúe.

**Release** — Mapeo de mando exponencial. Se muestra como `X ms`. Tiempos de soltada más cortos permiten que la ganancia regrese rápidamente entre sílabas; si es demasiado corto, el compresor bombea de forma audible. Tiempos de soltada más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se ajustan demasiado largos.

## Uso del editor de valor en línea

Al hacer clic en la etiqueta del valor numérico de un mando, esta se transforma en un campo de texto editable. Esto permite una entrada numérica precisa sin necesidad de arrastrar el mando.

1. Haga clic en el valor numérico debajo de cualquier mando (Thresh, Ratio, Attack, Release o Makeup). El texto del valor se convierte en un campo de entrada resaltado con un borde cian.
2. Escriba el valor deseado. Los formatos admitidos incluyen:
   - Números simples: `150`
   - Números con unidades: `150 ms`
   - Formato de configuración regional con coma decimal: `12,5`
   - Valores con signo negativo: `−18`
3. Presione **Enter** o haga clic en cualquier lugar fuera del editor para confirmar el valor. El mando se actualiza inmediatamente.
4. Presione **Escape** para cancelar la edición y volver al valor anterior.

El editor en línea está habilitado de forma predeterminada para los cinco mandos. No se puede deshabilitar en la vista del applet.

## Consejos

- La barra de reducción de ganancia se actualiza a aproximadamente 30 Hz con balística suavizada, por lo que refleja la envolvente promediada en lugar de los picos instantáneos. Confíe en sus oídos junto con el medidor.
- La visualización de la curva de transferencia almacena en caché las etiquetas de los ejes para mejorar el rendimiento. Las etiquetas se regeneran automáticamente al alternar el modo compacto (por ejemplo, al cambiar entre el panel del applet y el editor flotante). Esto garantiza que el tamaño de fuente (9 px en modo completo, 7 px en modo compacto) siempre coincida con la visualización actual sin ningún retraso visual.
- Un punto de partida que funciona para la mayoría de las voces en SSB: Attack de 10 a 20 ms, Release de 150 a 300 ms. Ajuste a partir de ahí según el comportamiento de la barra de reducción de ganancia.
- Si el panel aparece atenuado, la etapa del compresor está actualmente en bypass. Vuelva a habilitarla a través del widget CHAIN antes de evaluar la configuración de los mandos.
- Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo, que también expone los controles **Knee**, **Limiter**, **Drive** y **Phase**. El ablandamiento de la rodilla (Knee) puede reducir la necesidad de un ajuste extremadamente preciso del ataque. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente al mover un mando; no se necesita ningún paso de guardado explícito.
- Utilice el editor de valor en línea para obtener valores exactos y repetibles. Por ejemplo, escriba `12.5` para Attack en lugar de arrastrar para aproximarlo.

## Solución de problemas

- **Bombeo audible o respiración en cada sílaba** — La Soltada es demasiado rápida. Aumente el valor de Release. Pruebe con un rango inicial de 200 a 500 ms.
- **La ganancia nunca se recupera completamente entre palabras; todo suena comprimido** — La Soltada es demasiado lenta, o la Ratio es demasiado alta. Disminuya Release y verifique que Ratio no esté configurada por encima de 6:1 para trabajo de voz normal.
- **Los transitorios fuertes siguen recortándose incluso con un ataque rápido** — Attack no se puede configurar en 0 ms; el mínimo es 0.1 ms. Si el recorte persiste, habilite el limitador en el editor completo. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El panel está atenuado y el compresor parece no estar haciendo nada** — La etapa está en bypass. Habilítela a través del widget CHAIN. El panel vuelve al brillo completo cuando la etapa está activa.
- **El valor del mando se restablece inesperadamente** — Otra fuente (como la carga de un perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Vuelva a ajustar y el nuevo valor persistirá inmediatamente.
- **El valor del editor en línea es rechazado** — La entrada debe ser un número válido dentro del rango válido del mando. Si el valor está fuera del rango, se ajusta automáticamente. Los caracteres no numéricos (distintos de los separadores decimales, el signo y la coma) provocan que la edición se ignore.

## Soporte de temas

El applet del compresor y su widget de curva de transferencia ahora respetan el tema actual de AetherSDR. Los colores de los siguientes elementos se toman de las variables del tema en lugar de valores fijos:

| Elemento | Variable del tema |
|---------|----------------|
| Fondo del widget | `color.background.0` |
| Líneas de cuadrícula | `color.background.1` |
| Etiquetas de los ejes | `color.text.label` |
| Línea de unidad (identidad) | `color.background.1` |
| Curva de transferencia | `color.accent.dim` |
| Resplandor de la bola de envolvente | `color.accent.warning` |
| Núcleo de la bola de envolvente | `color.text.primary` |

El relleno del control deslizante de reducción de ganancia utiliza el color del tema `color.slider.foreground` aplicado en el ámbito `applet/comp` a través de ThemeManager.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
