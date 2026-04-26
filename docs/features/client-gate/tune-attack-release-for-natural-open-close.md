# Ajuste del Attack y Release para una apertura/cierre natural

Ajuste la velocidad con que el noise gate se abre al comenzar a hablar y se cierra al dejar de hacerlo. Unos tiempos correctos de attack y release evitan que el gate recorte el inicio de las palabras o produzca un corte audible al final de cada transmisión.

## Antes de comenzar

- El applet GATE debe estar visible en el panel de applets. Aparece como un subcontenedor dentro del contenedor principal PooDoo Audio (TXDSP). Si está oculto, habilite la etapa Gate mediante el widget CHAIN o haga doble clic en la etapa Gate en el widget CHAIN para abrir el editor flotante de Gate.
- El gate debe estar habilitado. Consulte [Desactivar el gate desde la cadena](bypass-the-gate-from-the-chain.md) si el gate está actualmente en bypass.
- Establezca un umbral de trabajo antes de ajustar los tiempos. Consulte [Ajustar el umbral justo por encima del nivel de ruido ambiente](set-threshold-just-above-room-noise-floor.md).

## Pasos

1. Abra el applet GATE dentro del contenedor PooDoo Audio (TXDSP). Los cinco controles — Thresh, Ratio, Attack, Release, Floor — aparecen en fila debajo de la curva de transferencia y la barra de reducción de ganancia.
2. Active el micrófono y hable normalmente mientras observa la barra de reducción de ganancia. La franja ámbar se contrae hacia la izquierda cuando el gate se abre y se expande hacia la derecha cuando se cierra.
3. Gire el control Attack mientras habla. Los valores más bajos abren el gate más rápido; aumente el valor si el gate se abre demasiado bruscamente y provoca un efecto de bombeo audible en señales fuertes. La etiqueta muestra el valor actual en milisegundos (por ejemplo, `0.50 ms`).
4. Haga pausas entre palabras y observe cómo se rellena la barra de reducción de ganancia. Gire el control Release para determinar la velocidad con que el gate se cierra después de que su voz caiga por debajo del umbral. Los valores más cortos cierran el gate rápidamente; los valores más largos permiten que la cola de cada palabra decaiga de forma natural antes de que comience la atenuación.
5. Repita los pasos 3 y 4 hasta que el habla pase sin consonantes recortadas al abrirse y sin cortes bruscos al cerrarse.

## Función de cada control

| Control | Valor predeterminado | Rango válido | Clave persistida | Comportamiento |
|---|---|---|---|---|
| Attack | 0.5 ms | 0.1 a 100.0 ms | `ClientGateTxAttackMs` | Determina la rapidez con que el gate se abre cuando la entrada supera el umbral. Mapeado exponencialmente: desde el mínimo hasta el máximo abarca de 0.1 ms a 100.0 ms. |
| Release | 100 ms | 5 a 2000 ms | `ClientGateTxReleaseMs` | Determina la rapidez con que el gate se cierra cuando la entrada cae por debajo del umbral. Mapeado exponencialmente: desde el mínimo hasta el máximo abarca de 5 ms a 2000 ms. |
| Thresh | -40.0 dB | -80.0 a 0.0 dB | `ClientGateTxThresholdDb` | Nivel por debajo del cual el gate comienza a atenuar. Afecta al momento en que se activan los tiempos de Attack y Release. |
| Floor | -15.0 dB | -80.0 a 0.0 dB | `ClientGateTxFloorDb` | Atenuación máxima que aplica el gate cuando está cerrado. No afecta a los tiempos, pero limita la profundidad del corte durante la fase de release. |

## Consejos

- Comience con el Attack en el valor predeterminado (0.5 ms) y ajuste primero el Release. El Release tiene mayor efecto sobre la naturalidad percibida.
- Si el inicio de las palabras suena recortado, aumente el Attack ligeramente (pruebe entre 2 y 5 ms) para que el gate tenga tiempo de abrirse antes de que llegue el transitorio.
- Si el gate oscila — abriéndose y cerrándose rápidamente — aumente el Release para suavizar las pausas breves dentro de una palabra.
- La bola en movimiento sobre la curva de transferencia indica si el gate está actualmente por encima o por debajo del umbral. Obsérvela seguir su voz para confirmar que los cambios de temporización están surtiendo efecto.
- Los controles Attack y Release se sincronizan bidireccionalmente con el editor flotante de Gate. Los cambios realizados en cualquiera de las dos vistas se reflejan inmediatamente en la otra.

## Resolución de problemas

- **Las consonantes iniciales se recortan** — El Attack es demasiado rápido en relación con el tiempo de subida de la señal, o el Thresh está demasiado alto. Reduzca el Thresh ligeramente o aumente el Attack (pruebe entre 2 y 10 ms) para permitir que el gate se abra antes del transitorio.
- **El gate se cierra bruscamente en medio de una palabra durante pausas normales** — El Release es demasiado corto. Aumente el Release hacia valores de 200–500 ms para que las pausas breves no provoquen el cierre.
- **El gate no se cierra entre palabras** — Es posible que el Release sea muy largo o que el Thresh esté por debajo del nivel de ruido ambiente. Compruebe primero el Thresh (consulte [Ajustar el umbral justo por encima del nivel de ruido ambiente](set-threshold-just-above-room-noise-floor.md)) y luego reduzca el Release.
- **La barra de reducción de ganancia no se mueve** — Es posible que el gate esté en bypass o que el motor de audio no esté conectado. Confirme que la etapa Gate está activa en el widget CHAIN.

## Relacionados

- [Ajustar el umbral justo por encima del nivel de ruido ambiente](set-threshold-just-above-room-noise-floor.md)
- [Ajustar el Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir entre gate y expansor suave mediante el ratio](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar la reducción de ganancia en tiempo real sin hablar](watch-live-gr-while-not-speaking.md)
- [Desactivar el gate desde la cadena](bypass-the-gate-from-the-chain.md)
