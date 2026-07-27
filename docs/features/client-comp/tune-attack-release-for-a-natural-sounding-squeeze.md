# Ataque / Liberación para una Compresión de Sonido Natural

Los controles de Ataque y Liberación determinan la rapidez con que el compresor actúa sobre los transitorios fuertes y la velocidad con que se recupera después. Ajustarlos correctamente es lo que marca la diferencia entre una compresión transparente y de sonido natural, frente a un bombeo audible no deseado.

## Antes de comenzar

- El applet Compresor Aetherial (TX) o AGC-C Aetherial (RX) debe estar visible. El mosaico permanece oculto hasta que su etapa se habilita a través del widget CHAIN. Consulte [Bypass the compressor from the chain](bypass-the-compressor-from-the-chain.md) si el mosaico no se muestra.
- Cuando una etapa del compresor está desviada, todo el mosaico se renderiza con opacidad reducida (aproximadamente el 55% del brillo total). Esto es solo un indicador visual y no afecta la configuración de los controles.
- Decida si está ajustando la ruta TX (subcontenedor "Compresor Aetherial") o la ruta RX (subcontenedor "AGC-C Aetherial"). Ambos tienen controles independientes de Ataque y Liberación con los mismos rangos y comportamiento.

## Pasos

1. Localice la fila de cinco controles en la parte inferior del mosaico del compresor. Los controles están etiquetados como **Thresh**, **Ratio**, **Attack**, **Release** y **Makeup**, de izquierda a derecha.
2. Observe la barra de reducción de ganancia (la franja horizontal de color ámbar sobre la fila de controles) mientras habla al micrófono (TX) o mientras se reproduce audio (RX). La barra se llena desde la derecha; una marca indica 6 dB de reducción.
3. Gire el control **Attack** para definir la rapidez con que el compresor responde después de que la entrada supera el umbral. Gírelo a la izquierda para una acción más rápida (mayor control de transitorios), a la derecha para un inicio más lento (más transitorios pasan sin comprimir).
4. Gire el control **Release** para definir la rapidez con que la ganancia se recupera después de que la entrada vuelve a estar por debajo del umbral. Gírelo a la izquierda para una liberación más rápida (sonido más ajustado), a la derecha para una liberación más lenta (más suave, menos bombeo).
5. Observe la bola de envolvente en vivo en la curva de transferencia sobre la fila de controles. Una bola que sube rápido y retrocede en cada sílaba sugiere que la Liberación es demasiado rápida. Una bola que nunca vuelve a la posición de reposo sugiere que la Liberación es demasiado lenta.
6. Repita los pasos 3 a 5 hasta que la barra de reducción de ganancia se sitúe cerca de la marca de −6 dB durante los picos normales del habla y el sonido sea uniforme sin bombeo.

## Función de cada control

| Control  | Valor predeterminado | Rango válido      |
|----------|----------------------|-------------------|
| Attack   | 20.0 ms              | 0.1 a 300.0 ms   |
| Release  | 200 ms               | 5 a 2000 ms      |
| Drive    | 0.0 dB               | 0.0 a 18.0 dB    |
| Phase    | 0 etapas             | 0 a 6 etapas     |

**Attack** — Mapeo exponencial del control. Los valores inferiores a 10 ms se muestran como `X.X ms`; los valores de 10 ms o más se muestran como `X ms`. Tiempos de ataque más cortos comprimen los picos más rápido, pero pueden apagar las consonantes. Tiempos de ataque más largos permiten que los transitorios pasen antes de que actúe la compresión.

**Release** — Mapeo exponencial del control. Se muestra como `X ms`. Tiempos de liberación más cortos permiten que la ganancia vuelva rápidamente entre sílabas; si es demasiado corto, el compresor bombea audiblemente. Tiempos de liberación más largos producen una reducción de ganancia más suave y sostenida, pero pueden reducir la inteligibilidad si se ajustan demasiado largos.

**Drive** — Aumento de ganancia previo a la compresión con maquillaje automático vinculado. Empuja más señal a través del umbral para que el compresor actúe con más fuerza y, simultáneamente, agrega la misma ganancia en la salida, de modo que el RMS promedio se eleve junto con los picos en lugar de caer. Combínelo con Phase para mantener los picos limpios. Solo se muestra en el StripCompPanel flotante (columna derecha). La etiqueta muestra '+X.X dB'.

**Phase** — Número de secciones de paso total en cascada (0 = desactivado). Cada etapa agrega 12 dB/oct de rotación de fase en frecuencias escalonadas (300/700/1500/2500 Hz, más 1000/2000 Hz opcionales). Simetriza los picos de voz asimétricos antes de la compresión para reducir la PAPR. Solo se muestra en el StripCompPanel flotante (columna derecha). Etiqueta 'Off' cuando es 0, 'N stg' cuando está activo. Información sobre herramientas: 'Pre-comp phase rotator (#2887). Cascada de paso total que simetriza los picos de voz asimétricos antes de la compresión. 0 = desactivado, 4 = valor predeterminado para transmisión.'

## Uso del editor de valores en línea

Al hacer clic en la etiqueta del valor numérico de un control, esta se transforma en un campo de texto editable. Esto permite una entrada numérica precisa sin necesidad de arrastrar el control.

