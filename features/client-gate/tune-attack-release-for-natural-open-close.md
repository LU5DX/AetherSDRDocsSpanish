# Ajuste de ataque y liberación para una apertura/cierre natural

Ajuste la rapidez con que el noise gate se abre al comenzar a hablar y se cierra al dejar de hacerlo. Los tiempos correctos de ataque y liberación evitan cortar la primera sílaba de una palabra y previenen un corte brusco e innatural entre palabras.

## Antes de comenzar

- La etapa Gate debe estar habilitada. Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md) si la etapa está actualmente desactivada.
- Abra el applet GATE: localice el subcontenedor GATE dentro del contenedor padre PooDoo Audio (TXDSP) en el panel de applets. Si no es visible, haga doble clic en la etapa Gate del widget CHAIN para abrir el editor flotante Gate, o haga clic derecho en la barra de título del subcontenedor GATE y elija mostrarlo.
- Tenga un micrófono conectado y audio en tránsito para que la bola de entrada de la curva de transferencia y la barra de reducción de ganancia reaccionen en tiempo real mientras realiza ajustes.

## Pasos

1. Observe la barra de reducción de ganancia mientras habla con normalidad. La franja ámbar debe llenarse brevemente con audio fuerte y vaciarse entre palabras. Si el gate corta el inicio de cada palabra, el Attack es demasiado lento; si se cierra de golpe a mitad de una respiración con un clic audible, el Release es demasiado rápido.
2. Para corregir el corte al inicio de las palabras, gire el control **Attack** hacia la izquierda (valor menor). El valor predeterminado es 0.50 ms. Para la mayoría del trabajo de voz, valores entre 0.1 ms y 2.0 ms abren con suficiente rapidez para preservar las consonantes.
3. Para corregir un cierre brusco o intermitente, gire el control **Release** hacia la derecha (valor mayor). El valor predeterminado es 100 ms. Un valor de 150–300 ms permite que el gate permanezca abierto durante las pausas naturales sin cerrarse bruscamente entre sílabas.
4. Pronuncie una frase y observe la bola de entrada en la curva de transferencia. La bola debe cruzar la línea de umbral de forma limpia al comenzar cada palabra, sin una detención visible en el umbral.
5. Observe cómo la barra de reducción de ganancia se vacía suavemente después de cada palabra. Si la franja ámbar persiste demasiado o provoca un efecto de bombeo, reduzca el Release hacia 50–100 ms.
6. Repita los pasos 2–5 hasta que la apertura y el cierre se perciban transparentes durante el habla normal.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| **Attack** | 0.50 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Define la rapidez con que el gate se abre cuando la entrada supera el umbral. Escala de control exponencial. La etiqueta muestra `X.XX ms` por debajo de 10 ms y `X.X ms` por encima. |
| **Release** | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Define la rapidez con que el gate se cierra cuando la entrada cae por debajo del umbral. Escala de control exponencial. La etiqueta muestra `X.X ms` por debajo de 100 ms y `X ms` por encima. |
| **Barra de reducción de ganancia** | — | 0 a 40 dB GR | — | Franja ámbar horizontal, rellena desde la derecha. Muestra la profundidad de atenuación mientras el gate está cerrado. La marca de referencia en −15 dB corresponde al valor predeterminado de Floor. |
| **Curva de transferencia** | — | — | — | Representa la curva de transferencia estática con una bola de entrada en vivo. La posición de la bola indica si el gate está actualmente por encima o por debajo del umbral. |

## Consejos

- Attack y Release utilizan escala de control exponencial, por lo que los movimientos pequeños cerca del extremo inferior del rango producen cambios en milisegundos mayores que el mismo movimiento cerca del extremo superior. Realice ajustes pequeños y vuelva a probar después de cada uno.
- Si el gate oscila rápidamente —abriéndose y cerrándose varias veces por palabra— aumente primero el Release. Si eso solo no es suficiente, suba también ligeramente el control **Thresh** para que el audio en niveles límite no cruce repetidamente el umbral.
- La barra de reducción de ganancia y la bola de entrada se actualizan aproximadamente cada 33 ms. Observe ambas mientras pronuncia un pasaje que represente su situación de ruido más desfavorable, no solo palabras aisladas.
- Los cambios tienen efecto de inmediato y se guardan automáticamente. No se requiere ningún paso de guardado adicional.

## Solución de problemas

- **Se corta la primera consonante de cada palabra** — El Attack es demasiado lento. Reduzca Attack hacia 0.1 ms.
- **El gate se cierra de forma audible entre sílabas dentro de una misma palabra** — El Release es demasiado corto. Aumente Release a 150 ms o más y vuelva a probar.
- **El gate oscila entre abierto y cerrado rápidamente** — El nivel de entrada está rondando el umbral. Aumente Release a al menos 200 ms, o suba ligeramente Thresh para que los niveles marginales no activen el gate. Consulte [Establecer el umbral justo por encima del piso de ruido ambiente](set-threshold-just-above-room-noise-floor.md).
- **La barra de reducción de ganancia no se mueve** — Es posible que la etapa Gate esté desactivada o deshabilitada. Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md).
- **Los valores del control no coinciden con lo que se muestra en el editor flotante Gate** — El applet sincroniza desde el motor aproximadamente cada 33 ms. Espere un momento; los valores deben reconciliarse automáticamente.

## Relacionados

- [Descripción general del Noise Gate / Expansor](overview.md)
- [Establecer el umbral justo por encima del piso de ruido ambiente](set-threshold-just-above-room-noise-floor.md)
- [Establecer Floor para evitar silencios inaturales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Observar la reducción de ganancia en vivo mientras no se habla](watch-live-gr-while-not-speaking.md)
- [Elegir el comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md)
