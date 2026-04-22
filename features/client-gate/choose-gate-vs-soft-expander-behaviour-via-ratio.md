# Elegir el comportamiento de puerta o expansor suave mediante el ratio

El control Ratio determina si el Noise Gate / Expander actúa como un expansor descendente suave o como una puerta de ruido dura. Ajustarlo permite adaptar el carácter del procesamiento a su micrófono y entorno operativo.

## Antes de comenzar

- El applet GATE debe estar visible en el panel de applets. Si está oculto, habilite la etapa Gate mediante el widget CHAIN o haga doble clic en la etapa Gate del widget CHAIN para abrir el editor flotante de Gate.
- La etapa Gate debe estar habilitada. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md) si necesita activarla primero.
- El audio de transmisión debe estar fluyendo para que la curva de transferencia y la barra de reducción de ganancia reflejen el comportamiento en tiempo real mientras realiza los ajustes.

## Pasos

1. Localice el control Ratio en el applet GATE. Es el segundo control desde la izquierda en la fila de cinco controles, etiquetado como "Ratio".
2. Observe la curva de transferencia. La curva se vuelve más pronunciada al aumentar el Ratio, lo que muestra con qué agresividad el procesador atenúa la señal por debajo del umbral.
3. Gire Ratio hacia **1.0:1** para obtener un comportamiento de expansor suave. Con valores de ratio bajos, el audio por debajo del umbral se reduce de forma suave en lugar de cortarse bruscamente: las pausas entre palabras siguen siendo audibles, aunque más silenciosas.
4. Gire Ratio hacia **10.0:1** para obtener un comportamiento de puerta dura. Con valores de ratio altos, el audio por debajo del umbral se corta de forma abrupta, produciendo un silencio casi total entre palabras.
5. Hable con normalidad y observe la barra de reducción de ganancia. El relleno ámbar indica la profundidad de atenuación actual. La marca a −15 dB en la barra señala el valor predeterminado de Floor; si el relleno ámbar alcanza o supera regularmente esa marca con el ratio seleccionado, considere ajustar Floor. Consulte [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Ratio | 2.0 | 1.0 a 10.0 | `ClientGateTxRatio` | Mapeo lineal. Se muestra como X.X:1. Los valores más bajos producen una expansión descendente suave; los valores más altos producen un corte más duro, similar al de una puerta. |
| Thresh | −40.0 dB | −80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual la puerta comienza a atenuar. Establece el punto en que Ratio surte efecto. |
| Floor | −15.0 dB | −80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que la puerta puede aplicar, independientemente del Ratio. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja ámbar horizontal rellena desde la derecha. Muestra la profundidad de atenuación actual. La marca a −15 dB señala el Floor predeterminado. |
| Curva de transferencia | — | — | — | Representa la curva estática de entrada a salida y un punto en tiempo real en el nivel de entrada actual. |

## Consejos

- Comience con Ratio en 2.0:1 (el valor predeterminado) y auméntelo solo hasta que el ruido de fondo desaparezca entre transmisiones. Valores de ratio innecesariamente altos hacen que la voz suene cortada.
- El punto en tiempo real sobre la curva de transferencia indica si la puerta está abierta (punto por encima de la rodilla del umbral) o cerrada (punto por debajo). Úselo junto con la barra de reducción de ganancia para evaluar si Ratio está ajustado correctamente antes de salir al aire.
- Los cambios en Ratio se guardan inmediatamente en `ClientGateTxRatio` y se conservan tras un reinicio. No es necesario ningún paso de guardado adicional.
- Si la puerta se cierra demasiado lento después de dejar de hablar, un Ratio alto hará que el final de las palabras suene cortado. Ajuste Release en conjunto con Ratio. Consulte [Ajustar ataque/liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md).

## Solución de problemas

- **El control Ratio no tiene efecto sobre la curva de transferencia** — Es posible que la etapa Gate esté omitida. Verifique el widget CHAIN y confirme que la etapa Gate está activa. Consulte [Omitir la puerta desde la cadena](bypass-the-gate-from-the-chain.md).
- **La puerta corta el inicio o el final de las palabras incluso con un Ratio moderado** — Es posible que Thresh esté configurado demasiado alto, lo que hace que la puerta se cierre ante transitorios de voz. Baje Thresh para que la rodilla quede por debajo del nivel de su voz. Consulte [Ajustar el umbral justo por encima del nivel de ruido ambiental](set-threshold-just-above-room-noise-floor.md). Verifique también Attack y Release. Consulte [Ajustar ataque/liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md).
- **El ruido de fondo sigue siendo audible con un Ratio alto** — Es posible que Floor esté limitando la cantidad de atenuación aplicada. Baje Floor por debajo del nivel del piso de ruido. Consulte [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md).

## Relacionados

- [Descripción general del Noise Gate / Expander](overview.md)
- [Ajustar el umbral justo por encima del nivel de ruido ambiental](set-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Ajustar ataque/liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Observar la reducción de ganancia en tiempo real mientras no se transmite](watch-live-gr-while-not-speaking.md)