1. Haga clic en el valor numérico debajo de cualquier control (Thresh, Ratio, Attack, Release o Makeup). El texto del valor se convierte en un campo de entrada resaltado con un borde cian.
2. Escriba el valor deseado. Los formatos admitidos incluyen:
   - Números simples: `150`
   - Números con unidades: `150 ms`
   - Formato de configuración regional con coma decimal: `12,5`
   - Valores con signo menos: `−18`
3. Presione **Enter** o haga clic en cualquier lugar fuera del editor para confirmar el valor. El control se actualiza de inmediato.
4. Presione **Escape** para cancelar la edición y volver al valor anterior.

El editor en línea está habilitado de forma predeterminada para los cinco controles. No se puede deshabilitar en la vista del applet.

## Consejos

- La barra de reducción de ganancia se actualiza aproximadamente a 30 Hz con balística suavizada, por lo que refleja la envolvente promedio en lugar de los picos instantáneos. Confíe en sus oídos junto con el medidor.
- La visualización de la curva de transferencia almacena en caché las etiquetas de los ejes para mejorar el rendimiento. Las etiquetas se reconstruyen automáticamente al alternar el modo compacto (por ejemplo, al cambiar entre el mosaico del applet y el editor flotante). Esto garantiza que el tamaño de fuente (9 px en modo completo, 7 px en modo compacto) siempre coincida con la visualización actual sin retraso visual.
- El temporizador de animación del compresor utiliza una sincronización precisa y ejecuta repintados de forma continua para obtener una retroalimentación visual precisa. La bola de envolvente y la barra de reducción de ganancia se actualizan suavemente en cada tick de animación, independientemente del estado de estabilización.
- Un punto de partida que funciona para la mayoría de las voces en SSB: Attack 10–20 ms, Release 150–300 ms. Ajuste a partir de ahí según el comportamiento de la barra de reducción de ganancia.
- Si el mosaico aparece atenuado, la etapa del compresor está actualmente desviada. Vuelva a habilitarla a través del widget CHAIN antes de evaluar la configuración de los controles.
- Haga doble clic en la etapa COMP en el widget CHAIN para abrir el editor completo, que también expone los controles **Knee**, **Limiter**, **Drive** y **Phase**. El suavizado de la rodilla puede reducir la necesidad de un ajuste extremadamente preciso del ataque. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- Tanto Attack como Release se guardan inmediatamente al mover un control; no se necesita ningún paso de guardado explícito.
- Use el editor de valores en línea para valores exactos y repetibles. Por ejemplo, escriba `12.5` para Attack en lugar de arrastrar para aproximar.

## Solución de problemas

- **Bombeo audible o respiración en cada sílaba** — La Liberación es demasiado rápida. Aumente el valor de Release. Pruebe con un rango inicial de 200–500 ms.
- **La ganancia nunca se recupera completamente entre palabras; todo suena comprimido** — La Liberación es demasiado lenta o la Relación es demasiado alta. Disminuya Release y verifique que Ratio no esté por encima de 6:1 para trabajo de voz normal.
- **Los transitorios fuertes aún recortan incluso con un ataque rápido** — Attack no se puede configurar a 0 ms; el mínimo es 0.1 ms. Si el recorte persiste, active el limitador en el editor completo. Consulte [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md).
- **El mosaico está atenuado y el compresor no parece estar haciendo nada** — La etapa está desviada. Habilítela a través del widget CHAIN. El mosaico vuelve al brillo completo cuando la etapa está activa.
- **El valor del control se restablece inesperadamente** — Otra fuente (como la carga de un perfil) puede haber sobrescrito `ClientCompTxAttackMs` o `ClientCompTxReleaseMs`. Reajuste y el nuevo valor persistirá de inmediato.
- **El valor del editor en línea es rechazado** — La entrada debe ser un número válido dentro del rango válido del control. Si el valor está fuera del rango, se ajusta automáticamente. Los caracteres no numéricos (distintos de separadores decimales, signo y coma) hacen que la edición se ignore.

## Soporte de temas

El applet del compresor y su widget de curva de transferencia ahora respetan el tema actual de AetherSDR. Los colores de los siguientes elementos se toman de las variables del tema en lugar de valores fijos:

| Elemento                  | Variable del tema       |
|---------------------------|-------------------------|
| Fondo del widget          | `color.background.0`   |
| Líneas de cuadrícula      | `color.background.1`   |
| Etiquetas de ejes         | `color.text.label`     |
| Línea de unidad (identidad) | `color.background.1` |
| Curva de transferencia    | `color.accent.dim`     |
| Brillo de la bola de envolvente | `color.accent.warning` |
| Núcleo de la bola de envolvente | `color.text.primary` |

El relleno del control deslizante de reducción de ganancia usa el color del tema `color.slider.foreground` aplicado en el ámbito `applet/comp` a través de ThemeManager.

## Relacionados

- [Aetherial Compressor (TX) / Aetherial AGC-C (RX) overview](overview.md)
- [Adjust compressor threshold (TX or RX side)](adjust-compressor-threshold-tx-or-rx-side.md)
- [Set compression ratio for voice (TX) or for received audio (RX AGC-C)](set-compression-ratio-for-voice-tx-or-for-received-audio-rx-agc-c.md)
- [Apply make-up gain after compression](apply-make-up-gain-after-compression.md)
- [Watch live gain reduction while speaking or listening](watch-live-gain-reduction-while-speaking-or-listening.md)
- [Open the full Compressor editor for knee and limiter controls](open-the-full-compressor-editor-for-knee-and-limiter-controls.md)
