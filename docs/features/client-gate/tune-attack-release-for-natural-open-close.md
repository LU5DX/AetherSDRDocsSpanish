# Ajuste de Attack y Release para una apertura/cierre natural

Ajuste los controles **Attack** y **Release** para controlar la rapidez con que la puerta se abre cuando habla y la rapidez con que se cierra cuando deja de hablar. Un tiempo correcto evita el recorte de las sílabas iniciales y los cortes abruptos entre palabras.

## Antes de comenzar

- La etapa Gate debe estar habilitada en el lado que desea ajustar (TX o RX). Consulte [Desactivar la puerta desde la cadena](bypass-the-gate-from-the-chain.md) si la etapa aún no está activa.
- Abra el subcontenedor "Aetherial TX Gate" o "Aetherial AGC-T" dentro del contenedor principal Aetherial Audio (TXDSP), o haga doble clic en la etapa GATE en el widget CHAIN para abrir el editor flotante de ese lado.
- Reproduzca audio o hable al micrófono para que la barra de reducción de ganancia se mueva mientras realiza los ajustes.

## Pasos

1. Localice la fila de controles en la parte inferior del applet. Encuentre el control etiquetado **Attack** (tercer control desde la izquierda en TX; misma posición en RX).
2. Gire **Attack** hacia la izquierda (valores menores) para que la puerta se abra más rápido ante transitorios fuertes; gírelo hacia la derecha (valores mayores) para ralentizar la apertura y suavizar las entradas abruptas. El valor predeterminado es 0.5 ms. El rango válido es de 0.1 a 100.0 ms.
3. Observe la bola de entrada en vivo sobre la curva de transferencia. Al comenzar a hablar, la bola debe moverse por encima del umbral y la barra de reducción de ganancia debe despejarse con prontitud sin recortar el borde inicial.
4. Localice el control etiquetado **Release** (cuarto control desde la izquierda).
5. Gire **Release** hacia la derecha (valores mayores) para que la puerta se cierre más lentamente después de que el audio caiga por debajo del umbral — esto suaviza la cola entre palabras. Gírelo hacia la izquierda para cerrar más rápido y cortar el ruido de fondo de forma más agresiva. El valor predeterminado es 100 ms. El rango válido es de 5 a 2000 ms.
6. Pronuncie una frase con pausas naturales y observe la barra de reducción de ganancia. El relleno ámbar debe crecer de forma suave durante el silencio y retraerse con claridad cuando se reanuda la voz, sin bombeo ni saltos repentinos.
7. Si la puerta se cierra bruscamente a mitad de una palabra, aumente **Release**. Si el ruido de fondo se filtra entre oraciones, disminuya **Release**.
8. Si la primera sílaba de cada palabra resulta atenuada, disminuya **Attack**. Si la puerta se abre con ruido de respiración antes del habla, aumente **Attack**.

## Qué hace cada control

| Control | Predeterminado | Rango válido | Clave persistida (TX / RX) | Comportamiento |
|---|---|---|---|---|
| Attack | 0.5 ms | 0.1 – 100.0 ms | `ClientGateTxAttackMs` / `ClientGateRxAttackMs` | Define la rapidez con que la puerta se abre cuando la entrada supera el umbral. Utiliza mapeo exponencial. |
| Release | 100 ms | 5 – 2000 ms | `ClientGateTxReleaseMs` / `ClientGateRxReleaseMs` | Define la rapidez con que la puerta se cierra después de que la entrada cae por debajo del umbral. Utiliza mapeo exponencial. |

## Consejos

- La barra de reducción de ganancia alcanza un máximo de 40 dB y la marca de referencia en la posición −15 dB corresponde al valor predeterminado de Floor. Use esta marca como referencia visual: si el relleno ámbar rara vez llega a la marca, el ajuste de Floor es el límite determinante, no la relación ni los tiempos.
- Los cambios realizados en los controles del applet acoplado y en el editor flotante se mantienen sincronizados automáticamente. No es necesario volver a abrir ninguna de las dos vistas tras ajustar una.
- Para voz en SSB, un Release de 150–300 ms generalmente evita que la puerta se cierre durante las breves pausas entre palabras. Para tonos de audio en CW, un Release mucho más corto (10–30 ms) produce un resultado más limpio.

## Solución de problemas

- **La primera sílaba de cada palabra se corta** — Attack es demasiado lento. Gire el control **Attack** hacia la izquierda, acercándose a 0.1 ms, para que la puerta se abra antes de que pase el transitorio.
- **La puerta vibra o fluctúa entre abierta y cerrada** — Release es demasiado corto, o Thresh está configurado cerca del nivel de la señal. Aumente **Release** o disminuya ligeramente **Thresh** para que la puerta no se reactive con la respiración y el ruido ambiental.
- **El ruido de fondo es audible entre palabras** — Release es demasiado largo. Gire **Release** hacia la izquierda para acortar la cola. Verifique también que **Floor** esté configurado con un valor suficientemente negativo para atenuar el ruido cuando la puerta está cerrada.
- **La posición del control no coincide con lo que se configuró en el editor flotante** — El applet se sincroniza con el motor aproximadamente cada 33 ms. Espere un momento; la posición del control se actualizará para reflejar el valor actual del motor.

## Relacionados

- [Descripción general de Aetherial TX Gate / Aetherial AGC-T (RX)](overview.md)
- [Ajustar el umbral TX justo por encima del nivel de ruido ambiental](set-tx-threshold-just-above-room-noise-floor.md)
- [Ajustar Floor para evitar silencios artificiales entre palabras](set-floor-to-avoid-unnatural-silence-between-words.md)
- [Elegir el comportamiento de puerta o expansor suave mediante la relación](choose-gate-vs-soft-expander-behaviour-via-ratio.md)
- [Observar la reducción de ganancia en vivo sin hablar](watch-live-gr-while-not-speaking.md)
