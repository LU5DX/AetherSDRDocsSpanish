# Ajustar el Floor para evitar el silencio antinatural entre palabras

El control Floor limita la profundidad máxima de atenuación que puede aplicar el gate a su audio. Sin un floor definido, un gate duro corta completamente al silencio entre palabras, lo que suena antinatural en voz. Establecer un floor moderado permite que pase una pequeña cantidad de audio mientras el gate está cerrado, preservando la sensación de una transmisión en vivo.

## Antes de comenzar

- La etapa Gate debe estar habilitada. Consulte [Omitir el gate desde la cadena](bypass-the-gate-from-the-chain.md) para confirmar que la etapa está activa.
- Abra el applet GATE: es el subcontenedor etiquetado GATE dentro del contenedor principal PooDoo Audio (TXDSP). Si no está visible, haga doble clic en la etapa Gate en el widget CHAIN para abrir el editor flotante de Gate, o haga clic derecho en la barra de título del subcontenedor GATE y seleccione la opción correspondiente.

## Pasos

1. Localice el control Floor en la fila de cinco controles en la parte inferior del applet GATE. Es el control más a la derecha, etiquetado "Floor".
2. Observe la barra de reducción de ganancia (Gain-reduction) mientras hace una pausa al hablar. El relleno ámbar muestra cuánta atenuación está aplicando el gate en ese momento. La marca de referencia en la posición -15 dB señala el floor predeterminado.
3. Gire el control Floor en sentido horario (hacia 0 dB) para reducir la atenuación máxima y permitir que pase más audio cuando el gate está cerrado.
4. Gire el control Floor en sentido antihorario (hacia -80 dB) para aumentar la atenuación máxima y cortar más profundamente entre palabras.
5. Hable normalmente y haga pausas deliberadas. Ajuste hasta que las transiciones entre palabras suenen naturales, sin que sean abruptamente silenciosas ni inusualmente calladas.

## Qué hace cada control

| Control | Valor predeterminado | Rango válido | Clave de persistencia | Comportamiento |
|---|---|---|---|---|
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que el gate puede aplicar. Valores más altos (más cercanos a 0 dB) permiten que pase más audio cuando el gate está cerrado. Valores más bajos cortan más profundamente. |
| Barra de reducción de ganancia | — | 0 a 40 dB GR | — | Franja ámbar horizontal, rellena desde la derecha. Muestra la profundidad de atenuación mientras el gate está cerrado. La marca en -15 dB señala la posición del floor predeterminado. |

## Consejos

- El Floor predeterminado de -15.0 dB es moderado de forma intencional. Mantiene una señal residual tenue entre palabras, que la mayoría de los oyentes considera más natural que el silencio completo.
- Si está usando un Ratio bajo (comportamiento de expansor suave), el gate puede que nunca alcance el Floor incluso con la atenuación máxima — el Floor solo limita el máximo, no establece un objetivo.
- La curva de transferencia del applet GATE se actualiza para reflejar su ajuste de Floor. Observe el plateau inferior de la curva mientras realiza ajustes para ver el efecto visualmente junto con la bola de entrada en tiempo real.
- Los cambios se guardan de inmediato. El valor de Floor persiste entre reinicios mediante `ClientGateTxFloorDb`.

## Solución de problemas

- **El audio se corta a silencio completo entre palabras a pesar de un valor de Floor alto** — Confirme que la etapa de gate no está en bypass. Revise la barra de reducción de ganancia: si muestra el relleno ámbar completo llegando al borde derecho, el gate está aplicando la atenuación máxima. Suba el Floor (más cercano a 0 dB) y observe la barra para confirmar que limita el relleno.
- **El control Floor no tiene efecto audible** — Es posible que el gate no esté disparándose. Si la bola de entrada en la curva de transferencia permanece por encima del umbral, el gate está abierto y el Floor no se está aplicando. Baje Thresh para que el gate realmente se cierre entre palabras.

## Temas relacionados

- [Descripción general del Noise Gate / Expansor](overview.md)
- [Ajustar el umbral justo por encima del nivel de ruido ambiental](set-threshold-just-above-room-noise-floor.md)
- [Elegir el comportamiento de gate o expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Ajustar el ataque y la liberación para una apertura y cierre naturales](tune-attack-release-for-natural-open-close.md)
- [Observar la reducción de ganancia en tiempo real mientras no se habla](watch-live-gr-while-not-speaking.md)
